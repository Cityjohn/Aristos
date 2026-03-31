# Coaching Loops — Overview

The Aristos coaching system is built on **loops** — repeating processes that observe, decide, act, and learn. Each loop has a specific purpose, runs at a specific cadence, and shares state with other loops.

## Why loops, not features

Features are static. Loops improve. A loop that tracks what works and adjusts itself becomes more effective over time. A feature that sends a morning check-in sends the same check-in forever.

The goal: build loops that get better at guiding John toward his goals through self-learning.

---

## The Loops

| # | Loop | Cadence | Purpose |
|---|---|---|---|
| 1 | [Daily Pulse](#1-daily-pulse) | Every 3-4 hours | Keep John engaged with his daily notes and goal schedule |
| 2 | [Goal Churn](#2-goal-churn) | Daily + weekly | Track measurable progress toward active goals |
| 3 | [Strategy Rotation](#3-strategy-rotation) | Per coaching interaction | Learn which coaching approaches work for John, rotate accordingly |
| 4 | [Pattern Detection](#4-pattern-detection) | Continuous (event-driven) | Identify avoidance, burnout, distraction before they stall progress |
| 5 | [Knowledge Application](#5-knowledge-application) | Weekly | Mine the knowledge base + vault-memory for coaching insights |
| 6 | [Weekly Synthesis](#6-weekly-synthesis) | Sunday evening | Big-picture review, goal alignment, strategy reset |

---

## How the loops connect

```
                    ┌──────────────────────────┐
                    │     John's Daily Life     │
                    │  (actions, decisions,     │
                    │   mood, energy, output)   │
                    └────────────┬─────────────┘
                                │
                    ┌───────────▼───────────────┐
                    │    Obsidian Daily Note     │
                    │  (the ONLY human input)    │
                    └───────────┬───────────────┘
                                │
            ┌───────────────────┼───────────────────┐
            │                   │                   │
    ┌───────▼──────┐   ┌───────▼──────┐   ┌───────▼──────┐
    │  Loop 1:     │   │  Loop 2:     │   │  Loop 4:     │
    │  Daily Pulse │   │  Goal Churn  │   │  Pattern     │
    │              │   │              │   │  Detection   │
    │  nudge John  │   │  measure     │   │  flag issues │
    │  to write    │   │  progress    │   │  early       │
    └──────┬───────┘   └──────┬───────┘   └──────┬───────┘
           │                  │                   │
           │          ┌───────▼──────┐            │
           │          │  Loop 3:     │◄───────────┘
           │          │  Strategy    │  pattern triggers
           │          │  Rotation    │  strategy change
           │          │              │
           │          │  learn what  │
           │          │  works       │
           │          └──────┬───────┘
           │                 │
           │         ┌───────▼──────┐
           │         │  Loop 5:     │
           │         │  Knowledge   │
           │         │  Application │
           │         │              │
           │         │  deep        │
           │         │  analysis    │
           │         └──────┬───────┘
           │                │
           └────────┬───────┘
                    │
            ┌───────▼──────┐
            │  Loop 6:     │
            │  Weekly      │
            │  Synthesis   │
            │              │
            │  everything  │
            │  converges   │
            └──────────────┘
```

## Shared State

All loops read and write to a single state file. No complex data architecture. One file.

→ See [shared-state.md](shared-state.md)

## Principles

1. **The daily note is the single source of human input.** Everything John communicates about his goals, progress, mood, and challenges flows through the Obsidian daily note. If it's not in the note, the loops don't know about it.

2. **Loops are independent but connected.** Each loop can run without the others. But they share state, so insights from one loop inform the others.

3. **Self-learning through outcomes.** Every coaching action logs whether it worked. Over time, the system learns what specific strategies work for John specifically — not generic advice, but personalized coaching.

4. **Simplicity over completeness.** Better to have 5 loops that actually run than 20 that sit unused. If a loop can't demonstrate value in a week, it should be cut.

5. **Measure what matters.** The only real output metric: is John making progress toward his goals? Everything else is process optimization.
