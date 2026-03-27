# ⏰ Cron Reference

All proactive outreach uses isolated cron jobs and coaching nudges to the main session.

---

## Architecture: Coaching nudges vs isolated sessions

Coaching nudges trigger the **main session** — with full conversation context. Isolated jobs handle random engagement, maintenance, and reflection.

```
Coaching nudges (contextual):
  Cron fires -> Trigger sent to main session -> Agent responds WITH full context

Isolated jobs (background):
  Cron fires -> Separate session -> Reads files -> Sends message
```

---

## 📋 Job schedule

| Job | Time | Type | How it works |
|---|---|---|---|
| `morning-checkin` | 8:00 AM | Coaching nudge | Sends `[coaching-nudge:morning]` to main session |
| `random-engagement-morning` | 11:15 AM | Random | Isolated, probability-based, checks activity |
| `noon-followup` | 12:35 PM | Coaching nudge | Sends `[coaching-nudge:noon]` to main session |
| `random-engagement-afternoon` | 3:00 PM | Random | Isolated, probability-based, checks activity |
| `evening-review` | 9:00 PM | Coaching nudge | Sends `[coaching-nudge:evening]` to main session |
| `random-engagement-evening` | 8:30 PM | Random | Isolated, probability-based, checks activity |
| `midweek-check` | Wed 10 AM | Coaching nudge | Sends `[coaching-nudge:midweek]` to main session |
| `weekly-reflection` | Sun 6 PM | Isolated | Reads weekly notes, writes analysis |
| `nightly-maintenance` | 2:00 AM | Isolated | Archives, cleans, updates patterns |
| `email-check` | Every 3h | Isolated | Checks for new emails |

---

## How nudges work

When the main session receives a coaching nudge, the agent:
1. Checks `session-state.json` for `recentTopics`, `tone`, `activeCommitment`
2. References what was being discussed
3. Responds as a natural check-in, not a scheduled message
4. Updates `coachingSent` timestamp

**Examples:**
- After a coding session: "You've been grinding on that Astro site for hours. Still in the zone or time for a break?"
- After frustration: "That CMS hunt was rough. Did you land on anything or still circling?"
- After silence: "Quiet day. Everything okay, or just heads-down on something?"

---

## 🧠 Coaching memory

Outcome tracking creates a feedback loop: coach, log, analyze, adapt, coach better.

### Outcome tracking

After each coaching nudge, the agent logs the outcome in `strategyOutcomes`:

| Field | Meaning |
|---|---|
| `strategy` | Which strategy was used |
| `context` | What pattern it was applied to |
| `response` | engaged / no-response / deflected |
| `effective` | Did it lead to action within 24h? |

### How it improves

**Nightly review:** Aggregate outcomes by strategy. Flag ineffective ones. Recommend rotation.

**Real-time adaptation:** Before coaching, check recent outcomes. Skip strategies that failed 2+ times. Prioritize ones that work.

**The loop:**
Coach with strategy -> Log outcome -> Nightly analysis -> Update rotation -> Coach with better strategy -> Repeat forever

Over weeks, the agent builds a personalized coaching playbook. What works for one person (humor, directness) might fail for another. The framework discovers this automatically.

### Coaching log in Aris Coaching/

Outcome summaries live in the vault, not just in session-state.json:

```markdown
# Strategy outcomes - March 2026
- implementation-intentions: 4/5 effective on avoidance patterns
- humor-redirect: 3/4 effective on distraction
- socratic-questioning: 0/4 - avoid for this person
```

These are indexed in SQLite. When the agent searches for coaching context, it finds strategy outcomes alongside journal entries and pattern notes.

---

## The session-state.json bridge

Shared state between cron jobs and main session:

| Field | Purpose |
|---|---|
| `lastActivity` | When user was last active — jobs skip if within 90 minutes |
| `coachingSent` | Timestamps of coaching nudges sent today |
| `coachingResponses` | Whether user responded to coaching nudges |
| `randomSent` | Count of random engagement messages today (cap: 3) |
| `recentTopics` | Last 3-5 conversation topics — coaching references these |
| `tone` | Current conversation tone: chatty / neutral / heavy |
| `topicShifts` | Number of topic changes this session (avoidance signal) |
| `activeCommitment` | What the user said they'd work on |
| `lastCommitmentMention` | When they last referenced it (focus drift detection) |
| `strategyOutcomes` | Which coaching strategies worked/failed |

### Initial file

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

---

## Two vibes

The user typically has **two sides**: a playful/joking side AND a serious philosophical side. Outreach should reflect both:

- **Playful:** Absurd observations, weird facts, humor
- **Philosophical:** Markets, innovation, human psychology, societal critique, evolutionary behavior, deep abstract concepts

---

## Setup

1. Replace placeholders in `CRON.md` (timezone, chat ID, agent name, user name)
2. Copy the job JSON format from `CRON.md` and create each job
3. Create `session-state.json` in your workspace root

Full job definitions, prompts, and probability logic: see `AI Instructions - Claw/CRON.md`.

---

Back to [Architecture](architecture.md) · [Vault Memory →](vault-memory.md)
