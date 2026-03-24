---
title: "The Four-Part Description Formula for Agent Skills"
date: 2026-03-23
tags:
  - ai
  - til
description: "Tool descriptions are the most important factor in agent skill performance. Here's the formula that works."
---

The single highest-leverage investment in agent skill quality is the description field.

Anthropic's engineering team found that tool descriptions are "by far the most important factor in tool performance." Claude achieved state-of-the-art SWE-bench scores through description refinements alone — not model changes or prompt tuning.

Most teams underestimate what the description must accomplish: it tells the LLM both *what* the skill does and *when* to activate it. Production experience reveals a fourth element that's equally critical — when NOT to use it.

## The Formula

```yaml
description: >
  Generates developer handoff documentation from Figma design files.
  Use when user uploads .fig files, asks for "design specs", "component 
  documentation", or "design-to-code handoff". Do NOT use for general 
  image editing, wireframing, or non-Figma design tools. Outputs 
  structured markdown with component hierarchy, spacing tokens, and 
  color variables.
```

Four distinct signals:

1. **Core capability** — what it does (generates handoff docs)
2. **Positive triggers** — when to use it ("design specs", "component documentation")
3. **Negative boundaries** — when NOT to use it (not for wireframing)
4. **Output characterization** — what it returns (structured markdown)

## Precision vs. Recall

**Undertriggering** happens when descriptions lack the vocabulary users actually employ. Fix: add keyword variants and colloquial trigger phrases.

**Overtriggering** happens when descriptions are too broad or overlap with other skills. Fix: add explicit negative boundaries.

Composio documented a 10× reduction in tool failures after systematically improving descriptions across their 250+ integration platform. Most gains came from adding constraints that were previously implicit.

## Quick Standards

- 2-5 sentences, under 1024 characters
- Lead with capability, then triggers, then boundaries, then output
- Include exact phrases users say, not just technical terminology
- If two skills could match the same request, add mutual exclusion language

Debugging tip from Anthropic: ask Claude "When would you use the [skill name] skill?" It will quote the description back, revealing exactly which signals it latches onto.

---

*This is part 1 of a series on agent skill engineering. Next: [[agent-skill-architecture|Structuring Agent Skills for Scale]]*
