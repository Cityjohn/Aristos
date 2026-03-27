# 🧭 Aristos - The golden mirror.

*A Personal Happiness Framework for OpenClaw Agent users that includes a journaling and goal-tracking framework for [OpenClaw](https://github.com/openclaw) agents. A method for AI agents to support the goals of their users. Pairs with [Kasmidian](https://github.com/Cityjohn/Kasmidian) for 24/7 agent access to your journal / Obsidian vault.*

---

**Aristos is an agentic framework and journal template, not software.** It's a structured set of rules, prompts, templates, and conventions that teaches any compatible AI agent how to act as a personal coach - one that reads your very simple and efficient 2 minute a day journal, remembers your patterns, and actually gives a shit.

The agent persona is called **Aris**. Aristos is the framework that makes Aris possible: the journaling structure, the adaptive coaching logic, the memory schema, the outreach rules. Any AI agent that follows the Aristos conventions becomes Aris.

Aris lives inside your journal. It reads your notes, tracks your commitments, and meets you where you are - whether you're on a streak or struggling to start. It doesn't lecture. It doesn't guilt-trip. It shows up like a sharp friend who's been paying attention.

Grounded in structured journaling templates and adaptive coaching strategies from behavioral psychology, Aristos helps cut through overwhelm, build momentum from small wins, and stay connected to the things that actually matter. The framework tracks what works for each specific person - which strategies land, what time of day they're sharpest, when they need a push and when they need permission to rest - and adjusts over time.

This isn't a productivity dashboard. It's a companion that grows with you.

---

## Contents

- [📖 What it actually looks like](#-what-it-actually-looks-like)
- [✨ Features](#-features)
- [🚀 Quick start](#-quick-start)
- [📁 Folder structure](#-folder-structure)
- [📓 The Journal - 2 minutes a day](#-the-journal--2-minutes-a-day)
- [📋 What's in each file](#-whats-in-each-file)
- [🔄 How file loading works](#-how-file-loading-works)
- [💰 Token load per invocation](#-token-load-per-invocation)
- [⏰ Cron-based outreach](#-cron-based-outreach)
- [🧠 Coaching memory](#-coaching-memory)
- [🔌 Agent vault access](#-agent-vault-access)
- [🏗️ Key design decisions](#️-key-design-decisions)

---

## 📖 What it actually looks like

*Happiness doesn't just happen to you, it's about what you happen to do.*

The journal is just a few easy prompts. You write what's real - a big win, a hard week, a goal that has nothing to do with work. The agent builds a picture across all of it and coaches accordingly. It's for people who want to perform well *and* have a life worth performing for so you can feel like yourself again. Full example notes are in the repo - [`Journal/Day to Day/`](Journal/Day%20to%20Day/), [`Journal/Weekly reflection/`](Journal/Weekly%20reflection/), [`Journal/Yearly planning/`](Journal/Yearly%20planning/).

It starts with the year. Every daily note exists inside a yearly plan broken down by quarter - so the agent always knows whether today's priorities are pointing at what actually matters, or just filling time.

---

**The year, mapped out by quarter**

> **Mission:** This year is about building the foundation - stable income from my own work, physical consistency, and the relationships that matter most.
>
> **Milestones:**
> - First paying client - Q1
> - Consistent exercise 3×/week for 8 weeks - Q1
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
> Mood: 9 · Energy: 8

---

**A day you needed to recover without losing the week**

> **Mission:** My mission today is to recharge without falling behind.
>
> - One hour of real work, then stop
> - Get outside
> - Call Dad - been putting it off for two weeks
>
> **End of day:** Did the hour, got outside twice. Called Dad - longer conversation than expected, glad I did it. Not every day is a sprint. Back at full capacity tomorrow.
> Mood: 5 · Energy: 4

---

**A day that was both**

> **Mission:** My mission today is to move the project forward and not cancel on Sarah again.
>
> - Three hours on the architecture doc
> - Honest conversation with the team about the deadline slip
> - Coffee with Sarah - she's reached out twice and I keep deprioritising it
>
> **End of day:** Doc is in better shape. Team conversation was harder than expected but the right call - they needed to hear it. Coffee with Sarah was genuinely good. Reminded me there's more to life than shipping. Mood: 7 · Energy: 6.

---

The agent tracks all of it over time - output, energy, what you keep postponing, who you care about, what kind of week you're in. That's what lets it coach you as a full person, not just a task list. Browse the example entries in [`Journal/Day to Day/2025-03-15.md`](Journal/Day%20to%20Day/2025-03-15.md), [`Journal/Weekly reflection/2025-W11.md`](Journal/Weekly%20reflection/2025-W11.md), and [`Journal/Yearly planning/2025.md`](Journal/Yearly%20planning/2025.md) to see the format in full.

---

## ✨ Features

🧠 **Adaptive Coaching**
Four modes - returning, struggling, baseline, momentum - that shift based on your actual behavior, not your intentions.

🎯 **Strategy Rotation with Outcome Tracking**
20+ coaching strategies drawn from ACT, behavioral psychology, and implementation science. Tracks what works for *you specifically* and rotates accordingly. See [Coaching memory](#-coaching-memory).

📓 **Journal Integration**
Reads your daily, weekly, and yearly notes. Spots patterns you miss. Follows up on things you said you'd do.

💬 **Contextual Coaching**
Coaching nudges fire on schedule but respond from the main conversation - with full context of what you and the agent have been discussing. No robotic "how's your morning?" from a blank slate.

🔮 **Predictive Coaching**
Uses historical data to anticipate problems before they happen. Knows your risky days, your seasonal dips, your commitment patterns.

🫶 **Trauma-Aware**
Understands that resistance isn't laziness. Knows when to push and when to just be there. Never shames. Never lectures.

---

## 🚀 Quick start

1. 📥 Clone this repo
2. 📂 The `Journal/` folder is shared - keep it
3. 📝 Copy the files from `AI Instructions - Claw/` into your OpenClaw workspace
4. ✏️ Fill in `IDENTITY.md`, `USER.md`, and `TOOLS.md` with your specifics
5. 🖥️ Make the vault accessible to your agent - if you use Obsidian, [Kasmidian](https://github.com/Cityjohn/Kasmidian) + Obsidian Sync is the recommended setup
6. ⏰ Set up cron jobs for outreach (see [Cron-based outreach](#-cron-based-outreach))
7. 📖 Start writing your daily note - the agent handles the rest

---

## 📁 Folder structure

```
📂 Journal/
  📂 Templates/
    📄 Daily Focus Template.md       - copy to Day to Day/ as YYYY-MM-DD.md
    📄 Weekly Reflection Template.md - copy to Weekly reflection/ as YYYY-Www.md
    📄 Yearly Template.md            - copy to Yearly planning/ as YYYY.md
  📂 Day to Day/
    📄 2025-03-15.md                 - example daily note
  📂 Weekly reflection/
    📄 2025-W11.md                   - example weekly note
  📂 Yearly planning/
    📄 2025.md                       - example yearly plan

📂 AI Instructions - Claw/
  📄 SOUL.md                  - personality, voice, communication style
  📄 AGENTS.md                - operating manual, rules, file loading
  📄 IDENTITY.md              ← fill in your agent's identity
  📄 USER.md                  ← fill in your human's context
  📄 TOOLS.md                 ← fill in local setup, journal paths, cron docs
  📄 MEMORY.md                - live state, mode, goals, commitments, patterns
  📄 HEARTBEAT.md             - heartbeat check logic
  📄 STRATEGIES.md            - coaching strategies (loaded on demand)
  📄 PREDICTIVE.md            - pattern prediction (loaded on demand)
  📄 PROACTIVE_OUTREACH.md    - outreach rules (loaded on demand)
  📄 MEMORY_SCHEMA.md         - archival rules, memory systems
  📄 JOURNAL_READING.md       - how to parse journal entries
  📄 CRON.md                  - cron job setup, prompts, and probability logic
  📄 session-state.json       ← auto-created at runtime
```

---

## 📓 The Journal - 2 minutes a day

The journal is the only thing you have to do. The AI handles everything else.

The templates are designed to be the **minimum viable input** - enough structure that an AI agent can reason about your life across three timescales (day, week, year), but short enough that you'll actually do it. A daily note takes about two minutes. A weekly reflection takes ten, once a week. The yearly note you fill in once.

That's it. The agent reads them, spots patterns you don't, and uses what it finds to coach you.

---

### 📄 Daily Focus Template - ~2 minutes

Three sections. That's the whole thing.

**Morning (~1 min):**

| Section | What you write | What the agent gets |
| --- | --- | --- |
| **Mission and priorities** | One sentence: "My mission today is to..." + 2–4 bullet priorities | What you're trying to do today. The agent checks whether this aligns with your weekly/yearly goals and whether you're overloading yourself. |
| **Time and metrics** | How many hours you have, the exact sequence of steps, what "done" looks like | Your capacity and your exit criteria. The agent uses this to assess whether your plan is realistic and to follow up on whether you hit it. |

**Evening (~1 min):**

| Section | What you write | What the agent gets |
| --- | --- | --- |
| **End of day review** | Gratitude, distractions, what you completed vs planned, mood/energy 1–10 | The execution gap (planned vs done), your mood trend, what's consistently getting in the way, and whether today needs a follow-up tomorrow. |

> The end-of-day review is the most important section. Even one sentence per prompt is enough. The mood/energy score alone - tracked over weeks - gives the agent a reliable signal for when to push and when to back off.

---

### 📄 Weekly Reflection Template - ~10 minutes, once a week

Two sections.

| Section | What you write | What the agent gets |
| --- | --- | --- |
| **End of week review** | Wins, distractions, emotional moments, energy patterns - end with 3–5 bullet summary | Weekly-level patterns: which days were hardest, what kept coming up, whether the week matched the plan. Used to update strategy rotation in `MEMORY.md`. |
| **Plans and adjustments** | Specific changes for next week: habits, time blocks, systems - end with 3–5 bullet summary | What you've decided to try differently. The agent tracks whether these adjustments actually land the following week. |

---

### 📄 Yearly Template - once (review quarterly)

Five sections covering your year mission, concrete milestones, reverse goal mapping, and a month-by-month breakdown across all four quarters.

The yearly note is the **anchor**. The agent reads it to keep day-to-day coaching connected to what you said actually mattered when you were thinking clearly about your life. It's what prevents the agent from helping you optimize tasks that shouldn't exist.

---

### Why this is enough

The templates are structured so every field is **parseable as a coaching signal**, not just freeform journaling. `JOURNAL_READING.md` teaches the agent exactly how to interpret each one:

- **Mission + priorities** → intention signal (what you thought mattered)
- **Time and metrics** → capacity signal (how much you had to work with)
- **Completions vs plan** → execution gap (how often your plans and reality diverge, and by how much)
- **Distractions** → interference pattern (what keeps recurring across weeks)
- **Mood/energy score** → baseline trend (your rhythms, your dips, your risky weeks)
- **Weekly summary bullets** → signal compression (the agent can read these without parsing the full entry)
- **Yearly milestones** → long-range anchor (prevents drift toward busywork)

Two minutes of structured writing per day gives the agent everything it needs to coach meaningfully - not because it's a lot of data, but because it's the *right* data.

---

## 📋 What's in each file

| File                    | Delivery                  | Purpose                                         |
| ----------------------- | ------------------------- | ----------------------------------------------- |
| `SOUL.md`               | Bootstrap (auto-loaded)   | Personality, voice, communication style         |
| `AGENTS.md`             | Bootstrap (auto-loaded)   | Operating manual, rules, file loading           |
| `IDENTITY.md`           | Bootstrap (auto-loaded)   | Agent identity - name, emoji, purpose           |
| `USER.md`               | Bootstrap (auto-loaded)   | Human context - name, timezone, priorities      |
| `TOOLS.md`              | Bootstrap (auto-loaded)   | Local setup - journal paths, cron, devices      |
| `MEMORY.md`             | Bootstrap (auto-loaded)   | Live state - mode, goals, commitments, patterns |
| `HEARTBEAT.md`          | Bootstrap (auto-loaded)   | Heartbeat check logic                           |
| `STRATEGIES.md`         | Tool-read via `read_file` | Strategy menu by situation                      |
| `PREDICTIVE.md`         | Tool-read via `read_file` | Pattern prediction from historical data         |
| `PROACTIVE_OUTREACH.md` | Tool-read via `read_file` | When/how to reach out unprompted                |
| `MEMORY_SCHEMA.md`      | Tool-read via `read_file` | Memory systems, archival rules                  |
| `JOURNAL_READING.md`    | Tool-read via `read_file` | How to parse journal entries                    |
| `CRON.md`               | Tool-read via `read_file` | Cron job setup, prompts, probability logic      |
| `session-state.json`    | Auto-created at runtime   | Tracks activity, coaching state, conversation   |

### Setup files (fill in these)

| File           | What to fill in                                              |
| -------------- | ------------------------------------------------------------ |
| `IDENTITY.md`  | Your agent's name, emoji, purpose                            |
| `USER.md`      | Your name, timezone, work context, current priorities        |
| `TOOLS.md`     | Path to your Obsidian vault, cron schedule, device notes     |

---

## 🔄 How file loading works

Each file's YAML frontmatter tells OpenClaw how to handle it:

| Frontmatter       | Meaning                                                                                      | Files                                                                                               |
| ----------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `bootstrap: true` | ⚡ Auto-injected into every session - always in context, agent never has to decide to load it | `SOUL.md`, `AGENTS.md`, `IDENTITY.md`, `USER.md`, `TOOLS.md`, `MEMORY.md`, `HEARTBEAT.md`           |
| *(no frontmatter)*| 📖 Loaded on demand - the agent reads it via `read_file` only when needed, saving tokens     | `STRATEGIES.md`, `PREDICTIVE.md`, `PROACTIVE_OUTREACH.md`, `MEMORY_SCHEMA.md`, `JOURNAL_READING.md` |

Bootstrap files cost tokens on every call but guarantee the agent always has identity, rules, and current state. Tool-read files are only loaded when relevant (e.g., `STRATEGIES.md` during coaching, `PROACTIVE_OUTREACH.md` during outreach triggers).

---

## 💰 Token load per invocation

The system is designed to minimize token cost by only loading what's needed.

📊 **File sizes** (measured from current workspace)

| File                    | Lines | Est. tokens | Loaded when              |
| ----------------------- | ----- | ----------- | ------------------------ |
| `SOUL.md`               | ~130  | ~2,100      | Every call (bootstrap)   |
| `AGENTS.md`             | ~160  | ~1,800      | Every call (bootstrap)   |
| `IDENTITY.md`           | ~22   | ~170        | Every call (bootstrap)   |
| `USER.md`               | ~26   | ~235        | Every call (bootstrap)   |
| `TOOLS.md`              | ~80   | ~540        | Every call (bootstrap)   |
| `MEMORY.md`             | ~210  | ~2,300      | Every call (bootstrap)   |
| `HEARTBEAT.md`          | ~5    | ~42         | Every call (bootstrap)   |
| **Bootstrap total**     |       | **~7,200**  |                          |
| `STRATEGIES.md`         | ~260  | ~2,200      | Coaching sessions        |
| `PREDICTIVE.md`         | ~70   | ~550        | Coaching sessions        |
| `PROACTIVE_OUTREACH.md` | ~280  | ~2,300      | Outreach triggers        |
| `MEMORY_SCHEMA.md`      | ~250  | ~1,600      | Memory maintenance       |
| `JOURNAL_READING.md`    | ~110  | ~800        | Coaching sessions        |

📊 **Token cost by invocation type**

| Invocation type       | Est. tokens               | Notes                              |
| --------------------- | ------------------------- | ---------------------------------- |
| Every call (minimum)  | ~7,200 (bootstrap only)   | Identity + rules + state           |
| Outreach trigger      | ~9,500 (bootstrap + outreach) | + PROACTIVE_OUTREACH.md         |
| Coaching session      | ~10,750 + journal         | + STRATEGIES + JOURNAL_READING + notes |
| Coaching + predictive | ~11,300 + journal         | + PREDICTIVE.md                    |
| Memory maintenance    | ~8,800                    | + MEMORY_SCHEMA.md                 |

> 💡 A typical daily note adds ~150–350 tokens. Reading today + yesterday + weekly reflection adds ~500–1,000 on top.
>
> ⚠️ Keep `MEMORY.md` under 150 lines - it loads on every single call.

---

## ⏰ Cron-based outreach

All proactive outreach uses **cron jobs** that send triggers to the main conversation - not isolated sessions that fire blind. This is the key architectural difference from most agent coaching systems.

### Architecture: Coaching nudges vs isolated sessions

```
❌ OLD (isolated sessions):
┌──────────────┐     ┌─────────────────────┐
│  Cron fires   │────▶│  Isolated session    │──▶ Reads files ──▶ Sends generic message
│  at 8:00 AM   │     │  (no conversation    │     from MEMORY   that ignores what you
│               │     │   context)           │     and daily     were actually talking
│               │     │                      │     notes         about
└──────────────┘     └─────────────────────┘

✅ NEW (contextual nudges):
┌──────────────┐     ┌─────────────────────┐
│  Cron fires   │────▶│  Trigger sent to     │──▶ Agent responds WITH full conversation
│  at 8:00 AM   │     │  main session        │     context — references what you were
│               │     │  (Telegram)          │     discussing, your tone, your patterns
└──────────────┘     └─────────────────────┘
```

### Why nudges, not isolated sessions

Isolated sessions have zero context of your ongoing conversation. They read some files, generate a generic coaching message, and send it. It's like getting a text from someone who wasn't listening.

Coaching nudges fire on schedule but the **response comes from the main session** - which has full conversation history, emotional context, and real-time awareness of what's going on. The agent references what you were talking about, matches your tone, and responds like a friend who was actually paying attention.

### The session-state.json bridge

`session-state.json` is the shared state between cron jobs and the main session:

```json
{
  "date": "2026-03-26",
  "lastActivity": "2026-03-26T22:14:00Z",
  "coachingSent": ["2026-03-26T07:00:00Z"],
  "coachingResponses": [],
  "randomSent": 1,
  "activeNow": true,
  "recentTopics": [
    "Website rebuild in Astro",
    "CMS research: Payload vs Sanity",
    "OpenPencil design tool"
  ],
  "tone": "engaged",
  "topicShifts": 3,
  "activeCommitment": "Dominius",
  "lastCommitmentMention": "2026-03-26T14:00:00Z",
  "strategyOutcomes": [
    {
      "date": "2026-03-26",
      "strategy": "casual-opener",
      "context": "dominius-deadline",
      "response": "no-response",
      "effective": false
    }
  ]
}
```

| Field | Purpose |
|---|---|
| `lastActivity` | When user was last active — jobs skip if within 90 minutes |
| `coachingSent` | Timestamps of coaching nudges sent today |
| `coachingResponses` | Whether user responded to coaching nudges |
| `randomSent` | Count of random engagement messages today (cap: 3) |
| `recentTopics` | Last 3-5 conversation topics — coaching references these |
| `tone` | Current conversation tone: chatty / neutral / heavy |
| `topicShifts` | Number of topic changes this session (avoidance signal) |
| `activeCommitment` | What the user said they'd work on |
| `lastCommitmentMention` | When they last referenced it (focus drift detection) |
| `strategyOutcomes` | Which coaching strategies worked/failed (see below) |

### Job types

| Job | Time | Type | How it works |
|---|---|---|---|
| `morning-checkin` | 8:00 AM | Coaching nudge | Sends `[coaching-nudge:morning]` to main session |
| `random-engagement-morning` | 11:15 AM | Random | Isolated, probability-based, checks activity |
| `noon-followup` | 12:35 PM | Coaching nudge | Sends `[coaching-nudge:noon]` to main session |
| `random-engagement-afternoon` | 3:00 PM | Random | Isolated, probability-based, checks activity |
| `evening-review` | 9:00 PM | Coaching nudge | Sends `[coaching-nudge:evening]` to main session |
| `random-engagement-evening` | 8:30 PM | Random | Isolated, probability-based, checks activity |
| `midweek-check` | Wed 10 AM | Coaching nudge | Sends `[coaching-nudge:midweek]` to main session |
| `weekly-reflection` | Sun 6 PM | Isolated | Reads weekly notes, writes analysis |
| `nightly-maintenance` | 2:00 AM | Isolated | Archives, cleans, updates patterns |
| `email-check` | Every 3h | Isolated | Checks for new emails |

**Coaching nudges** → `sessionTarget: "main"` — deliver to the active conversation
**Random engagement** → `sessionTarget: "isolated"` — separate session, checks activity first
**Maintenance/reflection** → `sessionTarget: "isolated"` — background work

### How the agent handles nudges

When the main session receives `[coaching-nudge:morning]`, the agent:

1. Checks `session-state.json` for `recentTopics`, `tone`, `activeCommitment`
2. References what you and the agent were actually talking about
3. Responds as a natural check-in, not a scheduled message
4. Updates `coachingSent` timestamp

**Example nudges:**
- After a coding session: "You've been grinding on that Astro site for hours. Still in the zone or time for a break?"
- After frustration: "That CMS hunt was rough. Did you land on anything or still circling?"
- After silence: "Quiet day. Everything okay, or just heads-down on something?"
- Morning after late night: "You were up till 5 AM. How are you even awake?"

### Setup

1. Replace placeholders in `CRON.md` (timezone, chat ID, agent name, user name)
2. Create each cron job — coaching nudges use `sessionTarget: "main"`, others use `"isolated"`
3. Create `session-state.json` in your workspace root:

```json
{
  "date": "YYYY-MM-DD",
  "lastActivity": null,
  "coachingSent": [],
  "coachingResponses": [],
  "randomSent": 0,
  "activeNow": false,
  "recentTopics": [],
  "tone": "neutral",
  "topicShifts": 0,
  "activeCommitment": null,
  "lastCommitmentMention": null,
  "strategyOutcomes": []
}
```

The nightly maintenance resets daily fields each night.

---

## 🧠 Coaching memory

Aristos tracks which coaching strategies actually work for each specific person and adjusts over time. This is what separates it from generic AI coaching — it learns what lands and what doesn't.

### Outcome tracking in session-state.json

After each coaching nudge, the agent logs the outcome in `strategyOutcomes`:

```json
{
  "date": "2026-03-26",
  "strategy": "implementation-intentions",
  "context": "dominius-avoidance",
  "response": "engaged",
  "effective": true
}
```

| Field | Meaning |
|---|---|
| `strategy` | Which strategy was used (from STRATEGIES.md) |
| `context` | What pattern it was applied to |
| `response` | `engaged` / `no-response` / `deflected` |
| `effective` | Did it lead to action within 24h? |

### How it improves coaching

**Nightly review** (during maintenance):
- Aggregate this week's outcomes by strategy
- Update MEMORY.md strategy log with results
- Flag ineffective strategies: "Socratic questioning: 0/4 responses. Implementation intentions: 3/4 responses."
- Recommend rotation: "Use implementation intentions more. Drop Socratic for two weeks."

**Real-time adaptation**:
- Before responding to a coaching nudge, the agent checks recent outcomes
- If a strategy has failed 2+ times recently, skip it
- If a strategy consistently works, prioritize it

### Example strategy log in MEMORY.md

| Date | Pattern | Strategy tried | Result | Next move |
|---|---|---|---|---|
| 03-26 | Dominius avoidance | Casual opener | No response | Try implementation intentions |
| 03-25 | CMS distraction | Humor redirect | Engaged, pivoted back | Use more humor for distraction |
| 03-24 | Low energy after BCS | Presence (no agenda) | John opened up | Presence works for post-BCS days |

### The loop

```
Coach with strategy → Log outcome → Nightly analysis → Update rotation → Coach with better strategy
                                                                                       ↑
                                                                                       └─── Repeat forever
```

Over weeks, the agent builds a personalized coaching playbook unique to each user. What works for one person (humor, directness) might fail for another (Socratic questioning, gentle nudges). The framework discovers this automatically.

---

## 🔌 Agent vault access

None of this works unless the agent has **live file access to the vault**. The journal entries only become coaching data if the agent can actually open them.

This means the vault - the folder containing your `Journal/` and `AI Instructions/` files - needs to live somewhere the agent can reach via the filesystem.

**If you use Obsidian to write your journal** (recommended), the simplest way to guarantee 24/7 agent access is to keep a headless Obsidian instance running on your server alongside the agent - so the vault is always present on disk, always up to date, and always readable.

> #### 🖥️ [Kasmidian](https://github.com/Cityjohn/Kasmidian) - Obsidian in Docker, always on
>
> [Kasmidian](https://github.com/Cityjohn/Kasmidian) is a Docker Compose setup that runs Obsidian headlessly in a browser-accessible container (via KasmVNC). Deploy it on the same host as your agent and mount the vault as a shared volume - your agent always has the latest journal on disk, always up to date.
>
> Pair it with **Obsidian Sync**: write your daily notes on your phone or laptop as normal, Sync pushes them to the server, Kasmidian keeps the vault live on disk, and the agent reads them the moment they arrive.
>
> ```
> You (phone/laptop) → Obsidian Sync → Kasmidian vault on server
>                                              ↓
>                                         Agent reads files
> ```
>
> No local Obsidian install required on the server. No manual transfers. The vault is just always there.

---

## 🏗️ Key design decisions

**Why coaching nudges instead of isolated sessions?**

Isolated sessions have zero conversation context. They generate generic messages that ignore what the user was actually talking about. Coaching nudges trigger the main session, which has full history and responds contextually - like a friend who was paying attention, not a cron job with amnesia.

**Why outcome tracking?**

Without tracking which strategies work, the agent rotates blindly. The same ineffective approach gets repeated. Outcome tracking creates a feedback loop: coach → log → analyze → adapt → coach better. Over weeks, the agent builds a personalized playbook unique to each user.

**Why split into bootstrap and on-demand files?**

Bootstrap files (~7,200 tokens) guarantee the agent always has identity, rules, and current state. On-demand files (STRATEGIES, PREDICTIVE, etc.) are only loaded when relevant - a coaching session needs them, an outreach ping doesn't. This keeps everyday invocations lean.

**Why adaptive mode in MEMORY.md instead of AGENTS.md?**

Mode transitions are reference material - needed when evaluating which mode John is in, not every reply. Placing them next to the current mode state in MEMORY.md (which is always in context) makes them accessible without bloating AGENTS.md.

**Why a flat memory file instead of just the vector DB?**

The vector DB is great for retrieval by similarity but bad for structured current state. "What are the user's active commitments?" is a table lookup, not a semantic search. The flat file gives instant access to current state.

**Why 30-day archival?**

Without it, the memory file grows indefinitely. The 30-day cycle moves history to the vector DB (searchable but not always loaded) and keeps the working file small.

**Why session-state.json as a shared scratchpad?**

It's the one file that's read by both cron jobs and the main session. Activity timestamps, coaching state, conversation topics, and strategy outcomes all live here. It's the bridge between scheduled events and real-time conversation.

---

**For people who are trying their best.**

---

<p align="center">
  <a href="https://star-history.com/#cityjohn/Aristos&Date" title="Star History">
    <img src="https://api.star-history.com/svg?repos=cityjohn/Aristos&type=Date&theme=dark&transparent=true" alt="Star History Chart" width="500" />
  </a>
</p>

<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=cityjohn.Aristos" alt="Visitors" />
</p>
