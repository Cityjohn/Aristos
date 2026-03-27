# 📓 Journal Guide

2 minutes a day. That's the whole commitment.

---

## How it works

The templates are designed to be the **minimum viable input** — enough structure that an AI agent can reason about your life across three timescales (day, week, year), but short enough that you'll actually do it.

- **Daily note:** ~2 minutes, morning + evening
- **Weekly reflection:** ~10 minutes, once a week
- **Yearly plan:** Once (review quarterly)

That's it. The agent reads them, spots patterns you don't, and uses what it finds to coach you.

---

## 📖 What it actually looks like

*Happiness doesn't just happen to you, it's about what you happen to do.*

The journal is just a few easy prompts. You write what's real - a big win, a hard week, a goal that has nothing to do with work. The agent builds a picture across all of it and coaches accordingly. Full example notes are in the repo - [`Journal/Day to Day/`](../Journal/Day%20to%20Day/), [`Journal/Weekly reflection/`](../Journal/Weekly%20reflection/), [`Journal/Yearly planning/`](../Journal/Yearly%20planning/).

It starts with the year. Every daily note exists inside a yearly plan broken down by quarter - so the agent always knows whether today's priorities are pointing at what actually matters, or just filling time.

---

**The year, mapped out by quarter**

> **Mission:** This year is about building the foundation - stable income from my own work, physical consistency, and the relationships that matter most.
>
> **Milestones:**
> - First paying client - Q1
> - Consistent exercise 3x/week for 8 weeks - Q1
> - Revenue covers monthly costs - Q2
> - One meaningful trip with close friends or family - Q3
> - 3-month emergency fund - Q4
>
> **Q1 theme - Launch and validate:** First client signed, exercise habit locked in, emergency fund started. January: define the offer and start outreach. February: first sales conversations, hit the 8-week streak. March: close the client, document the process, review and adjust.

---

**A day you close something**

> **Mission:** My mission today is to get the contract signed before EOD.
>
> - Final proposal out by 10am - no more tweaking, it's good enough
> - Follow-up call at 2pm, push for a decision
> - Clear the backlog so tomorrow starts clean
>
> **End of day:** Proposal went at 9:40. They signed on the call. Inbox at zero. Three weeks of work landed today - that felt good.
> Mood: 9, Energy: 8

---

**A day you needed to recover without losing the week**

> **Mission:** My mission today is to recharge without falling behind.
>
> - One hour of real work, then stop
> - Get outside
> - Call Dad - been putting it off for two weeks
>
> **End of day:** Did the hour, got outside twice. Called Dad - longer conversation than expected, glad I did it. Not every day is a sprint. Back at full capacity tomorrow.
> Mood: 5, Energy: 4

---

**A day that was both**

> **Mission:** My mission today is to move the project forward and not cancel on Sarah again.
>
> - Three hours on the architecture doc
> - Honest conversation with the team about the deadline slip
> - Coffee with Sarah - she's reached out twice and I keep deprioritising it
>
> **End of day:** Doc is in better shape. Team conversation was harder than expected but the right call - they needed to hear it. Coffee with Sarah was genuinely good. Reminded me there's more to life than shipping.
> Mood: 7, Energy: 6.

---

The agent tracks all of it over time - output, energy, what you keep postponing, who you care about, what kind of week you're in. That's what lets it coach you as a full person, not just a task list. Browse the example entries in [`Journal/Day to Day/2025-03-15.md`](../Journal/Day%20to%20Day/2025-03-15.md), [`Journal/Weekly reflection/2025-W11.md`](../Journal/Weekly%20reflection/2025-W11.md), and [`Journal/Yearly planning/2025.md`](../Journal/Yearly%20planning/2025.md) to see the format in full.

---

## 📄 Daily Focus Template (~2 minutes)

Three sections. Morning and evening.

### Morning (~1 min)

| Section | What you write | What the agent gets |
|---|---|---|
| **Mission and priorities** | One sentence: "My mission today is to..." + 2-4 bullet priorities | What you're trying to do. Checks alignment with weekly/yearly goals. |
| **Time and metrics** | Hours available, exact sequence of steps, what "done" looks like | Capacity and exit criteria. Assesses if the plan is realistic. |

### Evening (~1 min)

| Section | What you write | What the agent gets |
|---|---|---|
| **End of day review** | Gratitude, distractions, completions vs planned, mood/energy 1-10 | Execution gap, mood trends, recurring interference patterns. |

> The end-of-day review is the most important section. Even one sentence per prompt is enough. The mood/energy score alone - tracked over weeks - gives the agent a reliable signal for when to push and when to back off.

---

## 📄 Weekly Reflection Template (~10 minutes, once a week)

Two sections.

| Section | What you write | What the agent gets |
|---|---|---|
| **End of week review** | Wins, distractions, emotional moments, energy patterns - end with 3-5 bullet summary | Weekly patterns, hardest days, recurring themes. Updates strategy rotation. |
| **Plans and adjustments** | Specific changes for next week - habits, time blocks, systems - end with 3-5 bullet summary | What you're trying differently. Agent tracks whether adjustments land. |

---

## 📄 Yearly Template (once, review quarterly)

Five sections covering your year mission, concrete milestones, reverse goal mapping, and month-by-month breakdown across all four quarters.

The yearly note is the **anchor**. The agent reads it to keep day-to-day coaching connected to what you said actually mattered when you were thinking clearly about your life. It prevents the agent from helping you optimize tasks that shouldn't exist.

---

## Why this is enough

Every field is **parseable as a coaching signal**, not just freeform journaling:

| Field | Signal type |
|---|---|
| Mission + priorities | Intention — what you thought mattered |
| Time and metrics | Capacity — how much you had to work with |
| Completions vs plan | Execution gap — reality vs expectation |
| Distractions | Interference — what keeps recurring |
| Mood/energy score | Baseline trend — rhythms, dips, risky weeks |
| Weekly summary bullets | Signal compression — agent reads these without parsing full entry |
| Yearly milestones | Long-range anchor — prevents drift toward busywork |

Two minutes of structured writing per day gives the agent everything it needs to coach meaningfully - not because it's a lot of data, but because it's the *right* data.

---

Back to [Setup](setup.md) · [Architecture Reference →](../reference/architecture.md)
