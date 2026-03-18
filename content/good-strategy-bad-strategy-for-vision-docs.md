---
title: "Good Strategy, Bad Strategy for Vision Documents"
date: 2026-03-17
tags:
  - architecture
  - systems-thinking
  - career
description: "Applying Richard Rumelt's strategy kernel to engineering vision documents — how to spot fluff, face real challenges, and write strategies that actually guide decisions."
draft: false
---

Most engineering vision documents are bad strategy dressed up in technical language.

I've read hundreds of them over the years — platform visions, architecture roadmaps, team charters. The pattern is depressingly consistent: ambitious goals, vague principles, and a conspicuous absence of anything that would help someone make an actual decision.

Richard Rumelt's book *Good Strategy Bad Strategy* gave me a framework for understanding why. His "kernel" of good strategy applies directly to how we write (and evaluate) technical vision documents.

## The kernel of good strategy

Rumelt argues that good strategy has three essential elements:

1. **Diagnosis** — A clear-eyed assessment of the challenge. What's actually the problem? What obstacles stand in the way?

2. **Guiding policy** — An overall approach for dealing with the challenge. Not a list of actions, but the logic that constrains and directs action.

3. **Coherent actions** — Specific, coordinated steps that implement the guiding policy.

```mermaid
graph LR
    A[Diagnosis] --> B[Guiding Policy]
    B --> C[Coherent Actions]
    C --> D[Outcomes]
    
    style A fill:#e1f5fe
    style B fill:#fff3e0
    style C fill:#e8f5e9
```

The kernel is deceptively simple. Most strategy documents skip the diagnosis entirely, mistake goals for guiding policy, and list actions that don't cohere.

## The four hallmarks of bad strategy

Rumelt identifies four warning signs. I see all of them in engineering vision documents:

### 1. Fluff

Fluff is gibberish masquerading as insight. It uses inflated language to create the illusion of strategic thinking.

Bad:
> "We will leverage our unified data platform to enable seamless cross-functional collaboration and drive transformational business outcomes through data-driven decision making."

This says nothing. What's the actual problem? What decisions does this guide? Strip away the buzzwords and there's no substance underneath.

Good:
> "Our data platform has three separate query engines with incompatible schemas. Teams spend 40% of their time reconciling data across systems. We need a single source of truth."

The good version names a specific problem with a measurable impact. You can argue with it, refine it, or disagree — but you can't ignore it.

### 2. Failure to face the challenge

Bad strategy avoids naming the hard problem. It describes a desired future state without acknowledging what makes getting there difficult.

Bad:
> "Our vision is to become the industry-leading real-time analytics platform."

This is an aspiration, not a strategy. What's stopping you from being industry-leading today? What specific obstacles need to be overcome?

Good:
> "Our batch processing architecture can't support sub-second query latency. Migrating to streaming would require rewriting our entire ingestion layer and retraining the team on new tooling. We need to find a path that delivers real-time capabilities without a multi-year rewrite."

The good version names the actual constraint: architectural debt and team skills. Now you can evaluate whether proposed solutions actually address these obstacles.

### 3. Mistaking goals for strategy

This is the most common failure mode. The document lists ambitious objectives but provides no approach for achieving them.

Bad:
> "Strategic priorities:
> - Achieve 99.99% uptime
> - Reduce query latency by 50%
> - Support 10x data volume growth
> - Improve developer productivity"

These are goals, not strategy. They don't tell you *how* to achieve them or *which* to prioritize when they conflict. (And they will conflict — 99.99% uptime often trades off against developer velocity.)

Good:
> "We will prioritize reliability over new features for the next two quarters. This means: no new data sources until we've eliminated the top 5 causes of pipeline failures, mandatory chaos testing before any production deployment, and a dedicated on-call rotation instead of the current ad-hoc coverage."

The good version makes a choice (reliability over features) and specifies actions that follow from that choice. Someone reading this knows what to do when faced with a trade-off.

### 4. Bad strategic objectives

Bad objectives are either too vague to act on or just as hard to achieve as the original problem.

Bad:
> "Objective: Build a world-class data infrastructure."

What does "world-class" mean? How would you know if you achieved it? This objective provides no guidance.

Also bad:
> "Objective: Migrate all workloads to the new platform by Q4."

This might be specific, but if migrating all workloads is just as hard as the original challenge, you haven't added any strategic value. You've just restated the problem as a deadline.

Good:
> "Objective: Migrate the three highest-volume pipelines (representing 80% of compute cost) to the new platform by Q4. Remaining workloads migrate opportunistically as teams have capacity."

The good version identifies a proximate objective — something achievable that creates momentum. It applies the 80/20 principle and acknowledges that not everything needs to happen at once.

## Applying the kernel to your vision doc

When writing or reviewing a vision document, I now ask three questions:

**Does it diagnose the actual challenge?**

Not the symptoms, not the desired end state — the underlying obstacle. If you can't articulate what makes this problem hard, you don't understand it well enough to strategize about it.

**Does the guiding policy make a choice?**

Strategy is about focus. A guiding policy that tries to optimize everything optimizes nothing. Look for explicit trade-offs: "We will prioritize X over Y." If there's no trade-off, there's no strategy.

**Do the actions cohere?**

Each action should reinforce the others. If your actions could be shuffled randomly without changing the strategy, they're just a to-do list. Coherent actions create a system where the whole is greater than the sum of parts.

## A template that works

Here's the structure I now use for vision documents:

```markdown
## Diagnosis

[2-3 paragraphs naming the specific challenge, its root causes, 
and why it's hard. Include data where possible.]

## Guiding Policy

[1-2 paragraphs describing the overall approach. 
State explicit trade-offs. This should be memorable enough 
that someone could recite it from memory.]

## Coherent Actions

[Numbered list of 3-7 specific actions that implement 
the guiding policy. Each action should clearly connect 
to the diagnosis and policy.]

## What This Means Day-to-Day

[Concrete examples of decisions this strategy guides. 
"When faced with X, we will choose Y because Z."]
```

The last section is my addition to Rumelt's kernel. Vision documents often fail because they're too abstract to guide daily decisions. By including explicit examples, you test whether your strategy actually has teeth.

## The one-liner

A vision document without a diagnosis is just wishful thinking. Name the hard problem, make a real choice about how to address it, and specify actions that cohere — that's the kernel of good strategy.

---

*Rumelt's book is worth reading in full. The examples from business strategy translate surprisingly well to technical leadership. [Good Strategy Bad Strategy](https://www.amazon.com/Good-Strategy-Bad-Difference-Matters/dp/0307886239) — highly recommended.*
