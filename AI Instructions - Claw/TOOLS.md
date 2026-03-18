---
bootstrap: true
purpose: Local setup notes. Environment-specific details the agent needs to operate. Auto-loaded by OpenClaw on every session.
---

# TOOLS.md - Local Notes

<!-- Function: Local setup notes. Cameras, SSH, TTS, device names, cron jobs, journal paths. Environment-specific. Loaded every session. -->

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

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

Document your cron job schedule here so it can be recreated:

<!-- Example format:
| Job | Time | Purpose |
|---|---|---|
| morning-checkin | 8:00 AM | Daily coaching check-in |
| email-check | Every 30 min | Monitor inbox for important messages |
-->

- [Add your cron jobs here]

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
