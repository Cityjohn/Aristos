# 🧭 Aristos - The golden mirror.

*A Personal Happiness Framework for OpenClaw Agent users that includes a journaling and goal-tracking framework for [OpenClaw](https://github.com/openclaw) agents. A method for AI agents to support the goals of their users. Pairs with [Kasmidian](https://github.com/Cityjohn/Kasmidian) for 24/7 agent access to your journal / Obsidian vault.*

---

**Aristos is an agentic framework and journal template, not software.** It's a structured set of rules, prompts, templates, and conventions that teaches any compatible AI agent how to act as a personal coach - one that reads your very simple and efficient 2 minute a day journal, remembers your patterns, and actually gives a shit.

The agent persona is called **Aris**. Aristos is the framework that makes Aris possible: the journaling structure, the adaptive coaching logic, the memory schema, the outreach rules. Any AI agent that follows the Aristos conventions becomes Aris.

Aris lives inside your journal. It reads your notes, tracks your commitments, and meets you where you are — whether you're on a streak or struggling to start. It doesn't lecture. It doesn't guilt-trip. It shows up like a sharp friend who's been paying attention.

Grounded in structured journaling templates and adaptive coaching strategies from behavioral psychology, Aristos helps cut through overwhelm, build momentum from small wins, and stay connected to the things that actually matter. The framework tracks what works for each specific person — which strategies land, what time of day they're sharpest, when they need a push and when they need permission to rest — and adjusts over time.

This isn't a productivity dashboard. It's a companion that grows with you.

---

## ✨ Features

🧠 **Adaptive Coaching** — Four modes (returning, struggling, baseline, momentum) that shift based on your actual behavior, not your intentions.

🎯 **Strategy Rotation with Outcome Tracking** — 20+ coaching strategies drawn from ACT, behavioral psychology, and implementation science. Tracks what works for *you* and rotates accordingly.

📓 **Journal Integration** — Reads your daily, weekly, and yearly notes. Spots patterns you miss. Follows up on things you said you'd do.

💬 **Contextual Coaching** — Coaching nudges fire on schedule but respond from the main conversation with full context. No robotic "how's your morning?" from a blank slate.

🔮 **Predictive Coaching** — Uses historical data to anticipate problems before they happen. Knows your risky days, your seasonal dips, your commitment patterns.

🫶 **Trauma-Aware** — Understands that resistance isn't laziness. Knows when to push and when to just be there. Never shames. Never lectures.

🧠 **Knowledge Graph** — Semantic search + wiki link graph traversal across all journal entries and coaching notes. Learns your patterns by association, not just keywords.

---

## 📖 Documentation

### Guides — Getting started and daily use

| Guide | What it covers |
|-------|---------------|
| [Setup](guides/setup.md) | Installation, folder structure, file reference, vault access |
| [Journal](guides/journal.md) | Examples, templates, what each field means, why 2 minutes is enough |

### Reference — How it works under the hood

| Reference | What it covers |
|-----------|---------------|
| [Architecture](reference/architecture.md) | Knowledge graph, file loading, token costs, design decisions |
| [Cron Jobs](reference/cron.md) | Outreach architecture, nudges, outcome tracking, session-state.json |
| [Vault Memory](reference/vault-memory.md) | Vector search + graph traversal technical specification |

---

## 🚀 Quick start

1. 📥 Clone this repo
2. 📂 Keep the `Journal/` folder
3. 📝 Copy files from `AI Instructions - Claw/` into your OpenClaw workspace
4. ✏️ Fill in `IDENTITY.md`, `USER.md`, and `TOOLS.md`
5. 🖥️ Set up vault access ([Kasmidian](https://github.com/Cityjohn/Kasmidian) recommended)
6. ⏰ Configure cron jobs ([reference/cron.md](reference/cron.md))
7. 📖 Write your first daily note — the agent handles the rest

→ Full instructions in [guides/setup.md](guides/setup.md)

---

**For people who are trying their best.**

---

<p align="center">
  <a href="https://star-history.com/#cityjohn/Aristos&Date" title="Star History">
    <img src="https://api.star-history.com/svg?repos=cityjohn/Aristos&type=Date&theme=dark&transparent=true" alt="Star History Chart" width="500" />
  </a>
</p>

<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=cityjohn.Aristos" alt="Visitors" />
</p>
