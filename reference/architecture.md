# 🏗️ Architecture Reference

How Aristos works under the hood — file loading, knowledge graph, token costs, and key design decisions.

---

## 🔄 How file loading works

| Type | Meaning | Files |
|---|---|---|
| `bootstrap: true` | Auto-injected every call, always in context | SOUL, AGENTS, IDENTITY, USER, TOOLS, MEMORY, HEARTBEAT |
| *(no frontmatter)* | Loaded on demand via `read_file` | PROACTIVE_OUTREACH, MEMORY_SCHEMA, CRON |

Bootstrap files cost tokens on every call but guarantee the agent always has identity, rules, and current state. On-demand files are only loaded when relevant.

**Obsidian files** (Aris Coaching, journal entries) are loaded via vector DB search when context matters, not on every call.

---

## 🧠 The Knowledge Graph

Aristos uses SQLite + sqlite-vec for semantic search across all vault content, combined with wiki link graph traversal for associative reasoning.

### How it works

Every `.md` file in the vault gets:
1. **Embedded** — content converted to a 3072-dim vector (OpenRouter text-embedding-3-large)
2. **Parsed for links** — `[[wiki links]]` extracted and stored as graph edges
3. **Indexed** — vector + edges stored in `~/.openclaw/vault-memory.db`

When the agent needs context, a single hybrid query runs:
- **70% semantic similarity** — find notes by meaning, not keywords
- **30% graph distance** — follow wiki links (2 hops max, 50% decay per hop)

### Why three directories?

```
Your journal          Aris Coaching          Our Knowledge
(permanent record)    (what Aris learns)     (shared knowledge)
      │                     │                       │
      └──── wiki links ─────┘──── wiki links ───────┘
                         │
                    SQLite index
                    (semantic + graph)
```

Your journal stays untouched. Aris writes coaching insights that link TO your entries. Our Knowledge contains shared discoveries. The graph connects everything without polluting any single directory.

### Performance

| Operation | Time | Cost |
|---|---|---|
| Vector search (10k notes) | ~5ms | Free (local) |
| Graph traversal (2 hops) | ~1ms | Free (local) |
| Full hybrid query | ~8ms | Free (local) |
| Embedding (per note) | ~200ms | ~$0.0001 |

### When it activates

The agent queries the vector DB when context matters: coaching sessions, pattern discussions, "remember when" questions. Not on every call - just when history would help.

---

## 💰 Token load per invocation

### Bootstrap files (~7,200 tokens every call)

| File | Est. tokens |
|---|---|
| `SOUL.md` | ~2,100 |
| `AGENTS.md` | ~1,800 |
| `IDENTITY.md` | ~170 |
| `USER.md` | ~235 |
| `TOOLS.md` | ~540 |
| `MEMORY.md` | ~2,300 |
| `HEARTBEAT.md` | ~42 |

### Cost by invocation type

| Type | Est. tokens | Notes |
|---|---|---|
| Every call (minimum) | ~7,200 | Bootstrap only |
| Coaching (with vector DB) | ~8,700 + journal | 5 relevant snippets (~1,500 tokens) instead of 20 mixed (~4,000) |
| Coaching (without vector DB) | ~15,000-20,000 | Broad file reads, manual context gathering |
| Outreach trigger | ~9,500 | Bootstrap + PROACTIVE_OUTREACH |
| Memory maintenance | ~8,800 | Bootstrap + MEMORY_SCHEMA |

> **Vector DB impact:** Coaching calls drop ~40-50% in token usage. The DB retrieves only relevant context instead of loading broad file dumps. Historical patterns surface automatically without manual searching.
>
> Keep `MEMORY.md` under 150 lines — it loads on every single call.

---

## 🏗️ Key design decisions

**Why three directories instead of one?**

Separation of concerns. Your journal is personal - the agent reads it but never edits it. Aris Coaching is where the agent builds its understanding of your patterns. Our Knowledge is shared ground for discoveries and concepts. All three are indexed in SQLite, but ownership is clear.

**Why vector DB instead of just file reads?**

File reads are broad - you load entire files hoping relevant context is in there. Vector search retrieves only relevant snippets by meaning. Token usage drops 40-50% for coaching calls, and quality improves because noise is filtered out.

**Why wiki links as graph edges?**

Your wiki links ARE your knowledge graph. They represent your editorial judgment about what's connected. The graph traversal surfaces connected knowledge that keyword search misses.

**Why hybrid scoring (70% semantic + 30% graph)?**

Pure semantic search finds notes by meaning but misses editorial connections. Pure graph search follows your links but misses implicit patterns. Hybrid gives you both: what's semantically relevant AND what you've explicitly connected.

**Why split bootstrap and on-demand files?**

Bootstrap files (~7,200 tokens) guarantee identity, rules, and state on every call. On-demand files are only loaded when relevant. Everyday invocations stay lean.

**Why adaptive mode in MEMORY.md instead of AGENTS.md?**

Mode transitions are reference material — needed when evaluating which mode the user is in, not every reply. Placing them next to the current mode state in MEMORY.md (which is always in context) makes them accessible without bloating AGENTS.md.

**Why a flat memory file instead of just the vector DB?**

The vector DB is great for retrieval by similarity but bad for structured current state. "What are the user's active commitments?" is a table lookup, not a semantic search. The flat file gives instant access to current state.

**Why session-state.json as shared scratchpad?**

It's the one file read by both cron jobs and the main session. Activity timestamps, coaching state, conversation topics, and strategy outcomes live here as the bridge between scheduled events and real-time conversation.

**Why 30-day archival?**

Without it, the memory file grows indefinitely. The 30-day cycle moves history to the vector DB and keeps the working file small.

**Why log strategies?**

Without a strategy log, the AI repeats the same approach to the same pattern. The log enables rotation and tracks what actually works for this specific person.

**Why cron instead of native heartbeat?**

Cron jobs run in isolated sessions — they never interrupt the main conversation. The native heartbeat can cause context bleed and interrupt mid-thought. Cron gives precise timing control and prevents the agent from going quiet during important conversations.

---

Back to [Journal Guide](../guides/journal.md) · [Cron Reference →](cron.md)
