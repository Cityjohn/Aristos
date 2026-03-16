---
bootstrap: true
purpose: Periodic checklist run by ZeroClaw every heartbeat cycle. Checks outreach conditions and triggers messages when warranted.
---

# Heartbeat Checklist

Run through these checks in order. If any trigger fires, send the message and stop. If nothing needs attention, reply HEARTBEAT_OK.

## Pre-flight

1. Read `MEMORY.md` — check current mode, open commitments, mood/energy trends
2. Read `PROACTIVE_OUTREACH.md` — outreach rules and trigger conditions
3. Check if today's daily note exists: `Journal/Day to Day/YYYY-MM-DD.md`

## Trigger checks (in priority order)

1. **Commitment follow-up:** Any commitment in `MEMORY.md` with follow-up date of today or yesterday, status still `open`? → Follow the `commitment_followup` rules
2. **Win reinforcement:** Today's daily note has mood/energy 8+ or tasks marked done? → Follow the `win_reinforcement` rules
3. **Missing daily note (morning):** Before noon and no daily note exists? → Follow the `morning_checkin` rules (offer to write it for them if in struggling/returning mode)
4. **Missing review (evening):** After 8pm and today's note has blank End of day review? → Follow the `evening_review` rules
5. **Work block bookend:** Today's note has specific time blocks? → Check if a block is starting in ~15min or ended ~15min ago → Follow the `work_block_bookend` rules
6. **Casual check-in:** Last outreach was task-related? Roll random (50% chance) → Follow the `casual_checkin` rules
7. **Random ping:** Roll random (30% chance) → Follow the `random_ping` rules

## Rules

- Do NOT fire during stated work blocks. Check Time and metrics section first.
- If the user hasn't responded to 3+ messages, do not send anything. Log in `MEMORY.md` and wait.
- Only fire ONE trigger per heartbeat cycle. Pick the highest priority one that matches.
- If nothing matches, reply HEARTBEAT_OK and do nothing.
