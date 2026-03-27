# ⏰ Cron Reference

All proactive outreach uses isolated cron jobs — not the native heartbeat.

---

## Architecture

```
┌─────────────────────────────────────────────────┐
│                  Cron Jobs                       │
│                                                  │
│  🌅 8:00 AM   morning coaching check-in         │
│  🎲 11:15 AM  random engagement (probabilistic) │
│  ☀️ 12:35 PM  noon follow-up                    │
│  🎲 3:00 PM   random engagement (probabilistic) │
│  🌙 6:00 PM   evening coaching wrap-up           │
│  🎲 8:30 PM   random engagement (probabilistic) │
│  📋 9:00 PM   evening review (daily note check) │
│  📅 Wed 10 AM  midweek check                    │
│  📝 Sun 6 PM   weekly reflection                │
│  🔧 2:00 AM   nightly maintenance               │
│  📧 every 30m  email check                      │
│                                                  │
│  Each job reads session-state.json for context   │
│  Each job writes back to session-state.json      │
└─────────────────────────────────────────────────┘
```

## How it works

- **Isolated sessions** — each cron runs independently, never blocks the main chat
- **session-state.json** — shared state file tracks `lastActivity`, coaching sent/responses, random count
- **Activity awareness** — random crons check `lastActivity` timestamp; skip if user was active in last 90 minutes
- **Adaptive probability** — random engagement starts at 15% and climbs based on unanswered coaching messages and silence duration. See `CRON.md` for the full formula.
- **Self-cleaning** — nightly maintenance archives old data, rolls up mood/energy, enforces memory limits

## Two vibes

The user typically has **two sides**: a playful/joking side AND a serious philosophical side. Outreach should reflect both:

- **Playful:** Absurd observations, weird facts, humor
- **Philosophical:** Markets, innovation, human psychology, societal critique, evolutionary behavior, deep abstract concepts

## session-state.json

```json
{
  "date": "YYYY-MM-DD",
  "lastActivity": null,
  "coachingSent": [],
  "coachingResponses": [],
  "randomSent": 0
}
```

Reset by nightly maintenance each night.

## Setup

1. Replace placeholders in `CRON.md` (timezone, chat ID, agent name, user name)
2. Copy the job JSON format from `CRON.md` and create each job
3. Create `session-state.json` in your workspace root

Full job definitions, prompts, and probability logic: see `AI Instructions - Claw/CRON.md`.

---

Back to [Architecture](reference/architecture.md) · [Vault Memory →](reference/vault-memory.md)
