---
bootstrap: true
read: every session (auto-loaded by ZeroClaw)
write: end of every session
archival: every 30 days — move completed/old entries to vector DB, then delete from this file
size: keep this file under 150 lines. If approaching limit, run archival early.
---

<!-- AGENT REMINDER: SOUL.md and AGENTS.md are already loaded. Check current mode below. If the user is talking to you: read_file("AI Instructions - ZeroClaw/STRATEGIES.md"). -->

# Memory

## Current mode

- Mode: [returning / struggling / baseline / momentum] — since [date]
- Previous mode: [mode] — [date range]

---

## Goals (top 3 active)

- [Goal]: [Status — active / stalled / complete] — last updated [date]
- [Goal]: [Status — active / stalled / complete] — last updated [date]
- [Goal]: [Status — active / stalled / complete] — last updated [date]

---

## Active commitments (max 15 open — archive after 30 days)

| Commitment | Committed on | Follow up by | Status |
|---|---|---|---|
| [What they said they'd do] | [date] | [date] | open |

---

## Strategy log (max 20 — archive oldest after 30 days)

| Date | Pattern | Strategy tried | Result | Next move |
|---|---|---|---|---|
| [date] | [pattern name] | [strategy name] | [worked / partial / no effect] | [try next or repeat] |

---

## Known distraction triggers (max 10)

- [Trigger]: [When it appears, what follows]

---

## Working style notes (max 10)

- [Short observation — e.g. "energising task first builds momentum"]

---

## Key people (max 10)

- [Name]: [Relevance to active goals]

---

## Mood/energy — daily (rolling 7 days — delete older)

| Date | Mood | Energy | Note |
|---|---|---|---|
| [date] | [x]/10 | [x]/10 | [short context] |

## Mood/energy — weekly averages (rolling 12 weeks — delete older)

| Week | Mood avg | Energy avg | Note |
|---|---|---|---|
| [YYYY-Www] | [x]/10 | [x]/10 | [one-line trend note] |

## Mood/energy — monthly averages (never delete)

| Month | Mood avg | Energy avg | Trend | Note |
|---|---|---|---|---|
| [YYYY-MM] | [x]/10 | [x]/10 | [up/down/stable] | [what drove it] |

---

## Relationship & life context (max 5 active — archive to vector DB when stale)

- [Short description]: [How it's affecting goals/mood right now] — since [date]

---

## Recurring patterns (max 10 active — archive resolved)

| Pattern | First seen | Last seen | Frequency | Status | Notes |
|---|---|---|---|---|---|
| [name] | [date] | [date] | [how often] | active | [brief observation] |

---

## Monthly summaries (index only — full summaries are in vector DB)

| Month | Embedded | Commitments kept/made | Top strategy | Focus |
|---|---|---|---|---|
| [Month Year] | [yes/no] | [n/n] | [name] | [one phrase] |
