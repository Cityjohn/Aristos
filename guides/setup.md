# 🚀 Setup Guide

Get Aristos running on your OpenClaw instance.

---

## Prerequisites

- [OpenClaw](https://github.com/openclaw/openclaw) installed and running
- An Obsidian vault (or any folder for your journal)
- Optional: [Kasmidian](https://github.com/Cityjohn/Kasmidian) for 24/7 vault access

## Step-by-step

1. **Clone this repo**
   ```bash
   git clone https://github.com/Cityjohn/Aristos.git
   ```

2. **Copy the journal** — The `Journal/` folder is yours. Keep it.

3. **Copy AI instructions** — Move files from `AI Instructions - Claw/` into your OpenClaw workspace.

4. **Fill in your specifics** — Three files need your input:

   | File | What to fill in |
   |------|-----------------|
   | `IDENTITY.md` | Your agent's name, emoji, purpose |
   | `USER.md` | Your name, timezone, work context, priorities |
   | `TOOLS.md` | Path to your Obsidian vault, cron schedule, devices |

5. **Make the vault accessible** — The agent needs filesystem access to your journal. See [Vault access](#vault-access) below.

6. **Set up cron jobs** — See [reference/cron.md](../reference/cron.md) for job definitions and setup.

7. **Write your first daily note** — Copy `Journal/Templates/Daily Focus Template.md` to `Journal/Day to Day/YYYY-MM-DD.md` and fill it in. The agent handles the rest.

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

## 🔌 Agent vault access

None of this works unless the agent has **live file access to the vault**. The journal entries only become coaching data if the agent can actually open them.

This means the vault - the folder containing your `Journal/` and `AI Instructions/` files - needs to live somewhere the agent can reach via the filesystem.

**If you use Obsidian to write your journal** (recommended), the simplest way to guarantee 24/7 agent access is [Kasmidian](https://github.com/Cityjohn/Kasmidian) - a Docker Compose setup that runs Obsidian headlessly via KasmVNC. Deploy it on the same host as your agent and mount the vault as a shared volume.

Pair it with **Obsidian Sync**: write your daily notes on your phone or laptop, Sync pushes them to the server, Kasmidian keeps the vault live on disk, and the agent reads them the moment they arrive.

```
You (phone/laptop) -> Obsidian Sync -> Kasmidian vault on server
                                              |
                                         Agent reads files
```

No local Obsidian install required on the server. No manual transfers. The vault is just always there.

---

Back to [README](../README.md) · [Journal Guide →](journal.md)
