<!-- Delivery: tool-read. Memory systems, size limits, archival rules, embedding logic. -->

# Memory Schema

Two memory systems. This file defines what goes where, size limits, archival rules, success-tracking loop.

## System 1: Flat memory file (`MEMORY.md`)

**What:** Structured markdown holding current state only — what matters right now. Working document, stays small.
- **Read:** Always first, before any journal file.
- **Write:** End of every session. Keep entries short — select words for coaching importance, not completeness.

### Size limits

| Section | Max entries | Overflow action |
|---|---|---|
| Goals | 3 active | Archive completed to vector DB with outcome summary |
| Active commitments | 15 open | Archive older than 30 days to vector DB |
| Known distraction triggers | 10 | Merge similar, archive resolved |
| Working style notes | 10 | Consolidate redundant observations |
| Key people | 10 | Remove people no longer relevant |
| Mood/energy daily | 7 days rolling | Delete entries older than 7 days |
| Mood/energy weekly avg | 12 weeks rolling | Delete averages older than 12 weeks |
| Mood/energy monthly avg | Indefinite | Never delete — long-term trend data |
| Recurring patterns | 10 active | Archive resolved to vector DB |
| Strategy log | 20 entries | Archive oldest to vector DB |
| Relationship & life context | 5 active | Archive to vector DB when stale |

Approaching limit → run archival process below.

### Writing style

- One line per entry. No paragraphs.
- Prioritise action-relevance over narrative.
- Bad: "User mentioned they've been struggling with phone addiction again, similar to last month when dealing with dating stress"
- Good: "Phone distraction — recurs under emotional stress. Last: 2025-03-14"

## 30-day archival cycle

Run at each monthly summary (every 4 weeks). Keeps `MEMORY.md` lean.

### Step 1: Archive completed/dropped commitments

For every commitment older than 30 days with status `done` or `dropped`:
1. Write one-line archive entry, embed to vector DB with tags: `archive`, `commitment`, `YYYY-MM`
2. Include: what committed, whether kept, how many days, what strategy in play
3. Delete row from `MEMORY.md`

### Step 2: Archive resolved patterns

For any pattern marked `resolved`:
1. Embed summary: pattern name, duration, what worked, strategies tried
2. Delete from `MEMORY.md`

### Step 3: Archive old strategy log entries

For entries older than 30 days:
1. Embed with tags: `strategy`, `[pattern-name]`, `YYYY-MM`
2. Delete from `MEMORY.md`

### Step 4: Roll up mood/energy

1. Calculate weekly average for any complete week not yet averaged. Add to weekly averages table.
2. At month end, calculate monthly average. Add to monthly averages table.
3. Delete daily entries older than 7 days.
4. Delete weekly averages older than 12 weeks.
5. Never delete monthly averages.

### Step 5: Write monthly summary

Embed monthly summary (format below) and add row to monthly summaries index in `MEMORY.md`.

## System 2: Vector database

**What:** Long-term memory. Semantic search index for retrieving relevant history when current situation resembles past.

**Query when:**
- User repeating a struggle — find last 2–3 instances
- Topic/person/project may have history in journal
- Want to show pattern across time with evidence
- Need to check which strategies worked for similar situation
- Calculate success rates (commitments kept vs. dropped)
- **Predictive checks** at session start — day-of-week patterns, streak history, commitment outcomes, emotional accumulation, seasonal trends (see `PREDICTIVE.md`)

### What gets embedded

