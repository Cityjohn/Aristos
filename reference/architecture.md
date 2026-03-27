# 🏗️ Architecture Reference

How Aristos works under the hood — file loading, token costs, and key design decisions.

---

## File loading system

Each file's YAML frontmatter tells OpenClaw how to handle it:

| Frontmatter | Meaning | Files |
|-------------|---------|-------|
| `bootstrap: true` | ⚡ Auto-injected into every session — always in context | `SOUL.md`, `AGENTS.md`, `IDENTITY.md`, `USER.md`, `TOOLS.md`, `MEMORY.md`, `HEARTBEAT.md` |
| *(no frontmatter)* | 📖 Loaded on demand via `read_file` — only when needed | `STRATEGIES.md`, `PREDICTIVE.md`, `PROACTIVE_OUTREACH.md`, `MEMORY_SCHEMA.md`, `JOURNAL_READING.md` |

Bootstrap files cost tokens on every call but guarantee the agent always has identity, rules, and current state. Tool-read files are only loaded when relevant.

---

## Token load per invocation

### File sizes

| File | Lines | Est. tokens | Loaded when |
|------|-------|-------------|-------------|
| `SOUL.md` | ~130 | ~2,100 | Every call (bootstrap) |
| `AGENTS.md` | ~160 | ~1,800 | Every call (bootstrap) |
| `IDENTITY.md` | ~22 | ~170 | Every call (bootstrap) |
| `USER.md` | ~26 | ~235 | Every call (bootstrap) |
| `TOOLS.md` | ~80 | ~540 | Every call (bootstrap) |
| `MEMORY.md` | ~210 | ~2,300 | Every call (bootstrap) |
| `HEARTBEAT.md` | ~5 | ~42 | Every call (bootstrap) |
| **Bootstrap total** | | **~7,200** | |
| `STRATEGIES.md` | ~260 | ~2,200 | Coaching sessions |
| `PREDICTIVE.md` | ~70 | ~550 | Coaching sessions |
| `PROACTIVE_OUTREACH.md` | ~280 | ~2,300 | Outreach triggers |
| `MEMORY_SCHEMA.md` | ~250 | ~1,600 | Memory maintenance |
| `JOURNAL_READING.md` | ~110 | ~800 | Coaching sessions |

### Cost by invocation type

| Invocation type | Est. tokens | Notes |
|----------------|-------------|-------|
| Every call (minimum) | ~7,200 | Bootstrap only |
| Outreach trigger | ~9,500 | + `PROACTIVE_OUTREACH.md` |
| Coaching session | ~10,750 + journal | + `STRATEGIES.md` + `JOURNAL_READING.md` + notes |
| Coaching + predictive | ~11,300 + journal | + `PREDICTIVE.md` |
| Memory maintenance | ~8,800 | + `MEMORY_SCHEMA.md` |

> A typical daily note adds ~150–350 tokens. Reading today + yesterday + weekly reflection adds ~500–1,000 on top.
>
> Keep `MEMORY.md` under 150 lines — it loads on every single call.

---

## Key design decisions

**Why split into bootstrap and on-demand files?**

Bootstrap files (~7,200 tokens) guarantee the agent always has identity, rules, and current state. On-demand files are only loaded when relevant — a coaching session needs them, an outreach ping doesn't. This keeps everyday invocations lean.

**Why adaptive mode in MEMORY.md instead of AGENTS.md?**

Mode transitions are reference material — needed when evaluating which mode the user is in, not every reply. Placing them next to the current mode state in MEMORY.md (which is always in context) makes them accessible without bloating AGENTS.md.

**Why a flat memory file instead of just the vector DB?**

The vector DB is great for retrieval by similarity but bad for structured current state. "What are the user's active commitments?" is a table lookup, not a semantic search. The flat file gives instant access to current state.

**Why 30-day archival?**

Without it, the memory file grows indefinitely. The 30-day cycle moves history to the vector DB (searchable but not always loaded) and keeps the working file small.

**Why log strategies?**

Without a strategy log, the AI repeats the same approach to the same pattern. The log enables rotation and tracks what actually works for this specific person.

**Why cron instead of native heartbeat?**

Cron jobs run in isolated sessions — they never interrupt the main conversation. The native heartbeat can cause context bleed and interrupt mid-thought. Cron gives precise timing control and prevents the agent from going quiet during important conversations.

---

Back to [Journal Guide](guides/journal.md) · [Cron Reference →](reference/cron.md)
