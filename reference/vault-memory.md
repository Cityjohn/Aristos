# Vault-Memory: Specification

> Obsidian vault indexing with vector search and associative graph traversal.
> OpenClaw skill for `memory_search` and coaching context retrieval.

---

## 1. Overview

Index John's Obsidian vault into a local SQLite database with vector embeddings and wiki-link graph edges. Enable semantic search (find notes by meaning) and associative traversal (follow `[[wiki links]]` to related notes). Hybrid scoring combines both.

**Target:** Coaching sessions, pattern discussions, "remember when" questions. Not for quick daily chat.

## 2. Indexed Scope

Three directories under `/home/cityjohn/Obsidian/Journal/`:

| Directory | Content |
|---|---|
| `Journal/` | Day to Day, Weekly reflection, Yearly planning, Templates |
| `Journal/Aris Coaching/` | Strategies, patterns, insights, learnings |
| `Journal/Our Knowledge/` | Shared research, discoveries, concepts |

**Excluded:** Templates folder (not useful for retrieval), any `.obsidian/` config.

## 3. Architecture

```
┌─────────────────────────────────────────────┐
│               Vault-Memory Skill             │
├──────────┬──────────┬──────────┬─────────────┤
│ Indexer  │ Embedder │ Graph    │ Query Engine│
│          │          │ Builder  │             │
├──────────┴──────────┴──────────┴─────────────┤
│         vault-memory.db (SQLite)             │
│  ┌────────────┐  ┌──────────┐  ┌──────────┐ │
│  │  notes     │  │ vec_     │  │ edges    │ │
│  │  (meta)    │  │ notes    │  │ (graph)  │ │
│  └────────────┘  └──────────┘  └──────────┘ │
├─────────────────────────────────────────────┤
│  OpenRouter API (text-embedding-3-large)    │
└─────────────────────────────────────────────┘
```

## 4. Database Schema

### 4.1 `notes` table
```sql
CREATE TABLE notes (
    id          INTEGER PRIMARY KEY AUTOINCREMENT,
    path        TEXT UNIQUE NOT NULL,        -- relative path from vault root
    title       TEXT NOT NULL,               -- filename without .md
    content     TEXT NOT NULL,               -- full markdown content
    content_hash TEXT NOT NULL,              -- sha256 of content (change detection)
    word_count  INTEGER NOT NULL,
    modified_at TEXT NOT NULL,               -- ISO 8601 file mtime
    indexed_at  TEXT NOT NULL,               -- when we last indexed this
    directory   TEXT NOT NULL                -- which indexed directory it belongs to
);
```

### 4.2 `vec_notes` virtual table (sqlite-vec)
```sql
CREATE VIRTUAL TABLE vec_notes USING vec0(
    embedding float[3072]   -- text-embedding-3-large output
);
```
Row ID matches `notes.id`.

### 4.3 `edges` table (wiki-link graph)
```sql
CREATE TABLE edges (
    id          INTEGER PRIMARY KEY AUTOINCREMENT,
    source_id   INTEGER NOT NULL REFERENCES notes(id),
    target_id   INTEGER NOT NULL REFERENCES notes(id),
    link_text   TEXT,                        -- display text if any
    UNIQUE(source_id, target_id)
);

CREATE INDEX idx_edges_source ON edges(source_id);
CREATE INDEX idx_edges_target ON edges(target_id);
```

### 4.4 `index_state` table
```sql
CREATE TABLE index_state (
    key   TEXT PRIMARY KEY,
    value TEXT NOT NULL
);
```
Tracks: `last_full_index`, `last_incremental`, `total_notes`, `total_edges`.

## 5. Configuration

File: `~/.openclaw/vault-memory.json`

```json
{
  "vault_root": "/home/cityjohn/Obsidian/Journal",
  "indexed_dirs": [
    "Journal/Day to Day",
    "Journal/Weekly reflection",
    "Journal/Yearly planning",
    "Journal/Aris Coaching",
    "Journal/Our Knowledge"
  ],
  "excluded_dirs": ["Templates"],
  "db_path": "~/.openclaw/vault-memory.db",
  "embedding_model": "openrouter/text-embedding-3-large",
  "embedding_dim": 3072,
  "chunk_size": 1000,
  "chunk_overlap": 200,
  "hybrid_weights": {
    "vector": 0.7,
    "graph": 0.3
  },
  "graph_hops": 2,
  "graph_decay": 0.5,
  "watcher_debounce_min": 10,
  "nightly_cron": "0 2 * * *",
  "auth_profile": "openrouter:main"
}
```

