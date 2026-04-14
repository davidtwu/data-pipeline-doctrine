---
title: "Cross-Domain Pattern Reading for Engineers"
date: 2026-04-13
tags:
  - architecture
  - systems-thinking
  - career
description: "The best solutions to engineering problems often come from outside engineering. A practical method for finding them by reading across biology, economics, military strategy, and other fields."
draft: true
---

I was writing a strategy for how data teams should adopt shared tooling across an organization. Multiple teams, each building pipelines for their own projects, each with their own stack. Real fragmentation. The kind where every new project reinvents ingestion, transformation, and orchestration from scratch because nobody trusts anyone else's setup.

The obvious move was to pick a standard and drive adoption. Write a doc, present it at a review, get leadership alignment, roll it out. We'd tried versions of this before. It hadn't stuck. Teams nodded along in meetings and then kept building their own way.

I kept getting stuck in the strategy work. I'd interview stakeholders and get conflicting opinions about what the shared tooling should even look like. One team wanted flexibility. Another wanted guardrails. A third thought the whole effort was premature. I didn't have enough data to resolve the disagreements, and I couldn't reach consensus because the disagreements weren't about facts. They were about assumptions.

The breakthrough came from a place I wasn't expecting.

## The linguistics analogy

I'd been reading about Donella Meadows' leverage points, trying to understand how to create impact through shifts in paradigm rather than shifts in tooling. That reading led me to cross-domain examples of how standards emerge in other fields. One of them was linguistics.

When populations that speak different languages need to trade, they develop a pidgin: a simplified shared vocabulary, just enough to transact. Nobody designs it. It emerges from repeated contact. Over time, if the contact persists, children grow up speaking the pidgin natively. They add grammar, complexity, nuance. The pidgin becomes a creole, a full language. The standard wasn't imposed. It crystallized from practice.

I read that and stopped. That was my problem. Not the surface (programming languages vs. human languages) but the structure: distributed actors, no central authority, real investment in existing approaches, a need for coordination that couldn't be mandated from above. Linguists had been studying this dynamic for decades. I'd been trying to solve it from first principles.

That moment of recognition is what cross-domain pattern reading feels like. You're not borrowing a solution. You're discovering that someone else has already mapped the territory you're lost in.

## Abstracting the problem

The reason the linguistics case connected was that I'd already, almost accidentally, done the first step: I'd described my problem in structural terms rather than engineering terms.

"Five data teams won't adopt shared tooling because they've each built custom solutions" is an engineering problem. It invites engineering solutions: better tooling, better docs, a migration guide.

"How do you coordinate distributed autonomous actors on a shared interface when each has invested in a different approach and switching costs are real?" is a structural problem. It invites structural solutions from anywhere.

The abstraction strips away the jargon and exposes the bones. A biologist could engage with that second framing. So could an economist or a military strategist. That's what makes it useful: it turns your problem into a search query that works across every domain simultaneously.

Genrich Altshuller figured this out by analyzing over 200,000 patents. His core finding when building TRIZ (his theory of inventive problem solving): problems and solutions repeat across industries and sciences. But you can only see the repetition at the structural level. At the surface level, a data pipeline adoption problem and a language standardization problem look nothing alike.

## Naming the constraints

Once I had the structural framing, I could name why the problem was actually hard. Not the symptoms (fragmentation, duplicated effort, integration pain) but the constraints that made it resist solution.

Three stood out:

**Switching costs.** Every team had invested months in their current stack. Migrating meant rewriting working code, retraining people, and accepting a temporary productivity hit. Even if the shared tooling was better, the cost of getting there was real and immediate. The benefits were diffuse and future.

**Incentive misalignment.** Each team was evaluated on delivering their project, not on organizational coherence. A team that paused project work to migrate to shared tooling would look slower than a team that kept shipping on their custom stack. Locally rational, globally dysfunctional.

**Threshold dynamics.** Shared tooling adopted by one team is overhead. Adopted by four teams, it's infrastructure. The value is nonlinear, but you have to get through the low-value phase to reach the high-value phase. Nobody wants to be the first mover when the payoff requires three more movers behind you.

Naming these precisely mattered because each constraint pointed toward a different body of knowledge. Switching costs are studied extensively in economics. Incentive misalignment is a core topic in game theory and organizational behavior. Threshold dynamics show up in epidemiology, network science, and the sociology of social movements.

## Three cases that changed my thinking

With the constraints named, I went looking for how other domains had solved them. Three cases reshaped my strategy.

