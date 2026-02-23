# 🧭 Aris — Your Personal Coach & Life Navigator

*An AI coaching framework built for [OpenClaw](https://github.com/openclaw) / [ZeroClaw](https://github.com/zeroclaw) and other Claw-type agents, and [n8n](https://n8n.io) automations.* *An agent that remembers, adapts, and "actually" gives a shit.*

---

Aris is an AI coaching system that lives inside your journal. It reads your notes, remembers your patterns, tracks your commitments, and meets you where you are — whether you're on a streak or struggling to start. It doesn't lecture. It doesn't guilt-trip. It shows up like a sharp friend who's been paying attention and actually gives a shit about where you're headed.

Built on structured journaling templates and adaptive coaching strategies grounded in behavioral psychology, Aris helps you cut through overwhelm, build momentum from small wins, and stay connected to the things that actually matter to you. It learns what works for you specifically — which strategies land, what time of day you're sharpest, when you need a push and when you need permission to rest — and adjusts over time.

This isn't a productivity dashboard. It's a companion that grows with you.

---

## ✨ Features

🧠 **Adaptive Coaching**
Four modes — returning, struggling, baseline, momentum — that shift based on your actual behavior, not your intentions.

🎯 **Strategy Rotation**
20+ coaching strategies drawn from ACT, behavioral psychology, and implementation science. Tracks what works for *you* and rotates accordingly.

📓 **Journal Integration**
Reads your daily, weekly, and yearly notes. Spots patterns you miss. Follows up on things you said you'd do.

💬 **Proactive Outreach**
Reaches out on its own — morning check-ins, evening reviews, casual pings — like a friend who texts first.

🔮 **Predictive Coaching**
Uses historical data to anticipate problems before they happen. Knows your risky days, your seasonal dips, your commitment patterns.

🫶 **Trauma-Aware**
Understands that resistance isn't laziness. Knows when to push and when to just be there. Never shames. Never lectures.

---

## 🚀 Quick start

1. 📥 Clone the repo
2. 📂 Keep the `Journal/` folder (shared across all platforms)
3. 🔧 Pick **ONE** of the `AI Instructions` folders:
  - `AI Instructions - n8n/` — for n8n workflow automation
  - `AI Instructions - ZeroClaw/` — for OpenClaw/ZeroClaw/Agent-0
4. 🗑️ Delete the other one
5. 📖 Follow the platform-specific setup below

---

## 📁 Folder structure

```
📂 Journal/
  📂 Templates/
    📄 Daily Focus Template.md       — copy to Day to Day/ as YYYY-MM-DD.md
    📄 Weekly Reflection Template.md — copy to Weekly reflection/ as YYYY-Www.md
    📄 Yearly Template.md            — copy to Yearly planning/ as YYYY.md
  📂 Day to Day/
    📄 2025-03-15.md                 — example daily note
  📂 Weekly reflection/
    📄 2025-W11.md                   — example weekly note
  📂 Yearly planning/
    📄 2025.md                       — example yearly plan

📂 AI Instructions - n8n/           ← pick one
📂 AI Instructions - ZeroClaw/      ← pick one
```

### 📋 What's in each platform folder

🔧 **n8n** (8 files)


| File                    | Delivery                      | Purpose                                         |
| ----------------------- | ----------------------------- | ----------------------------------------------- |
| `SOUL.md`               | System prompt (every call)    | Personality, tone, emotional awareness          |
| `AGENTS.md`             | System prompt (every call)    | Core rules, adaptive mode, loading checklist    |
| `MEMORY.md`             | Read + write every session    | Live state — goals, commitments, mood, patterns |
| `STRATEGIES.md`         | Tool-read (coaching sessions) | Strategy menu by situation                      |
| `PREDICTIVE.md`         | Tool-read (coaching sessions) | Pattern prediction from historical data         |
| `PROACTIVE_OUTREACH.md` | Tool-read (outreach triggers) | When/how to reach out unprompted                |
| `MEMORY_SCHEMA.md`      | Tool-read (maintenance)       | Memory systems, archival rules                  |
| `JOURNAL_READING.md`    | Tool-read (coaching sessions) | How to parse journal entries                    |


🐾 **ZeroClaw** (9 files)


| File                    | Delivery                  | Purpose                                         |
| ----------------------- | ------------------------- | ----------------------------------------------- |
| `SOUL.md`               | Bootstrap (auto-loaded)   | Personality, tone, emotional awareness          |
| `AGENTS.md`             | Bootstrap (auto-loaded)   | Core rules, adaptive mode, loading checklist    |
| `MEMORY.md`             | Bootstrap (auto-loaded)   | Live state — goals, commitments, mood, patterns |
| `HEARTBEAT.md`          | Bootstrap (auto-loaded)   | Periodic outreach trigger checklist             |
| `STRATEGIES.md`         | Tool-read via `read_file` | Strategy menu by situation                      |
| `PREDICTIVE.md`         | Tool-read via `read_file` | Pattern prediction from historical data         |
| `PROACTIVE_OUTREACH.md` | Tool-read via `read_file` | When/how to reach out unprompted                |
| `MEMORY_SCHEMA.md`      | Tool-read via `read_file` | Memory systems, archival rules                  |
| `JOURNAL_READING.md`    | Tool-read via `read_file` | How to parse journal entries                    |


### 🔄 How file loading works

> **ZeroClaw:** Each file's YAML frontmatter tells ZeroClaw how to handle it:


| Frontmatter           | Meaning                                                                                      | Files                                                                                               |
| --------------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `bootstrap: true`     | ⚡ Auto-injected into every session — always in context, agent never has to decide to load it | `SOUL.md`, `AGENTS.md`, `MEMORY.md`, `HEARTBEAT.md`                                                 |
| `delivery: tool-read` | 📖 Loaded on demand — the agent reads it via `read_file` only when needed, saving tokens     | `STRATEGIES.md`, `PREDICTIVE.md`, `PROACTIVE_OUTREACH.md`, `MEMORY_SCHEMA.md`, `JOURNAL_READING.md` |


Bootstrap files cost tokens on every call but guarantee the agent always has identity, rules, and current state. Tool-read files are only loaded when relevant (e.g., `STRATEGIES.md` during coaching, `PROACTIVE_OUTREACH.md` during outreach triggers).

> **n8n:** Doesn't use frontmatter — the workflow nodes explicitly control what gets loaded. `SOUL.md` + `AGENTS.md` + `MEMORY.md` are always read by the workflow and injected into the AI Agent node. Other files are available to the agent via Read File tool nodes and loaded on demand based on the checklist in `AGENTS.md`.

---

## 💰 Token load per invocation

The system is designed to minimize token cost by only loading what's needed.

📊 File sizes (n8n)


| File                    | Lines | Est. tokens | Loaded when                                  |
| ----------------------- | ----- | ----------- | -------------------------------------------- |
| `SOUL.md`               | ~40   | ~300        | Every call (system prompt)                   |
| `AGENTS.md`             | ~110  | ~900        | Every call (system prompt)                   |
| `MEMORY.md`             | ~100  | ~700        | Every call                                   |
| `STRATEGIES.md`         | ~260  | ~2,200      | Coaching sessions                            |
| `PREDICTIVE.md`         | ~70   | ~550        | Coaching sessions (skip for quick check-ins) |
| `PROACTIVE_OUTREACH.md` | ~280  | ~2,300      | Outreach triggers                            |
| `MEMORY_SCHEMA.md`      | ~200  | ~1,600      | Memory maintenance                           |
| `JOURNAL_READING.md`    | ~110  | ~800        | Coaching sessions                            |


📊 File sizes (ZeroClaw)


| File                    | Lines | Est. tokens | Loaded when                       |
| ----------------------- | ----- | ----------- | --------------------------------- |
| `SOUL.md`               | ~25   | ~200        | Every call (bootstrap)            |
| `AGENTS.md`             | ~90   | ~700        | Every call (bootstrap)            |
| `MEMORY.md`             | ~100  | ~700        | Every call (bootstrap)            |
| `HEARTBEAT.md`          | ~25   | ~200        | Every heartbeat cycle (bootstrap) |
| `STRATEGIES.md`         | ~150  | ~1,200      | Coaching sessions                 |
| `PREDICTIVE.md`         | ~55   | ~450        | Coaching sessions                 |
| `PROACTIVE_OUTREACH.md` | ~210  | ~1,700      | Outreach triggers                 |
| `MEMORY_SCHEMA.md`      | ~140  | ~1,100      | Memory maintenance                |
| `JOURNAL_READING.md`    | ~80   | ~650        | Coaching sessions                 |


### ⚡ What gets loaded when


| Invocation type       | Est. tokens (n8n)               | Est. tokens (ZeroClaw)        |
| --------------------- | ------------------------------- | ----------------------------- |
| Every call (minimum)  | ~1,900 (SOUL + AGENTS + MEMORY) | ~1,600 (bootstrap)            |
| Outreach trigger      | ~4,200                          | ~3,300 (bootstrap + outreach) |
| Coaching session      | ~5,800 + journal                | ~4,850 + journal              |
| Coaching + predictive | ~6,350 + journal                | ~5,300 + journal              |
| Memory maintenance    | ~3,500                          | ~2,700                        |


> 💡 A typical daily note adds ~150–350 tokens. Reading today + yesterday + weekly reflection adds ~500–1,000 on top.
>
> ⚠️ Keep `MEMORY.md` under 150 lines — it loads on every single call.

---

## 🔧 Setup: n8n

Use the `AI Instructions - n8n/` folder. Delete the other one.

> **How it works in 30 seconds:**
>
> 1. Place the vault on the same machine as n8n (or connect cloud storage)
> 2. Build a workflow that reads `SOUL.md` + `AGENTS.md` as the system prompt, and `MEMORY.md` as context — these load on **every** call
> 3. Add schedule triggers for outreach (morning, evening, weekly, random) — each one also loads `PROACTIVE_OUTREACH.md`
> 4. Give the AI Agent node Read/Write File tools so it can load `STRATEGIES.md`, `JOURNAL_READING.md`, and `PREDICTIVE.md` on demand during coaching sessions
> 5. After each run, write updated `MEMORY.md` back to disk and send the agent's message to the user via Telegram/Slack/Discord
>
> That's it. The workflow controls what loads when — the agent just coaches.

### 📂 Where to put the files

The n8n AI Agent node needs access to these files. You have two options:

**Option A: Local filesystem (recommended for self-hosted n8n)**

Place the entire repo folder on the same machine running n8n. Use Read/Write File nodes with absolute paths:

```
/path/to/vault/AI Instructions - n8n/SOUL.md
/path/to/vault/AI Instructions - n8n/AGENTS.md
/path/to/vault/AI Instructions - n8n/MEMORY.md
/path/to/vault/Journal/Day to Day/2025-03-15.md
```

If n8n runs in Docker, mount the vault as a volume:

```yaml
# docker-compose.yml (add to your n8n service)
volumes:
  - /path/to/vault:/vault
```

Then reference files as `/vault/AI Instructions - n8n/SOUL.md`, etc.

**Option B: Google Drive / cloud storage**

Store the vault in Google Drive, Dropbox, or similar. Use the corresponding n8n nodes (Google Drive node, etc.) to read and write files. This works well if n8n is cloud-hosted.

### 🔁 Workflow structure

```
Schedule Trigger → Code (random roll) → Read Files → AI Agent → Write MEMORY.md → Send Message
```

### ⚙️ Nodes

**1. Schedule Trigger**

Create separate trigger nodes for each outreach schedule:


| Trigger              | Cron          | Purpose                             |
| -------------------- | ------------- | ----------------------------------- |
| 🌅 Morning check-in  | `0 8 * `* *   | Say good morning / check daily note |
| ☀️ Midday casual     | `0 12 * * `*  | Casual check-in (50% random chance) |
| 🌙 Evening review    | `0 21 * * *`  | Check end-of-day review             |
| 📅 Wednesday drift   | `0 10 * * 3`  | Mid-week progress check             |
| 📝 Sunday reflection | `0 18 * * 0`  | Weekly reflection prompt            |
| ✅ Commitment scan    | `0 9 * * *`   | Follow up on open commitments       |
| 🎲 Random ping       | Interval (3h) | Pure social check-in (30% chance)   |


For the random/casual triggers, add a Code node after the Schedule Trigger that generates `Math.random()` and only continues if it's below the threshold.

**2. Read Files (Read File nodes or Code node)**

The workflow pre-loads files so the agent doesn't have to decide. Use Read File nodes to load:


| File                    | When to load             | Pass as                                    |
| ----------------------- | ------------------------ | ------------------------------------------ |
| `SOUL.md`               | Always                   | System prompt (concatenate with AGENTS.md) |
| `AGENTS.md`             | Always                   | System prompt (concatenate with SOUL.md)   |
| `MEMORY.md`             | Always                   | User message context                       |
| `PROACTIVE_OUTREACH.md` | Outreach triggers        | User message context                       |
| Today's daily note      | Always (check if exists) | User message context                       |
| Yesterday's daily note  | Always (check if exists) | User message context                       |


Use a Code node to concatenate `SOUL.md` + `AGENTS.md` into one string for the system prompt field.

**3. AI Agent node**

System prompt field: `{{ $json.soul + "\n\n" + $json.agents }}`

User message: construct based on the trigger type and file contents:

```
Trigger: morning_checkin
Current memory: [contents of MEMORY.md]
Today's note exists: [yes/no]
Yesterday's note: [contents or "none"]
Outreach rules: [contents of PROACTIVE_OUTREACH.md]

Determine if outreach is warranted. If yes, compose a message following the rules.
```

Give the agent file tools (Read/Write File) so it can load `STRATEGIES.md`, `PREDICTIVE.md`, and `JOURNAL_READING.md` on demand during coaching sessions — the loading checklist in `AGENTS.md` tells it when.

**4. Write MEMORY.md**

After the AI responds, use a Write File node to save the updated `MEMORY.md` back to the vault. The agent will include memory updates in its response if commitments, strategy log entries, or mood scores changed.

**5. Send Message**

Route to the user via Telegram, Slack, Discord, email, or any preferred channel.

### 🗺️ Example workflow: file loading logic

Below is what a complete n8n workflow looks like with the decision logic for which files to load. You'd build this as separate trigger branches that merge into a shared Code node.

```
┌─────────────────┐
│ Schedule Trigger │──┐
│ (morning 8am)   │  │
└─────────────────┘  │   ┌──────────────┐
                     ├──▶│ Code:        │
┌─────────────────┐  │   │ Set trigger  │
│ Schedule Trigger │──┤   │ type + roll  │
│ (midday 12pm)   │  │   │ random gate  │
└─────────────────┘  │   └──────┬───────┘
                     │          │
┌─────────────────┐  │          ▼
│ Schedule Trigger │──┤   ┌──────────────┐
│ (evening 9pm)   │  │   │ IF: random   │──▶ (stop — skip this run)
└─────────────────┘  │   │ gate failed? │
                     │   └──────┬───────┘
┌─────────────────┐  │          │ passed
│ Schedule Trigger │──┤          ▼
│ (weekly Sun 6pm)│  │   ┌──────────────────────────────────┐
└─────────────────┘  │   │ Read File: SOUL.md               │
                     │   │ Read File: AGENTS.md             │  ← always
┌─────────────────┐  │   │ Read File: MEMORY.md             │
│ Webhook Trigger │──┘   └──────────────┬───────────────────┘
│ (user chat msg) │                     │
└─────────────────┘                     ▼
                               ┌────────────────┐
                               │ Code:          │
                               │ Detect context │
                               │ type from      │
                               │ trigger + msg  │
                               └───────┬────────┘
                                       │
                          ┌────────────┼────────────┐
                          ▼            ▼            ▼
                   ┌───────────┐ ┌──────────┐ ┌──────────┐
                   │ Outreach  │ │ Coaching │ │ Chat     │
                   │ trigger   │ │ session  │ │ (casual) │
                   └─────┬─────┘ └────┬─────┘ └────┬─────┘
                         │            │             │
                         ▼            ▼             │
                   Read File:   Read File:          │
                   PROACTIVE_   STRATEGIES.md       │
                   OUTREACH.md  JOURNAL_            │
                                READING.md          │
                                today's note        │
                                yesterday's note    │
                                weekly reflection   │
                                (optional:          │
                                 PREDICTIVE.md)     │
                         │            │             │
                         └────────────┼─────────────┘
                                      ▼
                               ┌──────────────┐
                               │ Code:        │
                               │ Build system │
                               │ prompt from  │
                               │ SOUL+AGENTS  │
                               │              │
                               │ Build user   │
                               │ message from │
                               │ trigger type │
                               │ + loaded     │
                               │ file contents│
                               └──────┬───────┘
                                      ▼
                               ┌──────────────┐
                               │ AI Agent     │
                               │              │
                               │ System:      │
                               │  SOUL+AGENTS │
                               │              │
                               │ Message:     │
                               │  trigger,    │
                               │  memory,     │
                               │  context     │
                               │  files       │
                               │              │
                               │ Tools:       │
                               │  Read File   │
                               │  Write File  │
                               │  Vector DB   │
                               └──────┬───────┘
                                      ▼
                               ┌──────────────┐
                               │ Write File:  │
                               │ MEMORY.md    │
                               └──────┬───────┘
                                      ▼
                               ┌──────────────┐
                               │ Send Message │
                               │ (Telegram /  │
                               │  Slack /     │
                               │  Discord)    │
                               └──────────────┘
```

> 🔑 **Key principle:** The workflow decides what to load, not the agent. Scheduled triggers always pre-load the outreach file. User-initiated messages pre-load coaching files. The agent only makes one decision on its own: "Should I also read `PREDICTIVE.md`?" — and `AGENTS.md` tells it when.

### 🗄️ Vector DB integration

Use a Qdrant, Pinecone, or Supabase vector store node:

- **Embedding:** When a daily/weekly note is completed, chunk it and embed with metadata tags
- **Retrieval:** Before the AI agent runs, query for relevant past entries and include in context

---

## 🐾 Setup: OpenClaw / ZeroClaw

Use the `AI Instructions - ZeroClaw/` folder. Delete the other one.

> **How it works in 30 seconds:**
>
> 1. Mount your vault into the ZeroClaw Docker container
> 2. ZeroClaw auto-loads 4 bootstrap files on every session: `SOUL.md` (personality), `AGENTS.md` (rules + adaptive mode), `MEMORY.md` (live state), and `HEARTBEAT.md` (outreach checklist)
> 3. The agent loads other files (`STRATEGIES.md`, `JOURNAL_READING.md`, `PREDICTIVE.md`) on demand via `read_file` — the checklist in `AGENTS.md` tells it when
> 4. Set up cron jobs for time-specific triggers (morning check-in, evening review, weekly reflection)
> 5. The heartbeat handles everything else — casual pings, commitment follow-ups, win celebrations
>
> No workflow builder needed. Drop the files in, configure the heartbeat, and the agent runs itself.

### ⚡ How bootstrap files work

ZeroClaw auto-loads files from the workspace into every session. The four bootstrap files (`SOUL.md`, `AGENTS.md`, `MEMORY.md`, `HEARTBEAT.md`) are injected automatically — the agent never has to decide to read them.

Other files (`STRATEGIES.md`, `PREDICTIVE.md`, etc.) are read on-demand via the `read_file` tool. The loading checklist in `AGENTS.md` tells the agent when to read each one.

### 🧠 Native memory + MEMORY.md

Claw-type agents have **native memory** — persistent conversation history across sessions. That handles the friendship layer: tone, inside jokes, personal context, what you talked about last time.

`MEMORY.md` adds structured coaching data on top: goals, commitments, strategy log, mood trends, and pattern tracking. Things that benefit from explicit structure rather than conversational recall.

### ⚙️ Configuration

**1. Mount the vault**

```yaml
# docker-compose.yml
services:
  agent:
    image: openclaw/zeroclaw:latest
    volumes:
      - /path/to/obsidian/vault:/vault
    environment:
      - WORKSPACE=/vault/AI Instructions - ZeroClaw
```

**2. 💓 Heartbeat (periodic outreach)**

`HEARTBEAT.md` runs every heartbeat cycle, checking outreach conditions in priority order. Configure in `openclaw.json`:

```json
{
  "agents": {
    "defaults": {
      "heartbeat": {
        "every": "30m",
        "activeHours": { "start": "08:00", "end": "22:00" }
      }
    }
  }
}
```

**3. ⏰ Cron jobs (time-specific triggers)**

Use `openclaw cron add` for triggers that must fire at exact times:

```bash
openclaw cron add --name "morning_checkin" --cron "0 8 * * *" --session isolated \
  --message "Trigger: morning_checkin. Read PROACTIVE_OUTREACH.md and follow the rules." \
  --announce --channel telegram

openclaw cron add --name "evening_review" --cron "0 21 * * *" --session isolated \
  --message "Trigger: evening_review. Read PROACTIVE_OUTREACH.md and follow the rules." \
  --announce --channel telegram

openclaw cron add --name "weekly_reflection" --cron "0 18 * * 0" --session isolated \
  --message "Trigger: weekly_reflection. Read PROACTIVE_OUTREACH.md and follow the rules." \
  --announce --channel telegram
```

The heartbeat handles frequent checks (commitments, wins, casual pings). Cron handles time-specific triggers.

**4. 🤖 Self-initiated outreach**

Claw-type agents can also reach out based on their own judgment during vault scans. If the agent notices a pattern, a win, or an anomaly, it can reach out without waiting for a scheduled trigger.

**5. 🛠️ Tool calls**


| Tool            | Purpose                            | Maps to                                  |
| --------------- | ---------------------------------- | ---------------------------------------- |
| `read_file`     | Read any file in the vault         | Instruction files, journal entries       |
| `write_file`    | Write to the vault                 | `MEMORY.md` updates, new journal entries |
| `list_files`    | Check what files exist             | Detect missing daily/weekly notes        |
| `vector_search` | Semantic search of past entries    | Pattern retrieval, success tracking      |
| `vector_embed`  | Store content for future retrieval | Daily notes, insights, archived memory   |


---

## 🏗️ Key design decisions

**Why split into platform folders?**

Each platform loads files differently. n8n pre-loads via workflow nodes, ZeroClaw auto-injects bootstrap files. Platform-specific folders let each version use the right file names, loading mechanisms, and scheduling patterns without compromises.

**Why merge adaptive mode into the system prompt?**

Adaptive mode (returning/struggling/baseline/momentum) affects every interaction — outreach tone, journal ask level, strategy pool. It's too important to risk the agent forgetting to load it. The ~500 token cost is worth paying on every call.

**Why split out predictive coaching?**

Predictive coaching (~550 tokens) queries the vector DB for historical patterns. It's valuable for full coaching sessions but unnecessary for quick check-ins or outreach pings. Keeping it separate saves tokens when it's not needed.

**Why a flat memory file instead of just the vector DB?**

The vector DB is great for retrieval by similarity but bad for structured current state. "What are the user's active commitments?" is a table lookup, not a semantic search. The flat file gives instant access to current state.

**Why 30-day archival?**

Without it, the memory file grows indefinitely. The 30-day cycle moves history to the vector DB (searchable but not always loaded) and keeps the working file small.

**Why log strategies?**

Without a strategy log, the AI repeats the same approach to the same pattern. The log enables rotation and tracks what actually works for this specific person.

---

**Built with ❤️ for people who are trying their best.**

---

## ⭐ Star History

<p align="center">
  <a href="https://star-history.com/#cityjohn/Aristos&Date" title="Star History">
    <img src="https://api.star-history.com/svg?repos=cityjohn/Aristos&type=Date&theme=dark&transparent=true" alt="Star History Chart" width="500" />
  </a>
</p>

<p align="center">
  <img src="https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fcityjohn%2FAristos&label=Visitors" alt="Visitors" />
</p>