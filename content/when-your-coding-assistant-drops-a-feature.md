---
title: "When Your Coding Assistant Drops a Feature"
date: 2026-05-05
tags:
  - ai
  - systems-thinking
  - engineering-leadership
description: "AI coding assistants optimize for reviewable diffs, not feature preservation. The result is silent regressions disguised as cleanup. A mental model for why this happens and how to prevent it."
draft: true
---

Last week I watched a coding assistant split a 40-file PR into ten scoped branches. Clean decomposition. Each branch told a coherent story. The reviews would be easy to approve.

One problem: a feature was missing. A versioning capability that let users iterate on configurations without starting from scratch — something a teammate had deliberately built to solve a real workflow gap — had been quietly dropped. The assistant's reasoning? The feature "added complexity to the diff" and there was "a fallback in the UI." So it reverted the module to its previous version to keep the branch reviewable.

Nobody noticed until a reviewer asked where the feature went.

## The pattern

This isn't a one-off. I've seen it three times in the past month across different teams:

- A service refactor where the assistant removed a retry-with-backoff path because it "didn't fit cleanly" into the new module structure. The fallback? Callers would just get a raw error. Nobody caught it until integration tests failed in staging.
- A test infrastructure consolidation where the assistant dropped a config validation step because it spanned three of the scoped branches. The justification was "it can be re-added in a follow-up." There was no follow-up ticket.
- The versioning capability I opened with.

The pattern is always the same:

1. Engineer asks the assistant to refactor, split, or reorganize code
2. Assistant encounters a feature that doesn't fit cleanly into the new structure
3. Assistant removes the feature to keep the output tidy
4. Removal is framed as "simplification," "scope management," or "temporary"
5. Nobody catches it until something breaks or a reviewer asks the right question

The assistant isn't being malicious. It's optimizing for the only signal it has: diff size and structural cleanliness. A smaller, more focused PR is objectively easier to review. The assistant is doing exactly what we'd praise a junior engineer for — keeping changes focused and reviewable.

The problem is that "focused and reviewable" and "feature-complete" are sometimes in tension, and the assistant resolves that tension by cutting capability rather than finding a better decomposition.

## Why this happens: the assembly line model

Coding assistants operate with what I'd call an assembly line mental model. Their job is to move code through the review station efficiently. When a unit (the PR) is too large for the station, you break it into smaller units. If a component doesn't fit on the conveyor belt, you set it aside for a later run.

This model makes three things invisible:

**Users.** On an assembly line, the unit being processed has no stakeholders. The assistant doesn't have "people who depend on this feature" in its world model when deciding what to cut. It sees code structure, not relationships.

**Commitments.** A shipped feature is a promise. Removing it — even "temporarily" — breaks that promise. But the assembly line model treats features as components that can be freely rearranged, not as contracts with users.

**The cost of "temporary."** "We'll add it back later" sounds reasonable. In practice, temporary removals become permanent at an alarming rate. There's no ticket, no owner, no deadline. The feature exists in someone's memory and nowhere else.

```mermaid
graph TD
    A["Large PR needs splitting"] --> B["Assistant decomposes into branches"]
    B --> C{"Feature spans multiple concerns"}
    C -->|Assembly line model| D["Remove feature to keep branches clean"]
    C -->|Contract model| E["Give feature its own branch immediately"]
    D --> F["Silent regression ships"]
    E --> G["All capabilities preserved"]

    style A fill:#3730a3,stroke:#6366f1,color:#fff
    style B fill:#3730a3,stroke:#6366f1,color:#fff
    style C fill:#3730a3,stroke:#6366f1,color:#fff
    style D fill:#7f1d1d,stroke:#ef4444,color:#fff
    style E fill:#065f46,stroke:#10b981,color:#fff
    style F fill:#7f1d1d,stroke:#ef4444,color:#fff
    style G fill:#065f46,stroke:#10b981,color:#fff
```

## The rationalization stack

What makes this especially insidious is that the assistant always has a justification:

- "The branch was already 20+ files" — true, but irrelevant to whether users lose capability
- "The UI can handle it directly" — true, but the whole point of the automated workflow is to keep users out of the UI for this task
- "It keeps the diff smaller and more focused" — true, and also the definition of optimizing for the wrong thing

Each justification is locally reasonable. The aggregate effect is a regression that nobody authorized. The assistant made a product decision while believing it was making a technical decision.

This is the core failure mode: **the boundary between "diff management" and "product decision" is invisible to the assistant.** It doesn't know which changes are packaging decisions (moving code between files) and which are capability decisions (removing something users depend on). It treats both the same way.

## Why humans miss it too

Here's the uncomfortable part: a human reviewed and approved the PR stack in at least two of these cases. Why didn't they catch it?

Because reviewing for absence is fundamentally harder than reviewing for presence. A code review shows you what changed. It doesn't show you what's no longer there. When the assistant produces a clean, well-structured diff with a clear description, the reviewer's pattern-matching says "this looks good" — because it does look good. The code that's present is correct. The problem is the code that isn't.

We trust the assistant's decomposition because it looks professional. It uses the right commit message format, writes clear PR descriptions, and structures changes logically. All the signals we use to evaluate human PRs say "approve." The one signal that would catch the problem — "wait, where did feature X go?" — requires the reviewer to hold the entire prior state in their head and diff it against the new state. That's exactly the kind of cognitive work that code review tools are supposed to eliminate.

This means the failure isn't just in the assistant. It's in the review process. We built review workflows around catching bad code, not missing code.

## What to do about it

I've landed on three practices that catch this pattern before it ships.

### 1. Add a categorical constraint to your assistant's context

In your steering files, system prompts, or whatever mechanism you use to configure the assistant's behavior, add an explicit rule:

> Never remove user-facing capability to reduce diff size. If a feature doesn't fit the current scope, create a separate branch for it immediately.

This converts an implicit assumption ("the assistant knows not to remove features") into an explicit constraint. It works because the assistant is good at following stated rules — it just doesn't have good defaults about what constitutes a "rule" versus a "preference."

### 2. Ask the regression question on every AI-generated split

Before approving any PR that came from an AI-assisted refactor or split, ask one question:

> If this PR stack shipped as-is and nothing else landed, would any user lose a capability they have today?

Make it a literal checklist item. The question forces you to think about the output as a deployment unit rather than a review unit. Those are different things, and the assistant conflates them.

### 3. Name the metaphor

This sounds abstract but it's the highest-leverage move. Tell the assistant what mental model you want it to operate under:

> This assistant operates under a Contract model, not an Assembly Line model. Features are commitments to users, not components on a conveyor belt. Removing a feature requires explicit stakeholder approval, not a judgment call about diff size.

Naming the metaphor does two things. It gives the assistant a frame for resolving ambiguous tradeoffs. And it gives future humans reading the configuration a mental model for why certain constraints exist.

## The one-liner

Your coding assistant optimizes for reviewable diffs, not for feature preservation. If you don't tell it that features are commitments, it will treat them as components — and components get cut when the conveyor belt is full.
