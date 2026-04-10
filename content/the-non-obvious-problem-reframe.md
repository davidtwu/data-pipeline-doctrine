---
title: "The Non-Obvious Problem Reframe"
date: 2026-03-19
tags:
  - architecture
  - systems-thinking
  - ai
description: "The highest-leverage moment in any project is before the first line of code. A good reframe changes the solution space, not just the solution — and sometimes you need someone else to see it."
draft: false
---

I almost missed the most important insight on a project last year. Not because I wasn't paying attention — because I was paying attention to the wrong things.

Business had flagged that metrics didn't match. Finance reported one number for monthly active users, Product reported another, and Engineering's dashboards showed a third. Leadership was asking questions. The kind of questions that come with an implicit "fix this."

My first instinct was to hunt for bugs. Somewhere in our pipelines, something was being calculated wrong. Find the bad join, fix the filter logic, close the ticket. That's how I'd solved data problems for years.

A coworker saw it differently. "The metrics aren't wrong," she said. "They're just not the same metric. Each team built their own aggregation from raw events, with their own filters and their own definitions of 'active.' We don't have a bug — we have three sources of truth."

That reframe changed the project. We weren't debugging pipelines. We were building a semantic layer.

## Why I missed it

I was deep in the infrastructure — job latencies, failure rates, data freshness. The pipelines were healthy by every measure I was watching. It took someone looking at the *outputs* — not the machinery — to see that the problem wasn't execution. It was architecture.

## What makes a good reframe

Watching my coworker nail this taught me what a useful reframe actually looks like:

**It's not visible from inside the problem.** The insight comes from stepping outside the immediate context — seeing the system from a different angle, questioning assumptions that everyone else treats as fixed. If you're heads-down in the pipelines, you see pipeline problems. The reframe required looking at how the data was *used*, not how it was *produced*.

**It changes what you'd build.** A reframe that leads to the same solution isn't a reframe — it's just a different description. The "implementation bug" framing would have led to audits and patches. The "semantic layer" framing led to a unified metrics platform. Structurally different solutions.

The classic pattern is a category shift:

- "This isn't a latency problem, it's a cache invalidation problem."
- "This isn't a scaling problem, it's a coordination problem."
- "This isn't a data quality problem, it's a semantic layer problem."

Each of these shifts the solution space. You're no longer optimizing within the original frame — you're solving a different (and often simpler) problem.

## How to find reframes

I've started being more deliberate about frame-hunting before projects kick off. The process:

**Question the constraints.** What assumptions is everyone making? Which constraints are actually fixed, and which are just habits? In our case, everyone assumed the metrics *should* match — that was the constraint nobody questioned. But maybe three teams having three definitions wasn't a bug. Maybe it was a symptom of missing infrastructure.

**Look for hidden feedback loops.** Most complex system problems are actually feedback loop problems in disguise. Where is information not flowing that should be? In our case, teams had no visibility into how other teams defined the same concepts. They weren't misaligned on purpose — they just couldn't see each other.

**Find the adjacent solved problem.** What domain has already solved a structurally similar problem? The "semantic layer" concept wasn't new — tools like dbt and Looker's modeling layer exist precisely because this problem is universal. My coworker recognized the pattern because she'd seen it solved elsewhere.

**Step back from the machinery.** If you're deep in implementation details, force yourself to look at outcomes. What are users actually experiencing? What are stakeholders actually asking for? The answer often reveals a different problem than the one you're solving.

## Using AI to accelerate reframing

This is where LLMs become genuinely useful — not for generating code, but for generating frames.

I've started using a simple prompt pattern before project kickoffs:

```
I'm about to start a project to [problem statement]. 

The obvious approach is [what everyone assumes we'll do].

Help me stress-test this framing:
1. What assumptions am I making that might be wrong?
2. What adjacent domains have solved similar problems?
3. What category shifts might reveal a simpler solution?
4. What feedback loops or incentive misalignments might be hiding?
```

The AI won't give you the answer — but it will give you angles you hadn't considered. Maybe 2-3 of those are worth exploring. That's enough to find a reframe if one exists.

The key is using AI as a brainstorming partner, not an oracle. You're looking for prompts to your own thinking, not finished insights.

## Presenting a reframe

When you do find a reframe, the PREP framework (Point, Reason, Example, Point) helps you present it convincingly:

**Point:** State the reframe directly. "I have a hypothesis: this isn't a data quality problem, it's a semantic layer problem."

**Reason:** Explain the observation that led you there. "Each team built their own aggregations from raw events with their own definitions. The numbers aren't wrong — they're just measuring different things."

**Example:** Make it concrete. "Finance counts a user as 'active' if they logged in. Product counts them if they completed an action. Engineering counts them if they generated any event. Same word, three definitions."

**Point:** Return to the reframe and its implications. "If this is a semantic layer problem, we need a single source of truth for metric definitions — not pipeline fixes."

The PREP structure makes your reasoning transparent and gives the team specific claims to push back on. A reframe that can't survive scrutiny isn't worth much.

## What success looks like

You know the reframe worked when:

- The team's approach is meaningfully different from what would have emerged without it
- Stakeholders say "I hadn't thought about it that way"
- There's a clear before/after in how the team understands the problem
- The solution ends up simpler than the obvious approach would have been

In our case, the semantic layer project was actually *smaller* than the audit-and-fix approach would have been. Instead of chasing bugs across dozens of pipelines, we built one shared definition layer. The reframe didn't just change the solution — it made the problem tractable.

## When reframing isn't the answer

A caveat: sometimes it really is just a bug. Not every problem rewards frame-hunting. If the symptoms are narrow, reproducible, and localized — debug first. Reframing is high-leverage when the obvious solution feels like it's fighting the system, when multiple teams are confused about the same thing, or when you've "fixed" the problem before and it keeps coming back. If none of those apply, trust your instincts and ship the patch.

## The one-liner

The highest-leverage moment in any project is before the first line of code. Sometimes you find the reframe yourself. Sometimes a coworker sees what you can't. Either way — the difference between solving the right problem and perfectly solving the wrong one is worth a few hours of frame-hunting.
