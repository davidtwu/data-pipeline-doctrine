---
title: "The Anti-Slop Series, Part 3: The Anti-Slop Workflow"
date: 2026-03-30
tags:
  - ai
  - writing
  - til
description: "A practical workflow for writing with AI assistance without producing slop — prompt guidelines, the 50% delete rule, and a before/after example."
draft: false
---

In [[anti-slop-part-1-what-is-ai-slop|Part 1]], I explained what AI slop is. In [[anti-slop-part-2-anatomy-of-slop|Part 2]], I showed how to recognize it. Now: how do you actually write with AI without producing it?

## The mental model

Think of yourself as the discriminator in a GAN (Generative Adversarial Network). The AI generates; you discriminate. Your job isn't to accept or reject wholesale — it's to apply judgment that the model can't.

This reframe matters. You're not "editing AI output." You're collaborating with a fast, dumb writer who has no taste. The taste is your job.

## The prompt guidelines

Hamel Hussain's anti-slop guidelines have become widely cited. Here are the five that matter most:

1. **No filler words.** State this explicitly in your prompt.
2. **Every sentence must add information.** If it restates the previous sentence, delete it.
3. **Shorter words over longer words.** "Use" not "utilize." "Help" not "facilitate."
4. **One example if it suffices.** Don't pad to three.
5. **Trust the reader's intelligence.** No "it's important to note" or "as we discussed."

I include a version of this in every writing prompt:

```
Follow these guidelines:
- No filler words or throat-clearing phrases
- Every sentence must add new information
- Prefer short words over long words
- One example per concept unless more are needed
- No "it's important to note" or similar editorializing
- No zoom-out conclusions about "the bigger picture"
- Trust the reader to understand without summaries
```

This doesn't eliminate slop, but it reduces it by maybe 40%. You still need to edit.

## The 50% delete rule

Even with good prompting, delete at least half the AI output.

This sounds aggressive. It is. But here's the thing: AI is verbose by default. RLHF trained it to produce text that *feels* complete, which means padding, hedging, and restating.

When I edit AI-generated text, I ask one question for each sentence: "Does this add information the reader doesn't already have?" If the answer is no, I delete it.

A 1,000-word AI draft typically becomes 400-600 words after editing. The information density doubles. The reading experience improves.

## The workflow

### Step 1: Write your own outline (5 min)

Don't ask AI to structure your thinking. That's where the skeleton problem starts. Write bullet points of what you actually want to say, in the order you want to say it.

### Step 2: Generate section by section (10-15 min)

Feed the AI one section at a time with your outline point as the prompt. This prevents the model from inventing structure you didn't ask for.

Bad:
> "Write a design doc for migrating to Kafka."

Good:
> "Write 2-3 paragraphs explaining why our current RabbitMQ setup can't handle our throughput requirements. Be specific about the bottleneck."

### Step 3: Aggressive edit (15-20 min)

For each paragraph:
1. Delete the first sentence (it's usually throat-clearing)
2. Delete any sentence that restates the previous one
3. Delete hedging phrases ("it's worth noting," "one might argue")
4. Replace any word over three syllables with a shorter synonym if one exists
5. Read aloud. If you wouldn't say it, rewrite it.

### Step 4: Add your voice (5-10 min)

AI can't write from experience. Add:
- One specific example from your actual work
- One thing you tried that didn't work
- One opinion that a reasonable person might disagree with

These are the markers of genuine expertise that slop lacks.

## Before and after

Here's a real example. I asked Claude to write about why data validation matters in ETL pipelines.

### Before (AI output, lightly prompted)

> Data validation is a crucial component of any robust ETL pipeline. It's important to note that without proper validation, data quality issues can propagate downstream, leading to incorrect analytics, flawed decision-making, and ultimately, significant business impact. Modern data architectures typically implement validation at multiple stages — during ingestion, transformation, and before loading — to ensure comprehensive coverage.
>
> Furthermore, validation serves as a critical safeguard against schema drift, null values, and type mismatches. By implementing thorough validation checks, organizations can catch issues early in the pipeline, reducing the cost and complexity of remediation. This proactive approach is essential for maintaining data integrity in today's fast-paced, data-driven business environment.

Word count: 114. Information density: low.

### After (edited)

> Validate early. A bad record that makes it to your warehouse costs 10x more to fix than one caught at ingestion.
>
> We validate at three points: ingestion (schema conformance), transformation (business rules), and pre-load (referential integrity). The ingestion check catches 80% of issues. The other two exist because the 20% that slip through are the ones that break dashboards.

Word count: 58. Same information, half the words, plus a specific ratio from experience.

What I deleted:
- "crucial component of any robust" — filler
- "It's important to note that" — throat-clearing
- "leading to incorrect analytics, flawed decision-making, and ultimately, significant business impact" — obvious consequences, rule of three
- "Modern data architectures typically" — vague attribution
- "comprehensive coverage" — meaningless
- "Furthermore" — transition inflation
- "critical safeguard" — importance inflation
- "thorough validation checks" — redundant
- "proactive approach is essential" — editorializing
- "today's fast-paced, data-driven business environment" — zoom-out filler

What I added:
- "10x more to fix" — specific claim (from experience)
- "catches 80% of issues" — specific ratio
- "the ones that break dashboards" — concrete consequence

## The GAN dynamic

Rajiv Pant frames this as a GAN dynamic: as you get better at discriminating slop, you force yourself to generate better prompts and edits. As your prompts improve, you need sharper discrimination. The floor rises.

The end state isn't an arms race where AI learns to evade detection. It's a world where your minimum standard for published writing goes up. That's a good outcome regardless of how the text was produced.

## The one-liner

AI makes you faster at generating words. Your job is to be faster at deleting the wrong ones.

---

*This is Part 3 of the Anti-Slop Series. See also: [[anti-slop-part-1-what-is-ai-slop|Part 1: What Is AI Slop?]] and [[anti-slop-part-2-anatomy-of-slop|Part 2: The Anatomy of Slop]].*
