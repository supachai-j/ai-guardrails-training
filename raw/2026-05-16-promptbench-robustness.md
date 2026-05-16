---
source_type: web
source_url: https://arxiv.org/abs/2306.04528
ingested_at: 2026-05-16
title: "PromptRobust: Towards Evaluating the Robustness of Large Language Models on Adversarial Prompts (Zhu et al., 2023)"
---

# PromptRobust: Robustness Evaluation Benchmark for LLMs

**Full Title:** "PromptRobust: Towards Evaluating the Robustness of Large Language Models on Adversarial Prompts"

**Authors:** Kaijie Zhu, Jindong Wang, Jiaheng Zhou, Zichen Wang, Hao Chen, Yidong Wang, Linyi Yang, Wei Ye, Yue Zhang, Neil Zhenqiang Gong, Xing Xie

**arxiv ID:** 2306.04528

**Submission Date:** June 7, 2023 (v1); last revised July 16, 2024 (v5)

**Subject Categories:** Computation and Language (cs.CL); Cryptography and Security (cs.CR); Machine Learning (cs.LG)

**Code Repository:** https://github.com/microsoft/promptbench

## Abstract Summary

The paper introduces a benchmark measuring how LLMs respond to adversarial prompts. Attacks operate across multiple linguistic levels—character, word, sentence, and semantic—mimicking realistic user errors. The evaluation encompasses diverse tasks including sentiment analysis, natural language inference, reading comprehension, machine translation, and mathematical problem-solving.

**Key Quantitative Details:**
- 4,788 adversarial prompts generated
- 8 tasks evaluated
- 13 datasets tested
- Multiple adversarial attack types applied

The findings indicate "contemporary LLMs are not robust to adversarial prompts" and provide recommendations for prompt composition strategies.

## Note on naming

This paper is sometimes referenced colloquially as "PromptBench" — the formal title in v5 is "PromptRobust", and the code/dataset is published as `microsoft/promptbench`.
