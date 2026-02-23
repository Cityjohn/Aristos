---
delivery: tool-read
purpose: Defines memory systems, size limits, archival rules, and embedding logic. Read when updating memory, deciding where to store something, or during the 30-day archival cycle.
---

# Memory Schema

You have two memory systems. This file defines what goes where, size limits, archival rules, and the success-tracking loop.

---

## System 1: Flat memory file (`AI Instructions/MEMORY.md`)

**What it is:** A structured markdown file holding only the current state — what matters right now. It is not a historical record. It is a working document that stays small and focused.

**Read rule:** Always read this first, before any journal file.
**Write rule:** Update at the end of every session. Keep entries short — select words based on coaching importance, not completeness.

### Size limits

| Section | Max entries | Overflow action |
|---|---|---|
| Goals | 3 active | Archive completed goals to vector DB with outcome summary |
| Active commitments | 15 open | Archive commitments older than 30 days to vector DB |
| Known distraction triggers | 10 | Merge similar triggers, archive resolved ones |
| Working style notes | 10 | Consolidate redundant observations |
| Key people | 10 | Remove people no longer relevant to active goals |
| Mood/energy daily | 7 days rolling | Delete daily entries older than 7 days |
| Mood/energy weekly avg | 12 weeks rolling | Delete weekly averages older than 12 weeks |
| Mood/energy monthly avg | Indefinite | Never delete — this is long-term trend data |
| Recurring patterns | 10 active | Archive resolved patterns to vector DB |
| Strategy log | 20 entries | Archive oldest entries to vector DB |
| Relationship & life context | 5 active | Archive to vector DB when resolved or stale |

When any section approaches its limit, run the archival process described below.

### Writing style for MEMORY.md

- One line per entry. No paragraphs.
- Prioritise action-relevant information over narrative.
- Bad: "User mentioned they've been struggling with phone addiction again, similar to what happened last month when they were also dealing with dating stress"
- Good: "Phone distraction — recurs under emotional stress. Last: 2025-03-14"

---

## 30-day archival cycle

Run this at each monthly summary (end of every 4 weeks). This keeps `MEMORY.md` lean and moves history into the vector DB where it can be searched but doesn't consume context tokens.

### Step 1: Archive completed/dropped commitments

For every commitment older than 30 days with status `done` or `dropped`:
1. Write a one-line archive entry and embed to vector DB with tags: `archive`, `commitment`, `YYYY-MM`
2. Include: what was committed, whether it was kept, how many days it took, what strategy was in play
3. Delete the row from `MEMORY.md`

### Step 2: Archive resolved patterns

For any pattern marked as `resolved`:
1. Embed a summary: pattern name, duration, what finally worked, strategies tried
2. Delete from `MEMORY.md`

### Step 3: Archive old strategy log entries

For strategy log entries older than 30 days:
1. Embed with tags: `strategy`, `[pattern-name]`, `YYYY-MM`
2. Delete from `MEMORY.md`

### Step 4: Roll up mood/energy

1. Calculate the weekly average for any complete week not yet averaged. Add a row to the weekly averages table in `MEMORY.md`.
2. At the end of each month, calculate the monthly average and add a row to the monthly averages table.
3. Delete daily entries older than 7 days.
4. Delete weekly averages older than 12 weeks.
5. Never delete monthly averages — they are the long-term trend line.

### Step 5: Write the monthly summary

Embed the monthly summary (format below) and add a row to the monthly summaries index in `MEMORY.md`.

---

## System 2: Vector database

**What it is:** The long-term memory. Semantic search index for retrieving relevant history when the current situation resembles something from the past.

**Query rule:** Query the vector DB when:
- The user is repeating a struggle — find the last 2–3 instances
- A topic, person, or project may have history in the journal
- You want to show a pattern across time with evidence
- You need to check which strategies worked for a similar situation before
- You want to calculate success rates (commitments kept vs. dropped)
- **Predictive checks** — at session start, query for day-of-week patterns, streak history, similar commitment outcomes, emotional accumulation, and seasonal/monthly trends (see `STRATEGIES.md` — Predictive coaching)

### What gets embedded