**The internet RFC process.** The IETF doesn't standardize internet protocols by committee vote or executive mandate. Someone writes a spec, builds a reference implementation, and invites others to try it. The motto is "rough consensus and running code." Standards that solve real problems get adopted. Standards that don't, die quietly. Nobody is forced to use TCP/IP. It won because it worked, and because working implementations existed before the standard was finalized.

What this taught me: demonstration beats persuasion. The teams I was trying to convince didn't need a better slide deck. They needed to see shared tooling solving a problem they actually had, on a team they actually respected.

**USB vs. FireWire.** FireWire was technically superior on almost every dimension. USB won the market. The reason: Intel embedded USB controllers directly into chipsets, making USB essentially free for hardware manufacturers. FireWire required a licensing fee from Apple. The switching cost to USB was zero. The switching cost to FireWire was nonzero. Technical merit was irrelevant once the economics diverged.

What this taught me: reducing switching costs can matter more than improving the product. If I wanted teams to adopt shared tooling, I needed to invest as much in migration tooling and compatibility layers as in the tooling itself. Make the switch cheap enough and inertia stops being a barrier.

**Basketball's three-point revolution.** For decades, NBA teams treated the three-point shot as a specialty play. The Golden State Warriors built an entire offensive system around it starting in 2014 and won three championships in four years. Within five seasons, every team in the league had restructured around three-point shooting. The average number of three-point attempts per game nearly doubled. No mandate. No league memo. Competitive proof from a visible, dominant adopter.

What this taught me: one successful early adopter, made visible, can trigger a cascade. The mechanism isn't persuasion. It's competitive pressure. Teams don't adopt because you convinced them. They adopt because they watched someone else win.

## The strategy I wrote

None of these ideas came from the data engineering literature. All of them came from asking "who else has solved this structural problem?"

The strategy combined the three levers:

Partner with one willing team to build a reference implementation on shared tooling and measure the results. Don't try to get all five teams aligned first. Don't write a standard and hope for adoption. Build something real with one team and make the outcomes undeniable. That's the RFC model.

Invest heavily in migration tooling. Compatibility layers, automated conversion scripts, side-by-side running capability. Make the switching cost as close to zero as possible. If teams have to rewrite six months of work to adopt, they won't, regardless of how good the tooling is. That's the USB model.

Publish the results internally. Quantify the before and after. Let other teams see what the early adopter gained. Don't mandate adoption for the remaining teams. Let competitive visibility do the work. That's the basketball model.

The strategy doc I produced was structurally different from anything I would have written by staying inside the data engineering frame. The old frame produced "pick a standard and drive adoption." The new frame produced "demonstrate, reduce friction, and let competitive dynamics do the rest." Different assumptions, different mechanisms, different actions.

## When to reach outside your domain

This approach isn't always the right move. If your pipeline is slow because of a bad join, profile it. If a service is throwing errors, read the logs. Domain expertise solves domain problems.

Cross-domain reading pays off when the problem is structural rather than technical. A few signals:

The problem keeps recurring despite repeated attempts to fix it. You've "solved" it before and it came back. That's a sign you're treating symptoms while the structure that generates them stays intact.

The obvious solutions have already been tried. If writing a standard and presenting it at a review was going to work, it would have worked the first time.

You find yourself saying "this isn't really a technical problem." It's a coordination problem, an adoption problem, an incentive problem. Those are structural problems, and structural problems have been studied across dozens of fields.

Conflicting stakeholder opinions can't be resolved with more data. When disagreements are about assumptions rather than facts, you're dealing with paradigm-level differences. Other domains have navigated those.

Cognitive scientist Dedre Gentner's research on analogical reasoning established the test for whether a cross-domain analogy is actually useful: do the relationships between elements in the source domain mirror your domain? USB and shared tooling adoption share relational structure (switching costs, network effects, incumbent lock-in). If only the surface features match ("both involve networks!"), the analogy will mislead you.

## Building the habit

I keep a running list of structural problems I encounter and their domain-neutral descriptions. When I read outside engineering, I'm loosely pattern-matching against that list. Most of the time, nothing connects. Occasionally something clicks.

The reading doesn't need to be systematic. A chapter of McChrystal's *Team of Teams*. A podcast about evolutionary biology. An article about how hospitals adopted surgical safety checklists. The latticework builds over time. Charlie Munger spent decades building his, and he'd be the first to say it compounds slowly.

The one deliberate practice: when I hit a problem that resists domain-internal solutions, I spend 30 minutes on the abstraction step before doing anything else. Strip the jargon, name the constraints, translate into other vocabularies. That 30 minutes has saved me weeks more than once.

## The one-liner

The best solutions to engineering problems often come from outside engineering. You just have to describe the problem in terms that let you find them.
