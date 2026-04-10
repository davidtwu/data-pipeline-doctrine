---
title: "Structuring Agent Skills for Scale"
date: 2026-03-23
tags:
  - ai
  - architecture
description: "Progressive disclosure, token budgets, and when to split vs. merge agent skills."
---

You've got 50 skills across 5 teams. Half of them overlap. Your token budget is bleeding out before the conversation even starts.

Once you've nailed the [[agent-skill-description-formula|description formula]], the next challenge is structuring skills that compose without collision — and don't bankrupt your context window in the process.

## The Token Tax Is Real

At 500 tokens per tool definition and 20 tools, you spend 10,000 tokens before the conversation starts. OpenAI considers fewer than 100 tools as "in-distribution" — but practical performance degrades well before that.

This is why progressive disclosure matters. Claude's skill framework uses three levels: YAML frontmatter (always loaded for routing), the skill body (loaded when selected), and linked references (loaded as needed). This minimizes token consumption while maintaining specialized expertise.

Design your skill library assuming only 3-5 skills will be active per invocation, selected dynamically from the full catalog. Anthropic's Tool Search Tool reduced token usage by 85% and improved Opus 4 accuracy from 49% to 74% on large tool libraries.

## Instruction Body Principles

**Put critical instructions first.** LLMs exhibit primacy bias. Place safety constraints, required validations, and output format requirements in the opening lines.

**Be specific and actionable.** `Run python scripts/validate.py --input {filename}` outperforms "Validate the data before proceeding" because it eliminates interpretation variance.

**Include error handling with specific causes and solutions.** Rather than "handle errors gracefully," specify: "If the API returns 429, wait 30 seconds and retry up to 3 times. If the file exceeds 10MB, return an error suggesting the user split the file."

**Keep instruction bodies under 5,000 words.** Move detailed reference material into a `references/` directory loaded on demand.

## When to Split

- Multiple conditional branches based on a mode parameter
- Parameter count exceeds 8 (AWS's empirically-derived threshold)
- Different user intents are served
- Error handling becomes ambiguous

## When to Merge

- 3+ API calls are commonly chained in a single workflow
- Intermediate outputs consume tokens without adding decision value
- The consolidated skill maps to a single clear user intent

Instead of `list_users` + `list_events` + `create_event`, build `schedule_event` that handles the full workflow internally.

## Three Orchestration Patterns

**Sequential pipelines** (skill A → skill B) work for linear workflows.

**Fan-out/fan-in** (dispatch to multiple skills, aggregate results) works for parallel analysis.

**Supervisor/delegation** (a coordinator skill routes to specialists) works for complex, context-dependent workflows.

Google, AWS, Microsoft, and Anthropic all document these same three patterns independently — they represent fundamental architectural primitives.

The anti-pattern to avoid is the "God Skill" — a single skill that attempts to solve too many loosely related problems. Its instruction body becomes bloated and internally inconsistent, degrading reliability.

---

*This is part 2 of a series on agent skill engineering. Previous: [[agent-skill-description-formula|The Four-Part Description Formula]]. Next: [[agent-skill-evaluation|Evaluation-Driven Skill Development]]*