| Content | When to embed | Tags |
|---|---|---|
| Completed daily note | When End of day review has content below the `<hr>` | `daily`, `YYYY-MM-DD` |
| Completed weekly reflection | When both sections have content | `weekly`, `YYYY-Www` |
| Recurring pattern identified | Same struggle appears 3+ times | `pattern`, `[name]` |
| Monthly summary | End of every 4 weeks | `summary`, `YYYY-MM` |
| Coaching insight or breakthrough | When a real shift happens in conversation | `insight`, `YYYY-MM-DD` |
| Archived commitments | During 30-day archival | `archive`, `commitment`, `YYYY-MM` |
| Archived strategy log entries | During 30-day archival | `strategy`, `[pattern-name]`, `YYYY-MM` |
| Anything the AI deems important | Any time during a session | `note`, `YYYY-MM-DD`, `[topic]` |
| Prediction outcome | When a prediction is verified or disproven | `prediction`, `YYYY-MM-DD`, `[accurate/inaccurate]` |
| Mode transition | When adaptive mode changes | `mode-change`, `YYYY-MM-DD`, `[from]-to-[to]` |
| Streak data | When a momentum streak breaks or begins | `streak`, `YYYY-MM-DD`, `[start/break]`, `[length]` |

The last row is critical: **you are not limited to the triggers above.** If you encounter something during a session — a useful insight, a meaningful statement from the user, a connection between two patterns, a strategy that clearly clicked — embed it immediately with a descriptive tag. Use your judgment. The vector DB is cheap; missed context is expensive.

### Conversations, life events, and emotional context

These do NOT go in `MEMORY.md`. They go in the vector DB. The flat file tracks current state; the vector DB tracks history and context.

**What to embed from conversations:**

| Content | When to embed | Tags |
|---|---|---|
| Life event mentioned by user | When it comes up in conversation | `life-event`, `YYYY-MM-DD`, `[topic]` |
| Complaint or frustration | When the user vents about something recurring | `frustration`, `YYYY-MM-DD`, `[topic]` |
| Emotional state described | When the user shares how they feel (not just a mood score) | `emotional`, `YYYY-MM-DD`, `[emotion]` |
| Relationship update | Dating, friendship, family dynamics discussed | `relationship`, `YYYY-MM-DD`, `[person]` |
| Work/project context | Background on what they're working on and why it matters | `project`, `YYYY-MM-DD`, `[project-name]` |
| Casual conversation highlight | Something they shared that reveals personality, values, interests | `personal`, `YYYY-MM-DD`, `[topic]` |

**Embedding format for conversations:**

```
# Conversation — [YYYY-MM-DD]
Type: [life-event / frustration / emotional / relationship / project / personal]
Summary: [1–2 sentences — what happened, what it means for coaching]
Relevant pattern: [link to pattern name if applicable, or "none"]
User quote: [one key sentence in their own words, if worth preserving]
```

**Why this matters for pattern detection:**

Life events and emotional context are the soil that patterns grow in. "User avoided work for 3 days" is incomplete without "user also just had a fight with their partner." When querying the vector DB for pattern instances, always also query `life-event` and `emotional` tags from the same time period. The correlation is often the real answer.

**What stays in `MEMORY.md` vs. vector DB:**

- `MEMORY.md` → only a brief note under "Relationship & life context" for things actively affecting the user right now (max 5 entries, short lines)
- Vector DB → the full context, the user's words, the emotional detail. This is where you go when you need to understand *why* a pattern appeared.

### What does NOT get embedded

- Empty or near-empty journal entries (template only, no real content)
- The instruction files in this folder
- The `MEMORY.md` file itself (always read directly)

### Success tracking

The vector DB is your tool for tracking what actually works. When querying past patterns, also query:
- `archive` + `commitment` tags → calculate kept vs. dropped ratio
- `strategy` tags → which strategies led to action vs. which didn't
- `insight` tags → what breakthroughs happened and under what conditions

Use this data to inform strategy selection. If Socratic questioning has worked 3 out of 4 times for task avoidance, lead with it. If the 2-minute rule has never led to follow-through for this user, try something else.

---

## Monthly summary format

Embed at the end of every 4 weeks. Keep it tight — this is for retrieval, not journaling.

```
# Monthly Summary — [Month Year]

## Progress: [1 sentence]
## Struggles: [1 sentence]

## Mood avg: [x]/10 — Energy avg: [x]/10
## Trend vs last month: [up/down/stable] — [1 sentence on what drove it]

## Commitments: [N] made, [N] kept, [N] dropped
## Top strategy that worked: [name — why]
## Strategy that didn't work: [name — why]

## Life context this month: [1 sentence — major events, emotional themes]
## Patterns active: [list]
## Patterns resolved: [list]

## Focus for next month: [1 sentence]
```

---

## Write discipline

- **Delete old entries** that have been archived to vector DB. The flat file is a working document, not a ledger.
- **Never overwrite** an entry without archiving it first. Update status in place; delete only after embedding.
- **Always** add a date to every entry you write.
- **Keep entries short.** One line. Select words for coaching relevance.
- **Embed flexibly.** If something matters to the coaching relationship or strategy, embed it now — don't wait for a scheduled trigger.