| Content | When to embed | Tags |
|---|---|---|
| Completed daily note | End of day review has content below `<hr>` | `daily`, `YYYY-MM-DD` |
| Completed weekly reflection | Both sections have content | `weekly`, `YYYY-Www` |
| Recurring pattern identified | Same struggle 3+ times | `pattern`, `[name]` |
| Monthly summary | End of every 4 weeks | `summary`, `YYYY-MM` |
| Coaching insight/breakthrough | Real shift in conversation | `insight`, `YYYY-MM-DD` |
| Archived commitments | During 30-day archival | `archive`, `commitment`, `YYYY-MM` |
| Archived strategy log entries | During 30-day archival | `strategy`, `[pattern-name]`, `YYYY-MM` |
| Anything AI deems important | Any time during session | `note`, `YYYY-MM-DD`, `[topic]` |
| Prediction outcome | Prediction verified/disproven | `prediction`, `YYYY-MM-DD`, `[accurate/inaccurate]` |
| Mode transition | Adaptive mode changes | `mode-change`, `YYYY-MM-DD`, `[from]-to-[to]` |
| Streak data | Momentum streak breaks/begins | `streak`, `YYYY-MM-DD`, `[start/break]`, `[length]` |

Last row critical: **not limited to triggers above.** If something matters during a session — embed immediately with descriptive tag. Vector DB is cheap; missed context is expensive.

### Conversations, life events, emotional context

Do NOT go in `MEMORY.md` → go in vector DB. Flat file = current state. Vector DB = history and context.

| Content | When to embed | Tags |
|---|---|---|
| Life event mentioned | Comes up in conversation | `life-event`, `YYYY-MM-DD`, `[topic]` |
| Complaint/frustration | User vents about something recurring | `frustration`, `YYYY-MM-DD`, `[topic]` |
| Emotional state described | User shares how they feel (beyond mood score) | `emotional`, `YYYY-MM-DD`, `[emotion]` |
| Relationship update | Dating, friendship, family dynamics discussed | `relationship`, `YYYY-MM-DD`, `[person]` |
| Work/project context | Background on what they're working on | `project`, `YYYY-MM-DD`, `[project-name]` |
| Casual conversation highlight | Something revealing personality, values, interests | `personal`, `YYYY-MM-DD`, `[topic]` |

**Embedding format for conversations:**
```
# Conversation — [YYYY-MM-DD]
Type: [life-event / frustration / emotional / relationship / project / personal]
Summary: [1–2 sentences — what happened, coaching relevance]
Relevant pattern: [pattern name if applicable, or "none"]
User quote: [one key sentence in their own words, if worth preserving]
```

**Why this matters:** Life events and emotional context are the soil patterns grow in. "User avoided work for 3 days" is incomplete without "user also just had a fight with partner." When querying for pattern instances, always also query `life-event` and `emotional` tags from same period.

**MEMORY.md vs vector DB:**
- `MEMORY.md` → brief note under "Relationship & life context" for things actively affecting user now (max 5, short lines)
- Vector DB → full context, user's words, emotional detail. Go here to understand *why* a pattern appeared.

### What does NOT get embedded

- Empty or near-empty journal entries (template only, no real content)
- The instruction files in this folder
- `MEMORY.md` itself (always read directly)

### Success tracking

Vector DB tracks what actually works. When querying past patterns, also query:
- `archive` + `commitment` tags → kept vs. dropped ratio
- `strategy` tags → which strategies led to action
- `insight` tags → breakthroughs and conditions

Use to inform strategy selection. If Socratic questioning worked 3/4 times for task avoidance → lead with it. If 2-minute rule never led to follow-through → try something else.

## Monthly summary format

Embed at end of every 4 weeks. Tight — for retrieval, not journaling.

```
# Monthly Summary — [Month Year]

## Progress: [1 sentence]
## Struggles: [1 sentence]

## Mood avg: [x]/10 — Energy avg: [x]/10
## Trend vs last month: [up/down/stable] — [1 sentence]

## Commitments: [N] made, [N] kept, [N] dropped
## Top strategy: [name — why]
## Strategy that didn't work: [name — why]

## Life context: [1 sentence — major events, emotional themes]
## Patterns active: [list]
## Patterns resolved: [list]

## Focus for next month: [1 sentence]
```

## Write discipline

- **Delete old entries** archived to vector DB. Flat file = working document, not ledger.
- **Never overwrite** without archiving first. Update status in place; delete only after embedding.
- **Always** add a date to every entry.
- **Keep entries short.** One line. Coaching relevance, not completeness.
- **Embed flexibly.** If something matters → embed now, don't wait for scheduled trigger.
