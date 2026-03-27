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
- [🧠 The Knowledge Graph](#-the-knowledge-graph)
- [📓 The Journal - 2 minutes a day](#-the-journal--2-minutes-a-day)
- [📋 What's in each file](#-whats-in-each-file)
- [🔄 How file loading works](#-how-file-loading-works)
- [💰 Token load per invocation](#-token-load-per-invocation)
- [⏰ Cron-based outreach](#-cron-based-outreach)
- [🧠 Coaching memory](#-coaching-memory)
- [🔌 Agent vault access](#-agent-vault-access)
- [🏗️ Key design decisions](#️-key-design-decisions)
- [📖 Detailed documentation](#-detailed-documentation)

---

## 📖 What it actually looks like

*Happiness doesn't just happen to you, it's about what you happen to do.*

The journal is just a few easy prompts. You write what's real - a big win, a hard week, a goal that has nothing to do with work. The agent builds a picture across all of it and coaches accordingly. Full example notes are in the repo - [`Journal/Day to Day/`](Journal/Day%20to%20Day/), [`Journal/Weekly reflection/`](Journal/Weekly%20reflection/), [`Journal/Yearly planning/`](Journal/Yearly%20planning/).

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

The agent tracks all of it over time - output, energy, what you keep postponing, who you care about, what kind of week you're in. That's what lets it coach you as a full person, not just a task list. Browse the example entries in [`Journal/Day to Day/2025-03-15.md`](Journal/Day%20to%20Day/2025-03-15.md), [`Journal/Weekly reflection/2025-W11.md`](Journal/Weekly%20reflection/2025-W11.md), and [`Journal/Yearly planning/2025.md`](Journal/Yearly%20planning/2025.md) to see the format in full.

---

## ✨ Features

🧠 **Adaptive Coaching** - Four modes (returning, struggling, baseline, momentum) that shift based on your actual behavior, not your intentions.

🎯 **Strategy Rotation with Outcome Tracking** - 20+ coaching strategies drawn from ACT, behavioral psychology, and implementation science. Tracks what works for *you* and rotates accordingly.

📓 **Journal Integration** - Reads your daily, weekly, and yearly notes. Spots patterns you miss. Follows up on things you said you'd do.

💬 **Contextual Coaching** - Coaching nudges fire on schedule but respond from the main conversation with full context. No robotic "how's your morning?" from a blank slate.

🔮 **Predictive Coaching** - Uses historical data to anticipate problems before they happen. Knows your risky days, your seasonal dips, your commitment patterns.

🫶 **Trauma-Aware** - Understands that resistance isn't laziness. Knows when to push and when to just be there. Never shames. Never lectures.

🧠 **Knowledge Graph** - Semantic search + wiki link graph traversal across all journal entries and coaching notes. Learns your patterns by association, not just keywords.

---

## 🚀 Quick start

1. Clone this repo
2. The `Journal/` folder is shared - keep it
3. Copy the files from `AI Instructions - Claw/` into your OpenClaw workspace
4. Fill in `IDENTITY.md`, `USER.md`, and `TOOLS.md` with your specifics
5. Make the vault accessible to your agent - if you use Obsidian, [Kasmidian](https://github.com/Cityjohn/Kasmidian) + Obsidian Sync is the recommended setup
6. Set up cron jobs for outreach (see [Cron-based outreach](#-cron-based-outreach))
7. Start writing your daily note - the agent handles the rest

---

## 📁 Folder structure

```
Journal/
  Templates/
    Daily Focus Template.md          - copy to Day to Day/ as YYYY-MM-DD.md
    Weekly Reflection Template.md    - copy to Weekly reflection/ as YYYY-Www.md
    Yearly Template.md               - copy to Yearly planning/ as YYYY.md
  Day to Day/
    2025-03-15.md                    - example daily note
  Weekly reflection/
    2025-W11.md                      - example weekly note
  Yearly planning/
    2025.md                          - example yearly plan

  Aris Coaching/                     - coaching-specific knowledge
    coaching-strategies.md           - strategy menu by situation
    predictive-patterns.md           - pattern prediction from history
    journal-reading-guide.md         - how to parse journal entries
    coaching-learnings/              - monthly outcome summaries
    patterns/                        - named patterns (post-BCS-avoidance, etc.)
    insights/                        - daily coaching notes

  Our Knowledge/                     - shared knowledge
    (research, observations, concepts, frameworks)

AI Instructions - Claw/
  SOUL.md                            - personality, voice, communication style
  AGENTS.md                          - operating manual, rules, file loading
  IDENTITY.md                        - agent identity (fill in)
  USER.md                            - human context (fill in)
  TOOLS.md                           - local setup, journal paths, cron docs (fill in)
  MEMORY.md                          - live state, mode, goals, commitments, patterns
  HEARTBEAT.md                       - heartbeat check logic
  PROACTIVE_OUTREACH.md              - outreach rules (loaded on demand)
  MEMORY_SCHEMA.md                   - archival rules, memory systems
  CRON.md                            - cron job setup, prompts, probability logic
  session-state.json                 - tracks activity, coaching state, conversation
```

### Three indexed directories

The vault is split into three directories, all automatically indexed in SQLite for semantic search:

| Directory | Owner | Contents |
|---|---|---|
| `Journal/Day to Day/`, `Weekly reflection/`, `Yearly planning/` | You | Personal journal - 2 minutes a day |
| `Journal/Aris Coaching/` | Aris | Strategies, patterns, insights, outcome tracking |
| `Journal/Our Knowledge/` | Shared | Research, observations, concepts |

All `.md` files in all three directories are indexed. Wiki links connect across directories. The agent never edits your journal directly - it writes its own notes that link to yours.

---

## 🧠 The Knowledge Graph

Aristos uses SQLite + sqlite-vec for semantic search across all vault content, combined with wiki link graph traversal for associative reasoning.

### Obsidian as the single source of truth

Your entire Obsidian vault is the canonical data layer. Not a database export, not a summary, not a cache. The `.md` files themselves are what the agent reads, indexes, and reasons over.

This means:

- **You write in Obsidian** (phone, laptop, whatever) — your notes are the record
- **The agent reads the same files** — no translation layer, no sync delay, no data duplication
- **Wiki links you create ARE the knowledge graph** — when you connect `[[post-BCS-avoidance]]` to `[[career transition]]`, that's a real graph edge the agent traverses
- **Everything lives in one place** — your journal, your coaching notes, your research, all connected through the same filesystem and the same link graph

The SQLite index (vectors + edges) is a **search accelerator**, not a separate data store. If the database is deleted, re-indexing from the vault rebuilds everything. The vault is authoritative. The index is disposable.

This is why the three-directory structure matters: your personal journal stays untouched, Aris writes coaching observations that link TO your entries, and shared knowledge connects across both. But it's all one vault, one graph, one source of truth.

### How it works

Every `.md` file in the vault gets:
1. **Embedded** - content converted to a 3072-dim vector (OpenRouter text-embedding-3-large)
2. **Parsed for links** - `[[wiki links]]` extracted and stored as graph edges
3. **Indexed** - vector + edges stored in `~/.openclaw/vault-memory.db`

When the agent needs context, a single hybrid query runs:
- **70% semantic similarity** - find notes by meaning, not keywords
- **30% graph distance** - follow wiki links (2 hops max, 50% decay per hop)

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

> 📖 **Technical deep-dive:** Full vault-memory specification (database schema, indexing pipeline, query engine, HippoRAG comparison) is in [reference/vault-memory.md](reference/vault-memory.md).

---

## 📓 The Journal - 2 minutes a day

The journal is the only thing you have to do. The AI handles everything else.

The templates are designed to be the **minimum viable input** - enough structure that an AI agent can reason about your life across three timescales (day, week, year), but short enough that you'll actually do it. A daily note takes about two minutes. A weekly reflection takes ten, once a week. The yearly note you fill in once.

That's it. The agent reads them, spots patterns you don't, and uses what it finds to coach you.

---

### Daily Focus Template (~2 minutes)

Three sections. That's the whole thing.

**Morning (~1 min):**

- **Mission and priorities** - One sentence: "My mission today is to..." + 2-4 bullet priorities. The agent checks whether this aligns with your weekly/yearly goals and whether you're overloading yourself.
- **Time and metrics** - How many hours you have, the exact sequence of steps, what "done" looks like. The agent uses this to assess whether your plan is realistic and to follow up on whether you hit it.

**Evening (~1 min):**

- **End of day review** - Gratitude, distractions, what you completed vs planned, mood/energy 1-10. The execution gap (planned vs done), your mood trend, what's consistently getting in the way.

> The end-of-day review is the most important section. Even one sentence per prompt is enough. The mood/energy score alone - tracked over weeks - gives the agent a reliable signal for when to push and when to back off.

### Weekly Reflection Template (~10 minutes, once a week)

Two sections:

- **End of week review** - Wins, distractions, emotional moments, energy patterns. The agent uses this to update strategy rotation.
- **Plans and adjustments** - Specific changes for next week. The agent tracks whether these adjustments actually land the following week.

### Yearly Template (once, review quarterly)

Five sections covering your year mission, concrete milestones, reverse goal mapping, and a month-by-month breakdown. The yearly note is the **anchor** - it's what prevents the agent from helping you optimize tasks that shouldn't exist.

### Why this is enough

Every field is **parseable as a coaching signal**:

- **Mission + priorities** - intention signal
- **Time and metrics** - capacity signal
- **Completions vs plan** - execution gap
- **Distractions** - interference pattern
- **Mood/energy score** - baseline trend
- **Weekly summary bullets** - signal compression
- **Yearly milestones** - long-range anchor

Two minutes of structured writing gives the agent everything it needs - not because it's a lot of data, but because it's the *right* data.

---

## 📋 What's in each file

**Workspace files (AI Instructions - Claw/)**

| File | Delivery | Purpose |
|---|---|---|
| `SOUL.md` | Bootstrap | Personality, voice, communication style |
| `AGENTS.md` | Bootstrap | Operating manual, rules, file loading |
| `IDENTITY.md` | Bootstrap | Agent identity - name, emoji, purpose |
| `USER.md` | Bootstrap | Human context - name, timezone, priorities |
| `TOOLS.md` | Bootstrap | Local setup - journal paths, cron, devices |
| `MEMORY.md` | Bootstrap | Live state - mode, goals, commitments, patterns |
| `HEARTBEAT.md` | Bootstrap | Heartbeat check logic |
| `PROACTIVE_OUTREACH.md` | On demand | When/how to reach out unprompted |
| `MEMORY_SCHEMA.md` | On demand | Memory systems, archival rules |
| `CRON.md` | On demand | Cron job setup, prompts, probability logic |
| `session-state.json` | Runtime | Activity, coaching state, conversation topics |

**Obsidian files (Journal/Aris Coaching/)**

| File | Purpose |
|---|---|
| `coaching-strategies.md` | Strategy menu by situation |
| `predictive-patterns.md` | Pattern prediction from historical data |
| `journal-reading-guide.md` | How to parse journal entries |
| `coaching-learnings/` | Monthly outcome summaries |
| `patterns/` | Named patterns with evidence links |
| `insights/` | Daily coaching notes |

### Setup files (fill in these)

| File | What to fill in |
|---|---|
| `IDENTITY.md` | Your agent's name, emoji, purpose |
| `USER.md` | Your name, timezone, work context, current priorities |
| `TOOLS.md` | Path to your Obsidian vault, cron schedule, device notes |

---

## 🔄 How file loading works

| Type | Meaning | Files |
|---|---|---|
| `bootstrap: true` | Auto-injected every call, always in context | SOUL, AGENTS, IDENTITY, USER, TOOLS, MEMORY, HEARTBEAT |
| *(no frontmatter)* | Loaded on demand via `read_file` | PROACTIVE_OUTREACH, MEMORY_SCHEMA, CRON |

Bootstrap files cost tokens on every call but guarantee the agent always has identity, rules, and current state. On-demand files are only loaded when relevant.

**Obsidian files** (Aris Coaching, journal entries) are loaded via vector DB search when context matters, not on every call.

---

## 💰 Token load per invocation

📊 **Bootstrap files** (~7,200 tokens every call)

| File | Est. tokens |
|---|---|
| `SOUL.md` | ~2,100 |
| `AGENTS.md` | ~1,800 |
| `IDENTITY.md` | ~170 |
| `USER.md` | ~235 |
| `TOOLS.md` | ~540 |
| `MEMORY.md` | ~2,300 |
| `HEARTBEAT.md` | ~42 |

📊 **Token cost by invocation type**

| Type | Est. tokens | Notes |
|---|---|---|
| Every call (minimum) | ~7,200 | Bootstrap only |
| Coaching (with vector DB) | ~8,700 + journal | 5 relevant snippets (~1,500 tokens) instead of 20 mixed (~4,000) |
| Coaching (without vector DB) | ~15,000-20,000 | Broad file reads, manual context gathering |
| Outreach trigger | ~9,500 | Bootstrap + PROACTIVE_OUTREACH |
| Memory maintenance | ~8,800 | Bootstrap + MEMORY_SCHEMA |

> **Vector DB impact:** Coaching calls drop ~40-50% in token usage. The DB retrieves only relevant context instead of loading broad file dumps. Historical patterns surface automatically without manual searching.

---

## ⏰ Cron-based outreach

### Architecture: Coaching nudges vs isolated sessions

Coaching nudges trigger the **main session** - with full conversation context. Isolated jobs handle random engagement, maintenance, and reflection.

```
Coaching nudges (contextual):
  Cron fires -> Trigger sent to main session -> Agent responds WITH full context

Isolated jobs (background):
  Cron fires -> Separate session -> Reads files -> Sends message
```

### The session-state.json bridge

Shared state between cron jobs and main session:

| Field | Purpose |
|---|---|
| `lastActivity` | When user was last active - jobs skip if within 90 minutes |
| `coachingSent` | Timestamps of coaching nudges sent today |
| `coachingResponses` | Whether user responded to coaching nudges |
| `randomSent` | Count of random engagement messages today (cap: 3) |
| `recentTopics` | Last 3-5 conversation topics - coaching references these |
| `tone` | Current conversation tone: chatty / neutral / heavy |
| `topicShifts` | Number of topic changes this session (avoidance signal) |
| `activeCommitment` | What the user said they'd work on |
| `lastCommitmentMention` | When they last referenced it (focus drift detection) |
| `strategyOutcomes` | Which coaching strategies worked/failed |

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

### How nudges work

When the main session receives a coaching nudge, the agent:
1. Checks `session-state.json` for `recentTopics`, `tone`, `activeCommitment`
2. References what was being discussed
3. Responds as a natural check-in, not a scheduled message
4. Updates `coachingSent` timestamp

**Examples:**
- After a coding session: "You've been grinding on that Astro site for hours. Still in the zone or time for a break?"
- After frustration: "That CMS hunt was rough. Did you land on anything or still circling?"
- After silence: "Quiet day. Everything okay, or just heads-down on something?"

---

## 🧠 Coaching memory

Outcome tracking creates a feedback loop: coach, log, analyze, adapt, coach better.

### Outcome tracking

After each coaching nudge, the agent logs the outcome in `strategyOutcomes`:

| Field | Meaning |
|---|---|
| `strategy` | Which strategy was used |
| `context` | What pattern it was applied to |
| `response` | engaged / no-response / deflected |
| `effective` | Did it lead to action within 24h? |

### How it improves

**Nightly review:** Aggregate outcomes by strategy. Flag ineffective ones. Recommend rotation.

**Real-time adaptation:** Before coaching, check recent outcomes. Skip strategies that failed 2+ times. Prioritize ones that work.

**The loop:**
Coach with strategy -> Log outcome -> Nightly analysis -> Update rotation -> Coach with better strategy -> Repeat forever

Over weeks, the agent builds a personalized coaching playbook. What works for one person (humor, directness) might fail for another. The framework discovers this automatically.

### Coaching log in Aris Coaching/

Outcome summaries live in the vault, not just in session-state.json:

```markdown
# Strategy outcomes - March 2026
- implementation-intentions: 4/5 effective on avoidance patterns
- humor-redirect: 3/4 effective on distraction
- socratic-questioning: 0/4 - avoid for this person
```

These are indexed in SQLite. When the agent searches for coaching context, it finds strategy outcomes alongside journal entries and pattern notes.

---

## 🔌 Agent vault access

The vault needs to live somewhere the agent can reach via the filesystem.

**If you use Obsidian to write your journal** (recommended), the simplest way to guarantee 24/7 agent access is [Kasmidian](https://github.com/Cityjohn/Kasmidian) - a Docker Compose setup that runs Obsidian headlessly via KasmVNC. Deploy it on the same host as your agent and mount the vault as a shared volume.

Pair it with **Obsidian Sync**: write your daily notes on your phone or laptop, Sync pushes them to the server, Kasmidian keeps the vault live on disk, and the agent reads them the moment they arrive.

```
You (phone/laptop) -> Obsidian Sync -> Kasmidian vault on server
                                              |
                                         Agent reads files
```

---

## 🏗️ Key design decisions

**Why three directories instead of one?**

Separation of concerns. Your journal is personal - the agent reads it but never edits it. Aris Coaching is where the agent builds its understanding of your patterns. Our Knowledge is shared ground for discoveries and concepts. All three are indexed in SQLite, but ownership is clear.

**Why coaching nudges instead of isolated sessions?**

Isolated sessions have zero conversation context. Coaching nudges trigger the main session, which has full history and responds contextually - like a friend who was paying attention.

**Why outcome tracking?**

Without it, the agent rotates blindly. The same ineffective approach gets repeated. Outcome tracking creates a feedback loop that builds a personalized playbook over time.

**Why vector DB instead of just file reads?**

File reads are broad - you load entire files hoping relevant context is in there. Vector search retrieves only relevant snippets by meaning. Token usage drops 40-50% for coaching calls, and quality improves because noise is filtered out.

**Why wiki links as graph edges?**

Your wiki links ARE your knowledge graph. They represent your editorial judgment about what's connected. The graph traversal surfaces connected knowledge that keyword search misses.

**Why hybrid scoring (70% semantic + 30% graph)?**

Pure semantic search finds notes by meaning but misses editorial connections. Pure graph search follows your links but misses implicit patterns. Hybrid gives you both: what's semantically relevant AND what you've explicitly connected.

**Why split bootstrap and on-demand files?**

Bootstrap files (~7,200 tokens) guarantee identity, rules, and state on every call. On-demand files are only loaded when relevant. Everyday invocations stay lean.

**Why session-state.json as shared scratchpad?**

It's the one file read by both cron jobs and the main session. Activity timestamps, coaching state, conversation topics, and strategy outcomes live here as the bridge between scheduled events and real-time conversation.

**Why 30-day archival?**

Without it, MEMORY.md grows indefinitely. The 30-day cycle moves history to the vector DB and keeps the working file small.

---

## 📖 Detailed documentation

For deeper dives on specific topics:

| Document | What it covers |
|---|---|
| [guides/setup.md](guides/setup.md) | Step-by-step setup, folder structure, vault access |
| [guides/journal.md](guides/journal.md) | Journal templates, examples, signal types |
| [reference/architecture.md](reference/architecture.md) | File loading internals, token optimization, deep design rationale |
| [reference/cron.md](reference/cron.md) | Full cron job definitions, probability formulas, coaching nudge prompts |
| [reference/vault-memory.md](reference/vault-memory.md) | Vault-memory technical spec: DB schema, indexing pipeline, query engine, HippoRAG comparison |

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
