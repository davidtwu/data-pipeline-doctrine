---
title: "The Anti-Slop Series, Part 1: What Is AI Slop and Why Should You Care?"
date: 2026-03-30
tags:
  - ai
  - writing
  - career
description: "AI slop is everywhere — in docs, PRDs, architecture proposals. Here's what it is, why it happens, and why technical writers need to care."
draft: false
---

Last month I reviewed a design doc that used the phrase "robust and scalable solution" four times. The author was a strong engineer. The architecture was sound. But the document read like it was written by a committee of middle managers who'd been fed through a blender.

It wasn't. It was written with Claude, lightly edited, and shipped. The author didn't notice the problem because the words *sounded* professional. That's the trap.

## The term

"AI slop" emerged as internet slang around 2022, initially describing low-effort AI-generated images. Simon Willison popularized it for text in May 2024. By the end of that year, Oxford Dictionary shortlisted it for Word of the Year (332% usage increase). Merriam-Webster and the American Dialect Society both named "slop" their 2025 Word of the Year.

The academic definition comes from Duede et al. in their 2025 paper "[Why Slop Matters](https://arxiv.org/abs/2601.06060)," which identifies three properties:

1. **Superficial competence** — It looks polished but lacks depth
2. **Asymmetric effort** — Trivial to produce, costly to verify  
3. **Mass producibility** — Can be generated at scale

That last property is the killer. When everyone has access to the same text generator with the same training, everyone's output starts to converge. Your design doc sounds like my design doc sounds like the vendor's marketing copy.

## The data

This isn't subjective. Researchers have measured it.

A linguistics study found that "delve" appears roughly 400% more often in recent PubMed articles than it did before late 2022. One analysis of online writing found "meticulously researched" increased in frequency by about 3,900% in the generative AI era.

The arxiv paper "Measuring AI Slop in Text" (Shaib et al.) found that some patterns appear **over 1,000x more frequently** in LLM output than in human-written text. Not 10x. Not 100x. A thousand times.

When you read something and think "this feels like AI," you're not imagining it. Your brain is pattern-matching against a statistical anomaly.

## Why this happens

The culprit is RLHF — Reinforcement Learning from Human Feedback. During training, human annotators rate model outputs. The model learns to produce text that gets high ratings.

The problem: annotation is tedious work, often outsourced, and annotators develop shortcuts. Certain words and structures become proxies for "good writing" — formal vocabulary, balanced sentence structure, the rule of three. The model learns these proxies and amplifies them.

Alex Hern at The Guardian [reported in April 2024](https://www.theguardian.com/technology/2024/apr/16/techscape-ai-gadgest-humane-ai-pin-chatgpt) that because RLHF annotation was heavily outsourced to English-proficient workers in countries like Nigeria, some patterns may reflect formal Nigerian English habits being rewarded repeatedly, then amplified at internet scale. The mechanism is clear either way: RLHF creates a homogenized "good writing" style that millions of people then copy and propagate.

## The vocabulary tells (circa 2024-2025)

The specific words shift as models evolve, but as of this writing, you know the tells:

- delve, tapestry, testament, landscape, realm
- underscore, meticulous, commendable, robust, seamless
- "it's important to note," "navigate the complexities"
- "rich cultural heritage," "stands as a testament to"
- "ever-evolving landscape," "in today's fast-paced world"

These aren't bad words. Humans use them too. But LLMs use them at statistically impossible frequencies. When three of them appear in the same paragraph, your reader's slop detector fires — consciously or not.

## The skeleton problem

Here's what most people miss: **deleting "delve" doesn't fix the problem.**

Louis Bouchard at Towards AI puts it well: even when the most obvious AI words are scrubbed out, the feeling often remains. The surface vocabulary has been cleaned; the underlying skeleton hasn't.

LLM-generated text follows predictable structural patterns:

- Tidy paragraph arcs (setup → elaboration → conclusion)
- Five-paragraph essay transitions ("Furthermore," "Moreover," "In conclusion")
- Zoom-out endings that gesture at a "bigger picture" no one asked for
- The rule of three everywhere (three examples, three benefits, three takeaways)

You can find-and-replace "delve" with "explore" all day. If the skeleton is still pure model, readers will feel it.

## Why technical writers should care

If you're a staff+ engineer, your written output is a significant part of your impact. Design docs, architecture proposals, RFCs, internal blog posts — these artifacts shape decisions and outlast your tenure.

When your writing reads like slop, three things happen:

1. **Credibility erosion.** Readers mentally categorize your doc with spam before they've processed the content. Your good ideas get filtered out.

2. **Signal loss.** The homogenized style strips out the markers of genuine expertise — the specific details, the hard-won insights, the "I tried X and it failed because Y" that only comes from experience.

3. **Review fatigue.** Other engineers start skimming your docs because they've learned that the first three paragraphs are throat-clearing. They miss the important parts buried in paragraph four.

The irony is that AI can make you a faster, better writer — but only if you understand what it's doing wrong and fix it. Unedited AI output is a net negative for your reputation.

## The one-liner

AI slop is what happens when statistical optimization for "sounds professional" replaces actual thinking. Your readers can tell, even when they can't articulate why.

---

*Next in this series: [[anti-slop-part-2-anatomy-of-slop|Part 2: The Anatomy of Slop]] — a pattern recognition guide with concrete examples and a self-assessment checklist.*