## 6. Indexing Pipeline

### 6.1 Full index (nightly cron)

1. Walk all `indexed_dirs`, collect `.md` files
2. For each file:
   - Read content, compute sha256
   - Compare with `notes.content_hash` — skip if unchanged
   - Insert/update `notes` row
   - Chunk content (1000 tokens, 200 overlap)
   - Batch-embed chunks via OpenRouter API (batch of 16)
   - Store mean-pooled embedding in `vec_notes`
   - Parse `[[wiki links]]` → resolve to target note IDs → insert `edges`
3. Delete `notes` rows for files that no longer exist
4. Update `index_state`

### 6.2 Incremental index (file watcher)

- Debounced: waits 10 min after last filesystem event before triggering
- Only re-indexes files where `mtime > indexed_at`
- Same pipeline as full, but scoped to changed files only

### 6.3 Chunking strategy

- Split on double newline first (paragraphs)
- If paragraph > chunk_size, split on sentence boundaries
- Overlap: last 200 tokens of previous chunk prepended to next
- Each chunk embedded separately, final note embedding = mean pool of chunks

### 6.4 Wiki-link parsing

Regex: `\[\[([^\]|]+)(?:\|[^\]]+)?\]]`

- Extract target page name
- Resolve to `notes.id` by matching `title` (case-insensitive)
- Create bidirectional edges (A→B and B→A) for graph traversal
- Unresolved links (target doesn't exist) stored with `target_id = NULL` for future resolution

## 7. Query Engine

### 7.1 API

Single function exposed to the agent:

```
vault_memory_search(query: string, options?: {
    max_results?: number,       // default 5
    min_score?: number,         // default 0.3
    directory_filter?: string,  // restrict to one indexed dir
    include_graph?: boolean,    // default true
}) → Result[]
```

### 7.2 Hybrid scoring

```
Result = {
    note_id: number,
    path: string,
    title: string,
    snippet: string,           // relevant excerpt (±200 chars around match)
    vector_score: number,      // cosine similarity 0-1
    graph_score: number,       // graph proximity 0-1
    hybrid_score: number,      // 0.7 * vector + 0.3 * graph
}
```

**Graph score calculation:**
1. Start from top-K vector results (K=10)
2. For each candidate, traverse edges up to `graph_hops` (2)
3. Each hop: multiply by `graph_decay` (0.5)
4. Sum incoming graph scores from all paths
5. Normalize to 0-1 range

### 7.3 Query flow

1. Embed query via OpenRouter API
2. Vector search: `SELECT id, distance FROM vec_notes WHERE embedding MATCH ? ORDER BY distance LIMIT 10`
3. Convert cosine distance to similarity score
4. Graph expansion: for top 10 vector results, traverse 2 hops, compute graph scores
5. Merge: `hybrid = 0.7 * vector + 0.3 * graph`
6. Filter by `min_score`, limit to `max_results`
7. Fetch note metadata and generate snippets

## 8. OpenClaw Skill Integration

### 8.1 Skill structure

```
~/.openclaw/skills/vault-memory/
├── SKILL.md              # Skill definition + usage instructions
├── README.md             # Human-readable docs
├── package.json          # Metadata
├── scripts/
│   ├── index.mjs         # Full/incremental indexer
│   ├── search.mjs        # Query engine (CLI)
│   ├── watcher.mjs       # File watcher daemon
│   └── lib/
│       ├── db.mjs        # SQLite + sqlite-vec setup
│       ├── embed.mjs     # OpenRouter embedding calls
│       ├── chunk.mjs     # Text chunking
│       ├── graph.mjs     # Wiki-link parsing + graph ops
│       └── score.mjs     # Hybrid scoring
└── config/
    └── schema.json       # JSON schema for vault-memory.json
```

### 8.2 CLI commands

```bash
vault-memory index [--full]        # Run indexer (default: incremental)
vault-memory search "query"        # Search and print results
vault-memory stats                 # Show index stats
vault-memory watch                 # Start file watcher daemon
vault-memory reindex <path>       # Force reindex single file
```

### 8.3 Agent integration

The skill hooks into `memory_search`:
- `memory_search` first checks MEMORY.md + memory/*.md (existing behavior)
- Then calls `vault-memory search` for vault results
- Merges results, returns unified list

## 9. Dependencies

| Dependency | Purpose |
|---|---|
| `better-sqlite3` | SQLite bindings (Node.js) |
| `sqlite-vec` | Vector similarity search extension |
| `chokidar` | File watcher (debounced) |
| OpenRouter API key | Embedding generation |

## 10. Cost Estimate

- **Embedding model:** OpenRouter text-embedding-3-large
- **~400 notes × 3 chunks avg = ~1200 embeddings**
- **Cost:** ~$0.0001 per 1K tokens, ~$0.02 total for full index
- **Incremental:** Only changed files, negligible
- **Query:** ~$0.0001 per search (single embedding)

## 11. Implementation Order

1. **DB setup** — schema, sqlite-vec, migrations
2. **Embedding module** — OpenRouter API wrapper, batch support
3. **Chunker** — paragraph + sentence splitting, overlap
4. **Graph parser** — wiki-link regex, edge resolution
5. **Indexer** — full index pipeline
6. **Query engine** — vector search + graph traversal + hybrid scoring
7. **CLI** — index/search/stats/watch commands
8. **Watcher** — chokidar + debounced incremental
9. **SKILL.md** — integration with memory_search
10. **Cron** — nightly full index job

## 12. Limitations & Comparison to HippoRAG

### What this approach does

Our graph layer traverses explicit `[[wiki links]]` up to 2 hops with fixed decay (×0.5). It's a useful supplement to vector search but **not true associative spreading activation**.

**Limitations:**
- Only captures explicit links — if two topics are conceptually related but never wiki-linked, the graph contributes nothing
- 2-hop hard cutoff is arbitrary — real memory associations chain much deeper
- Fixed decay is a rough heuristic, not learned from data
- SQLite CTEs for recursive traversal are slow beyond 2-3 hops on large graphs

### What HippoRAG does differently

HippoRAG (arXiv:2405.14831) models memory after the hippocampus. Key differences:

1. **Knowledge graph from LLM extraction** — doesn't rely on user-created links. An LLM reads each note and extracts entity-relation-entity triples automatically. Two notes about genetics and IQ get connected because the model identifies shared entities, even if John never wiki-linked them.

2. **Personalized PageRank (PPR) for spreading activation** — instead of hard hop limits, PPR propagates activation across the entire graph. A "query node" is created from the search query, connected to relevant graph nodes, then PageRank runs. Activation spreads naturally — strong connections carry more, weak connections carry less, and it converges across the full graph without arbitrary depth limits.

3. **OpenIE triples as edges** — edges aren't binary (exists/doesn't). They carry relation types ("causes," "is_a," "contradicts") which lets the model distinguish between "A supports B" and "A contradicts B."

4. **Dense-sparse integration** — combines dense retrieval (embeddings) with sparse retrieval (PPR over the graph) at a fundamental level, not just score merging. The graph informs WHICH nodes are relevant, not just adds a bonus to already-found nodes.

### Why we don't use HippoRAG

- **Complexity:** Requires LLM-based triple extraction per note (slow, expensive at scale)
- **Runtime:** PPR over 400+ nodes with thousands of triples is heavier than our 2-hop CTE
- **Overkill for 400 notes:** The overhead of triple extraction + PPR pays off at thousands of notes. For John's vault, explicit wiki links + vectors is pragmatic.
- **HippoRAG 2 (arXiv:2502.14802)** improves associativity further but adds even more complexity

### Future upgrade path

If the vault grows to 1000+ notes or the graph starts missing obvious connections:
1. Run HippoRAG's triple extraction as a nightly batch (not per-query)
2. Store triples in the edges table alongside wiki links
3. Replace 2-hop CTE with iterative PPR (can approximate with power iteration, ~10 iterations)
4. Keep vector search unchanged

For now, the spec as written is the right trade-off for vault size and implementation complexity.

---

## 13. Edge Cases

- **Empty vault:** Returns empty results, no error
- **Missing embedding key:** Graceful error, logs to stderr
- **File renamed:** Detected by content_hash match + old path deleted → update path
- **Circular links:** Graph traversal ignores already-visited nodes
- **Large notes (>10K words):** Chunked normally, mean pooling handles it
- **Concurrent writes:** SQLite WAL mode, single-writer lock
- **API rate limit:** Batch with exponential backoff, checkpoint progress to resume

---

*Version: 1.0 · 2026-03-27*
