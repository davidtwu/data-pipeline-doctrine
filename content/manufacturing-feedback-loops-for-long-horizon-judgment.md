---
title: "TIL: Long-Horizon Judgment Is a Feedback-Loop Problem"
date: 2026-04-21
tags:
  - til
  - career
  - systems-thinking
description: "I've been researching how senior engineers develop multi-year technical judgment. The interesting finding isn't about thinking skills. It's that the domain doesn't provide feedback, so the good ones manufacture their own."
draft: false
---

I've been reading about how senior engineers develop the kind of multi-year technical judgment you see from Distinguished Engineers on panels. I haven't put the findings into practice yet. Writing this down as a marker of what I want to try.

## The research finding

The 2009 Kahneman-Klein paper ["Conditions for Intuitive Expertise"](https://journals.sagepub.com/doi/10.1037/a0016755) makes a claim I hadn't considered: intuitive expertise only develops in environments with two properties together. The environment has regularities *and* practitioners get accurate, timely feedback. Remove the feedback, and what looks like experience is just confident pattern-matching from noise.

Long-horizon engineering decisions (platform bets, architectural invariants, multi-year technology positioning) fail the second test. They resolve on timescales so long that by the time you get the answer, you've forgotten what you predicted, why, and what model you used. You remember the wins. You rationalize the losses. Everybody gets to feel like they were mostly right.

This is why "20 years of experience" often means "one year of experience, 20 times." Without feedback, the loop never closes.

## What the good ones apparently do

Tetlock's [Good Judgment Project](https://goodjudgment.com/) found that the practice separating superforecasters from everyone else wasn't the forecasts. It was the updating discipline after each one resolved.

The translation to engineering:

1. Write down dated predictions with probabilities attached. Not prose opinions. Actual numbers with resolution criteria and resolution dates.
2. Resolve them on a schedule. Weekly is the commonly cited cadence.
3. Write one sentence per miss: *what model was wrong?*

The point isn't prediction accuracy. The point is making your judgment legible to yourself, so you can see when it drifts.

## The diagnostic I failed

Here's the test that made me stop and think: can you, right now, pull up a file containing dated predictions you made 6-12 months ago with probabilities attached, and tell me your calibration?

I can't. I have opinions I've shared in design docs. I have bets I've made architecturally. But nothing dated, probabilistic, and resolvable. Which means I have no way to distinguish "I was right a lot" from "I remember the times I was right."

## What I'm trying

Starting with one prediction per day on agentic AI topics I work on. Resolution date, probability, falsifiable criterion. Spreadsheet for now. I'll revisit in a quarter and see if the discipline sticks, or if I'm just writing unfalsifiable predictions to avoid being wrong.

Report back when there's data.

## The one-liner

If you can't show your calibration, you don't have judgment. You have memory.
