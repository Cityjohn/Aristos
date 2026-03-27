# 🚀 Setup Guide

Get Aristos running on your OpenClaw instance in 10 minutes.

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

6. **Set up cron jobs** — See [reference/cron.md](reference/cron.md) for job definitions and setup.

7. **Write your first daily note** — Copy `Journal/Templates/Daily Focus Template.md` to `Journal/Day to Day/YYYY-MM-DD.md` and fill it in. The agent handles the rest.

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

## Vault access

None of this works unless the agent has **live file access to the vault**. The journal entries only become coaching data if the agent can actually open them.

**If you use Obsidian** (recommended), the simplest way to guarantee 24/7 agent access is [Kasmidian](https://github.com/Cityjohn/Kasmidian) — a Docker Compose setup that runs Obsidian headlessly on your server.

```
You (phone/laptop) → Obsidian Sync → Kasmidian vault on server
                                             ↓
                                        Agent reads files
```

Write your daily notes on your phone or laptop as normal. Obsidian Sync pushes them to the server. Kasmidian keeps the vault live on disk. The agent reads them the moment they arrive.

---

## What's in each file

| File | Delivery | Purpose |
|------|----------|---------|
| `SOUL.md` | Bootstrap (auto-loaded) | Personality, voice, communication style |
| `AGENTS.md` | Bootstrap (auto-loaded) | Operating manual, rules, file loading |
| `IDENTITY.md` | Bootstrap (auto-loaded) | Agent identity — name, emoji, purpose |
| `USER.md` | Bootstrap (auto-loaded) | Human context — name, timezone, priorities |
| `TOOLS.md` | Bootstrap (auto-loaded) | Local setup — journal paths, cron, devices |
| `MEMORY.md` | Bootstrap (auto-loaded) | Live state — mode, goals, commitments, patterns |
| `HEARTBEAT.md` | Bootstrap (auto-loaded) | Heartbeat check logic |
| `STRATEGIES.md` | Tool-read | Strategy menu by situation |
| `PREDICTIVE.md` | Tool-read | Pattern prediction from historical data |
| `PROACTIVE_OUTREACH.md` | Tool-read | When/how to reach out unprompted |
| `MEMORY_SCHEMA.md` | Tool-read | Memory systems, archival rules |
| `JOURNAL_READING.md` | Tool-read | How to parse journal entries |
| `CRON.md` | Tool-read | Cron job setup, prompts, probability logic |

**Bootstrap files** are auto-injected into every session — always in context. **Tool-read files** are loaded on demand by the agent via `read_file`, saving tokens on everyday calls.

---

Next: [Journal Guide →](guides/journal.md)
