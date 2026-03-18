---
bootstrap: true
purpose: Local setup notes. Environment-specific details the agent needs to operate. Auto-loaded by OpenClaw on every session.
---

# TOOLS.md - Local Notes

<!-- Function: Local setup notes. Cameras, SSH, TTS, device names, cron jobs. Environment-specific. Loaded every session. -->

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Cron Jobs

Document your cron job schedule here so it can be recreated:

<!-- Example format:
| Job | Time | Purpose |
|---|---|---|
| morning-checkin | 8:00 AM | Daily coaching check-in |
| email-check | Every 30 min | Monitor inbox for important messages |
-->

- [Add your cron jobs here]

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

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps the agent do its job. This is the cheat sheet.
