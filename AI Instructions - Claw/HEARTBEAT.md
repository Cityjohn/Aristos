---
bootstrap: true
purpose: Deprecated — heartbeat-based outreach replaced by cron system.
---

# HEARTBEAT.md — Deprecated

**This file is no longer used.** Native heartbeat-based outreach has been replaced by the cron-based system described in `AGENTS.md`.

## Why?

Native heartbeats fire into the **main session**, blocking user conversations. Cron jobs run in **isolated sessions** and never interfere with chatting.

## Migration

If you're setting up Aristos for the first time, ignore this file. Follow the cron setup in `AGENTS.md` instead.

If you're migrating from the old heartbeat system:
1. Set up the coaching crons, random engagement crons, and nightly maintenance (see `AGENTS.md`)
2. Disable or remove any existing heartbeat configuration
3. Delete this file from your workspace (it's only here for backward compatibility)

## What the heartbeat used to do (now handled by crons)

| Old heartbeat task | Now handled by |
|---|---|
| Morning check-in | `morning-checkin` cron (8 AM) |
| Midday nudge | `noon-followup` cron (12:35 PM) |
| Evening review | `evening-coaching` cron (6 PM) |
| Random social pings | `random-engagement-*` crons (3/day, probabilistic) |
| Journal completion check | `nightly-maintenance` cron (2 AM) |
| Commitment follow-up | Coaching crons (built into prompts) |
