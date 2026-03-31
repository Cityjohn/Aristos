# Shared State — coaching-state.json

All loops read and write to a single file: `memory/coaching-state.json`

This replaces the current `session-state.json` which tracks almost nothing useful.

## Schema

```json
{
  "date": "2026-03-31",
  "lastActivity": "2026-03-31T13:30:00Z",
  "mode": "struggling",

  "goals": [
    {
      "id": "dominius-testing",
      "name": "Finish Dominius for testing",
      "deadline": "2026-03-31",
      "status": "active",
      "progress": 0.4,
      "lastProgressDate": "2026-03-30",
      "difficulty": "high",
      "blocks": ["burnout", "avoidance"]
    }
  ],

  "coaching": {
    "currentStrategy": "implementation-intentions",
    "lastStrategy": "humor-redirect",
    "strategyHistory": [
      {
        "strategy": "humor-redirect",
        "date": "2026-03-30",
        "context": "avoidance",
        "response": "engaged",
        "effective": true
      }
    ],
    "sentToday": [
      {"time": "08:00", "strategy": "casual-opener", "response": true},
      {"time": "12:35", "strategy": "implementation-intentions", "response": false}
    ],
    "randomSentToday": 1
  },

  "patterns": {
    "active": ["documentation-over-implementation", "weekend-avoidance"],
    "lastDetected": "2026-03-30",
    "detectionCount": {
      "documentation-over-implementation": 3,
      "weekend-avoidance": 2
    }
  },

  "signals": {
    "lastDailyNoteDate": "2026-03-30",
    "dailyNoteStreak": 2,
    "lastEndOfDayFilled": "2026-03-23",
    "journalGapDays": 0,
    "avgMood7d": null,
    "avgEnergy7d": null
  }
}
```

## Field Reference

### Top level

| Field | Type | Purpose |
|---|---|---|
| `date` | string | Current date |
| `lastActivity` | ISO timestamp | Last time John interacted — jobs skip if < 90 min ago |
| `mode` | string | Current coaching mode: returning / struggling / baseline / momentum |

### goals

Each goal has:

| Field | Type | Purpose |
|---|---|---|
| `id` | string | Unique identifier |
| `name` | string | Human-readable name |
| `deadline` | date string | Target date |
| `status` | string | active / completed / blocked / paused |
| `progress` | number 0-1 | Estimated completion (from daily notes) |
| `lastProgressDate` | date | Last time progress was reported |
| `difficulty` | string | low / medium / high (from daily notes or inference) |
| `blocks` | string[] | What's blocking this goal |

**Updated by:** Loop 2 (Goal Churn) reads daily notes and updates progress. Loop 6 (Weekly Synthesis) adds/removes goals.

### coaching

| Field | Type | Purpose |
|---|---|---|
| `currentStrategy` | string | Strategy being used this cycle |
| `lastStrategy` | string | Previous strategy |
| `strategyHistory` | array | Last 20 strategy outcomes |
| `sentToday` | array | Coaching messages sent today with response status |
| `randomSentToday` | number | Count of random engagement messages (cap: 3) |

**Updated by:** Loop 3 (Strategy Rotation) after each coaching interaction.

### patterns

| Field | Type | Purpose |
|---|---|---|
| `active` | string[] | Currently active patterns |
| `lastDetected` | date | Last pattern detection |
| `detectionCount` | map | How many times each pattern was detected |

**Updated by:** Loop 4 (Pattern Detection) when patterns are identified.

### signals

| Field | Type | Purpose |
|---|---|---|
| `lastDailyNoteDate` | date | Last daily note written |
| `dailyNoteStreak` | number | Consecutive days with notes |
| `lastEndOfDayFilled` | date | Last time end-of-day review was completed |
| `journalGapDays` | number | Days since last daily note |
| `avgMood7d` | number | Average mood over 7 days (null if < 3 entries) |
| `avgEnergy7d` | number | Average energy over 7 days (null if < 3 entries) |

**Updated by:** Loop 1 (Daily Pulse) checks if notes exist. Loop 6 (Weekly Synthesis) computes averages.

## What reads what

| Loop | Reads | Writes |
|---|---|---|
| 1. Daily Pulse | signals, coaching.sentToday | signals.lastDailyNoteDate, coaching.sentToday |
| 2. Goal Churn | goals, daily notes | goals.progress, goals.status |
| 3. Strategy Rotation | coaching, signals, patterns | coaching.currentStrategy, coaching.strategyHistory |
| 4. Pattern Detection | signals, goals, coaching | patterns.active, patterns.detectionCount |
| 5. Knowledge Application | vault-memory, all loops' state | (advisory — feeds into Loop 3 and 6) |
| 6. Weekly Synthesis | everything | goals, coaching, patterns, signals, mode |
