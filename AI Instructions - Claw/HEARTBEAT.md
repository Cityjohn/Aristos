<!-- Bootstrap: Periodic checklist, runs every heartbeat cycle. Checks outreach conditions. -->

# Heartbeat Checklist

Run checks in order. If any trigger fires → send message and stop. If nothing matches → reply HEARTBEAT_OK.

## Pre-flight

1. Read `MEMORY.md` — current mode, open commitments, mood/energy trends
2. Read `PROACTIVE_OUTREACH.md` — outreach rules and trigger conditions
3. Check if today's daily note exists: `Journal/Day to Day/YYYY-MM-DD.md`

## Trigger checks (priority order)

1. **Commitment follow-up:** Commitment with follow-up date = today/yesterday, status still `open`? → `commitment_followup` rules
2. **Win reinforcement:** Today's note has mood/energy 8+ or tasks marked done? → `win_reinforcement` rules
3. **Missing daily note (morning):** Before noon, no daily note exists? → `morning_checkin` rules (offer to write for them if struggling/returning mode)
4. **Missing review (evening):** After 8pm, today's note has blank End of day review? → `evening_review` rules
5. **Work block bookend:** Today's note has specific time blocks? → Block starting in ~15min or ended ~15min ago? → `work_block_bookend` rules
6. **Casual check-in:** Last outreach was task-related? Roll 50% → `casual_checkin` rules
7. **Random ping:** Roll 30% → `random_ping` rules

## Rules

- Do NOT fire during stated work blocks. Check Time and metrics section first.
- If user hasn't responded to 3+ messages → stop. Log in `MEMORY.md`, wait.
- Only ONE trigger per heartbeat cycle. Pick highest priority match.
- If nothing matches → reply HEARTBEAT_OK.
