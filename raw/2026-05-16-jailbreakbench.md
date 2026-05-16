---
source_type: web
source_url: https://arxiv.org/abs/2404.01318
ingested_at: 2026-05-16
title: "JailbreakBench: An Open Robustness Benchmark for Jailbreaking Large Language Models (Chao et al., 2024)"
---

# JailbreakBench: Arxiv Paper Summary

**Full Title:** JailbreakBench: An Open Robustness Benchmark for Jailbreaking Large Language Models

**ArXiv ID:** 2404.01318

**Submission Date:** March 28, 2024 (v1); Last revised October 31, 2024 (v5)

**Authors:** Patrick Chao, Edoardo Debenedetti, Alexander Robey, Maksym Andriushchenko, Francesco Croce, Vikash Sehwag, Edgar Dobriban, Nicolas Flammarion, George J. Pappas, Florian Tramer, Hamed Hassani, Eric Wong

**Subject Categories:** Cryptography and Security (cs.CR); Machine Learning (cs.LG)

## Abstract (Verbatim)

"Jailbreak attacks cause large language models (LLMs) to generate harmful, unethical, or otherwise objectionable content. Evaluating these attacks presents a number of challenges, which the current collection of benchmarks and evaluation techniques do not adequately address. First, there is no clear standard of practice regarding jailbreaking evaluation. Second, existing works compute costs and success rates in incomparable ways. And third, numerous works are not reproducible, as they withhold adversarial prompts, involve closed-source code, or rely on evolving proprietary APIs."

## Benchmark Components

The benchmark comprises four elements:
1. Repository of adversarial prompts ("jailbreak artifacts")
2. **Dataset of 100 behaviors** aligned with OpenAI's usage policies
3. Standardized evaluation framework with threat model and scoring functions
4. Leaderboard tracking attack and defense performance

**Code & Leaderboard:** https://github.com/JailbreakBench/jailbreakbench and https://jailbreakbench.github.io/

**Latest Version Updates (v1.0):** Enhanced with additional attack artifacts, test-time defenses, improved jailbreak judge (Llama-3-70B), and semantic refusal evaluation datasets.
