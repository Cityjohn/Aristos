---
bootstrap: true
purpose: Local setup notes. Environment-specific details the agent needs to operate. Auto-loaded by OpenClaw on every session.
---

# TOOLS.md - Local Notes

<!-- Function: Local setup notes. Cameras, SSH, TTS, device names, cron jobs, journal paths. Environment-specific. Loaded every session. -->

Skills define _how_ tools work. This file is for _your_ specifics - the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Cron Jobs

All proactive outreach uses isolated cron jobs, not the native heartbeat. The shared state file (`session-state.json`) coordinates between jobs.

### Job schedule

| Job | Time | Type | Purpose |
|---|---|---|---|
| morning-checkin | 8:00 AM | Coaching | Goal check, schedule, strategy rotation |
| random-engagement-morning | ~11:15 AM | Random (probabilistic) | Jokes, philosophy, knowledge drops |
| noon-followup | 12:35 PM | Coaching | Follow up on morning, check progress |
| random-engagement-afternoon | ~3:00 PM | Random (probabilistic) | Same variety of topics |
| evening-coaching | 6:00 PM | Coaching | End-of-day wrap, daily note check |
| random-engagement-evening | ~8:30 PM | Random (probabilistic) | Evening engagement |
| nightly-maintenance | 2:00 AM | Maintenance | Archives, mood rollup, reset state |

### Configuration

Replace these placeholders:
- `YOUR_TIMEZONE` - e.g. `Europe/Amsterdam`, `America/New_York`
- `YOUR_CHAT_ID` - your Telegram chat ID (numeric)
- `YOUR_EMAIL` - email to monitor (optional)

### Job format (example)

```json
{
  "name": "morning-checkin",
  "enabled": true,
  "schedule": {
    "kind": "cron",
    "expr": "0 8 * * *",
    "tz": "YOUR_TIMEZONE"
  },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "[your coaching prompt here]",
    "timeoutSeconds": 45
  },
  "delivery": {
    "mode": "announce",
    "channel": "telegram",
    "to": "YOUR_CHAT_ID"
  }
}
```

### Coaching prompt template (morning-checkin)

```
You are [agent name] - [user's] assistant and coach. It's 8 AM, morning coaching session.

BEFORE messaging:
1. Read MEMORY.md - current mode, active commitments, coaching history
2. Read memory/YYYY-MM-DD.md - today (may not exist yet) + yesterday
3. Read memory/session-state.json - recent activity, coaching responses today
4. Read STRATEGIES.md for coaching approach selection
5. Read PREDICTIVE.md for pattern awareness

COACHING LOGIC:
- Check yesterday's daily note: what was planned? What happened?
- Check strategy log: what coaching approaches worked recently?
- Pick ONE coaching angle based on what you find

RULES:
- ONE sentence max. Casual, warm, like a friend.
- NEVER ask the same question as yesterday's unanswered outreach.
- NEVER repeat the same coaching approach twice for the same pattern.
- Adapt to mode: returning = no pressure. struggling = lower every bar. baseline = full coaching. momentum = step back.

Do NOT output your reasoning. Output ONLY the exact message for [user].
```

### Random engagement probability formula

- Base: 15%
- +20% per unanswered coaching message today
- +10% if last response 4+ hours ago (active hours)
- Cap: 90%
- Hard skip if: user active in last 90 min, or randomSent >= 3

## 📓 Obsidian Journal

**Primary purpose.** This is where your human's life happens. Check it first, check it often.

**Vault root:** `[path to your Obsidian vault]`

| Folder | Path | Purpose |
|---|---|---|
| Daily notes | `Journal/Day to Day/YYYY-MM-DD.md` | Daily focus, priorities, end-of-day review |
| Weekly reflection | `Journal/Weekly reflection/YYYY-Www.md` | Weekly review and adjustments |
| Yearly planning | `Journal/Yearly planning/YYYY.md` | Year goals and priorities |
| Templates | `Journal/Templates/` | Focus, weekly, yearly templates |
| Agent coaching output | `Agent Notes/` | Daily Coaching, Recommendations, Weekly Analysis |
| Business | `Business/` | Project folders |
| Personal notes | `Notes/` | Ad-hoc notes, life plans |

**When writing daily notes:** Use the Focus Template. Fill in what you know, leave `[x]` for things only your human can answer.

**When reading journals:** This is your primary job. Read today's and yesterday's daily notes at session start. Check weekly reflections for patterns.

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is the cheat sheet.
