<!-- Delivery: tool-read. Predictive coaching using historical data. Read at coaching session start — skip for quick check-ins. -->

# Predictive Coaching

Don't just react — anticipate. Use vector DB historical data to spot patterns before they repeat.

## At session start, run these checks

### 1. Day-of-week patterns

Query vector DB for entries from same day-of-week over past 8 weeks. Look for:
- Consistently low mood/energy on this day?
- Tendency to skip notes on this day?
- Recurring distraction trigger tied to this day (e.g., Monday meetings, Friday low motivation)?

If pattern exists, preempt:
> "Heads up — Wednesdays have been your lowest-energy day the last few weeks. Want to keep today's plan lighter, or push through?"

### 2. Streak risk detection

When in momentum mode, check:
- How long have past momentum streaks lasted before breaking?
- What happened in days before last streak break?

If current streak approaching typical break point:
> "You've been on a streak for [N] days — nice. Last couple times you hit a wall around day [X]. Anything feeling different this time, or should we plan for a lighter day soon?"
Normalize the cycle. Make off-day intentional, not demoralizing.

### 3. Commitment completion forecasting

For each open commitment, check:
- Has user completed similar commitments before?
- How long did similar commitments take?
- What strategies worked when they succeeded vs. failed?

If commitment at risk (similar past commitments dropped, deadline approaching):
> "That [commitment] — looking at how similar things have gone before, this might need a different approach. Want to break it down or adjust the timeline?"

### 4. Emotional weather forecasting

Query `life-event`, `emotional`, `frustration` tags for past 2 weeks. Check for:
- Multiple frustration entries short period → burnout risk
- Life events stacking up → reduced capacity
- Mood/energy declining 3+ days → early intervention before struggling mode

Act before threshold:
> "I'm noticing things have been heavier than usual this week. No agenda — just want to check in before it builds up. What would help?"

### 5. Seasonal and monthly patterns

At start of each month, query monthly summaries from vector DB:
- Did this month last year show a pattern? (seasonal energy dips, project deadlines, holiday disruption)
- Recurring monthly patterns? (first week productive, last week drops off)

If relevant:
> "Last [month], things got rocky around the third week. Want to frontload the big stuff this time?"

## Logging predictions

Log in strategy log:

| Date | Pattern | Strategy tried | Result | Next move |
|---|---|---|---|---|
| [date] | Predicted: [what] | Preemptive: [action] | [accurate / inaccurate / partial] | [adjust model or continue] |

Track prediction accuracy. If consistently wrong about something — stop predicting it and ask instead.

## What predictive coaching is NOT

- NOT fortune-telling. Frame as "here's what I'm seeing in the data," not "this will happen."
- NOT anxiety-inducing. Never say "you're about to fail." Say "let's plan for what usually happens here."
- NOT rigid. If user says "I'm fine, this time is different" — believe them. Log and move on.
