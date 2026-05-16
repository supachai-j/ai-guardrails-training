---
source_type: web
source_url: https://arxiv.org/abs/2212.08073
ingested_at: 2026-05-16
title: "Constitutional AI: Harmlessness from AI Feedback (Bai et al., 2022, Anthropic)"
---

# Constitutional AI Paper Summary

**Full Title:** Constitutional AI: Harmlessness from AI Feedback

**arxiv ID:** 2212.08073

**Submission Date:** December 15, 2022

**Subject Categories:** Computation and Language (cs.CL); Artificial Intelligence (cs.AI)

**Authors:** Yuntao Bai, Saurav Kadavath, Sandipan Kundu, Amanda Askell, Jackson Kernion, Andy Jones, and 45 additional authors from Anthropic

## Abstract

The researchers describe training a helpful AI assistant toward safety objectives through self-improvement techniques requiring no human labels for harmful outputs. Instead, they use "a list of rules or principles" to guide development. Their methodology combines two phases: supervised learning where the model generates self-critiques and revisions, followed by reinforcement learning using "RL from AI Feedback" (RLAIF). The paper notes the system can "engage with harmful queries by explaining its objections to them" while maintaining transparency through chain-of-thought reasoning.

## Key Technical Concepts

- RLAIF (Reinforcement Learning from AI Feedback)
- Harmlessness without evasiveness
- Constitutional principles as training guidelines
- Self-critique and revision mechanisms
- Preference modeling for reward signals
