---
title: Field notes on building AI
description: "Just for context"
date: "2025-10-19"
---

Experimenting with AI in the last year felt like a game of trade-offs. Vibe-coding demos looked like magic, but shipping a feature that felt reliable and not like a coin toss required getting my hands dirty with the architecture. Here's notes from my experiments with popular AI use cases I've often come across.

### What I learned, fast

*   **One-shotting optimisation: Prompting isn't a conversation.** My first prompt for a meeting summariser was 10 lines. The production prompt is over 400, with a dozen few-shot examples baked in just to keep a JSON format from breaking. It's less "prompting" and more "brute-force spec writing" until it passes [evaluations](https://mlflow.org/docs/latest/genai/eval-monitor/).

*   **Breaking contexts: It's more about being an agent architect.** An AI coach I made was one big call. It constantly hallucinated feedback. I had to break it into a [3-step chain](https://google.github.io/adk-docs/agents/workflow-agents/sequential-agents/#how-it-works): 1) Identify interview techniques from the transcript, 2) Score each technique against a rubric, 3) Synthesise the scores into feedback. This included an LLM-as-a-judge to keep failures low. It's slower, but the quality shot up because each step is a simpler task.

*   **Measuring trust: Dashboards look different.** I stopped caring about daily active users for an AI tooltip I launched. Now, I obsess over the uncorrected output rate i.e. the percentage of AI summaries our users *don't* have to manually edit. If that number is low, the feature is failing, even if people are clicking on it.

### Back to Basics

*   **Discovery first, always.** Many seem to testing waters with a generic summariser because it's an easy demo. Discovery would tell you the market is a graveyard. I found a niche helping an acquaintance who works in sales auto-draft follow-up emails from call transcripts instead. That came from customer interviews, not just playing with the API.

*   **Trust and safety can't be an afterthought.** I constantly asked myself, "How could this go wrong?" and built guardrails ASAP. Consent to user's data needs to be baked in. Similarly for anything important, building an 'off-ramp' for a human to approve or fix the agent's work must be a required feature, not a nice-to-have. Users might soon be asked to explicitly share their [data with LLMs for better experiences](https://onfabric.io/), but we can't leave responsibility for safety alone to the service provider or consumer.

What I really learned is that this new tech is amazing, but if you skip discovery, you're just making cool stuff nobody actually needs. Start by testing the riskiest assumption ("Can AI even do this?") and de-risk it step-by-step. Shipping and learning is the only way.
