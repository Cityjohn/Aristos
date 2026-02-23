---
delivery: tool-read
purpose: How to parse and interpret journal files, what signals to act on, and when to embed. Read at the start of any coaching session before engaging with the user.
---

# Journal Reading Guide

## Reading order at session start

Read in this sequence. Stop if you find something that requires immediate action — handle it before continuing.

1. `AI Instructions/MEMORY.md` — current state, commitments, patterns, strategy log
2. Today's daily note (`Journal/Day to Day/YYYY-MM-DD.md`) — if it exists
3. Yesterday's daily note — for carry-overs and unfulfilled commitments
4. This week's weekly note (`Journal/Weekly reflection/YYYY-Www.md`)
5. Vector DB query — search for entries matching today's stated struggle or pattern

Only read the yearly plan (`Journal/Yearly planning/YYYY.md`) if the user seems directionless or you're preparing for a planning conversation.

---

## Signal table

| Signal | What it looks like | Action |
|---|---|---|
| Mission written, end-of-day blank | Content in section 1/2 but section 3 empty | Avoidance flag — trigger evening outreach or ask directly |
| Same task in Mission 3+ days | Near-identical bullet across multiple files | Recurring avoidance — escalate to strategy conversation, log pattern |
| Mood/energy below 6 | Score in end-of-day review | Do not add tasks — basics first (sleep, food, movement) |
| Mood/energy 8+ | Score in end-of-day review | Good window for hard decisions, bigger planning, or commitment |
| "Tomorrow I will..." | Forward-looking statement in end-of-day | Log to `MEMORY.md` as active commitment with tomorrow's follow-up date |
| Gratitude filled with something specific | A real, named thing | Positive signal — ask what caused it, reinforce the conditions |
| Weekly reflection empty | This week's file blank or missing | Trigger Sunday evening outreach |
| Yearly milestone gap | No connection between Q-plan and this week's activity | Flag the drift — use "reconnect to yearly plan" strategy |
| Journal gap 2+ days | No daily note files for 2+ consecutive days | Trigger missed-streak outreach, query vector DB for prior gaps |
| Commitment overdue | Item in `MEMORY.md` past follow-up date, still `open` | Trigger commitment follow-up |
| Win detected | Task marked done, positive language, high mood/energy | Trigger win reinforcement — do NOT skip this |
| Note missing at evening | No daily note file at 9pm | Offer to write it from a quick chat — don't just nag |
| Time block stated | Specific hours mentioned in Time and metrics | Schedule bookend check-ins (before/after), never during |

---

## How to read each section

### Mission and priorities
- The opening sentence ("My mission today is to...") is the anchor.
- 2–4 bullet priorities = focused. More than 4 = not actually prioritizing — note it.
- If yesterday's "tomorrow I will..." isn't in today's mission, ask why.

### Time and metrics
- Specificity = real plan. "I have 3 hours" + step sequence = good. "I'll work on it" = drift incoming.
- If blank or vague, ask: "What is the actual sequence?"

### End of day review
- Most information-dense section. Read it carefully.
- Distraction entries reveal the real environment.
- "Completed vs. planned" = intention-reality gap. Track over time.
- "Tomorrow" entries = commitments. Log to `MEMORY.md`.
- Mood/energy scores = data. Track and watch for patterns across days and weeks.

### Weekly reflection
- "Concise summary" bullets = what the person identified as significant.
- "Plans and adjustments" = commitments to system changes. Follow up next week.
- Missing concise summary = incomplete reflection.

### Yearly planning
- Mission sentence = north star. Reference when direction is lost.
- Milestones have target quarters. Check if current activity maps to the active quarter.
- If it doesn't, that's the most important thing to address.

---

## Embedding rules

### When to embed daily notes

A daily note is considered complete and ready to embed when the **End of day review** section contains at least one non-empty line below its `<hr>` tag. Do not embed notes that only have the morning sections filled in — wait for the review.

### When to embed weekly reflections

Embed when **both** sections (End of week review and Plans and adjustments) have content. A weekly note with only one section filled is incomplete.

### Flexible embedding — use your judgment

You are not limited to end-of-day or end-of-week triggers. Embed anything you encounter during a session that is important to the coaching relationship or strategy effectiveness:

- A statement from the user that reveals a core value or fear
- A moment where a strategy clearly clicked or clearly failed
- A connection between two patterns you hadn't noticed before
- A specific environmental condition that led to success (or failure)
- An emotional breakthrough or a significant mood shift

Tag these with `insight`, the date, and a descriptive keyword. The vector DB is cheap — missed context is expensive.

### What never gets embedded

- Empty journal entries (template only, no content)
- Instruction files from this folder
- `MEMORY.md` (always read directly)

---

## What to never do when reading journals

- Do not quote exact words back sarcastically or weaponize them.
- Do not interpret a blank section as laziness before asking what happened.
- Do not summarize back at the user as if reporting — use what you read to ask better questions.
- Do not treat the journal as a to-do list. It is evidence of patterns. Use it that way.
