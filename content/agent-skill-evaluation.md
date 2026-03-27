---
title: "Evaluation-Driven Skill Development"
date: 2026-03-23
tags:
  - ai
  - architecture
description: "How to measure skill quality, avoid silent failures, and let evaluation data drive design."
---

The most dangerous failure modes in agent skill design are silent — they produce plausible-looking but wrong outputs rather than errors. This is where [[agent-skill-description-formula|good descriptions]] and [[agent-skill-architecture|clean architecture]] meet rigorous measurement.

## Seven Anti-Patterns That Silently Degrade Performance

1. **The vague description** ("Helps with projects") — provides no trigger signal
2. **Missing negative examples** — causes persistent false positives
3. **Instruction bloat** — edge cases balloon context cost
4. **Implicit dependencies** — fragile chains between skills
5. **The API wrapper** — exposing every REST endpoint without considering agent affordances
6. **Overlapping descriptions** — forces impossible disambiguation
7. **Silent versioning breakage** — description changes cascade as hallucinations

## Building an Evaluation Flywheel

Anthropic's evaluation-driven development produced measurable improvements in their production MCP servers. Claude-optimized tools outperformed human-written expert implementations. Here's how to build the same flywheel.

Start by mining your logs for real failures. The best evaluation tasks require multi-step tool use and realistic complexity: "Customer ID 9182 reported triple charges; find all relevant log entries and determine if other customers were affected." Avoid tasks that are too specific — "Search the payment logs for purchase_complete and customer_id=9182" doesn't test tool selection at all.

Track five metrics religiously: tool selection accuracy (right skill chosen?), parameter accuracy (correct arguments?), task completion rate (end-to-end success), token consumption (efficiency), and error rate (reliability). These five together give you complete coverage.

Here's the counterintuitive part: feed your failure transcripts back to the agent itself. Let it analyze its own mistakes — ambiguous descriptions, missing parameter constraints, unnecessary tool calls — and propose specific improvements. This consistently outperforms manual optimization by human engineers.

Finally, validate every improvement on held-out test sets. Examples the agent hasn't seen during optimization. This prevents overfitting and reveals generalizable patterns that humans miss.

## Minimum Evaluation Coverage

For org-wide governance, mandate minimum coverage before any skill is published:

- 10 positive trigger cases (should activate)
- 10 negative trigger cases (should not activate)
- 5 end-to-end task completion scenarios

Track metrics over time with dashboards to catch regression early — before silent breakage reaches production.

## The Takeaway

The organizations getting the best results — Anthropic, Amazon, Composio — all converged on the same insight: let evaluation data drive skill design, not intuition. Build the flywheel, feed it real failures, and let it compound.

---

*This is part 3 of a series on agent skill engineering. See also: [[agent-skill-description-formula|The Four-Part Description Formula]] and [[agent-skill-architecture|Structuring Agent Skills for Scale]]*
