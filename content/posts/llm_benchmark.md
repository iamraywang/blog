---
date: '2025-11-25T09:22:54-08:00'
title: 'LLM Benchmark'
draft: true
categories: ["AI"]
tags: ["LLM", "Benchmark"]
---

This article provides a full overview of the most important and hardest benchmarks for evaluating Large Language Models since 2025.11.

------------------------------------------------------------------------

# 1. Reasoning & AGI-Oriented Evaluation

## **1.1 Humanity's Last Exam (HLE)**

-   **Description:** A frontier benchmark targeting long-horizon, multi-step reasoning and general problem-solving resembling "AGI entrance exam" tasks.
-   **Difficulty:** ★★★★★ (extremely hard)
-   **Evaluation:** *Objective*
-   **Correctness:** Exact answer or deterministic final result.
-   **Link:** https://agi.safe.ai/

------------------------------------------------------------------------

## **1.2 ARC-AGI-2 (Abstraction and Reasoning Corpus AGI v2)**

-   **Description:** Measures ability to infer abstract rules from few examples (generalization).
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective*
-   **Correctness:** Output grid must match ground truth exactly.
-   **Link:** https://github.com/fchollet/ARC/

------------------------------------------------------------------------

## **1.3 MRCR v2 (8-needle)**

-   **Description:** A multi-step needle-in-haystack reasoning benchmark
    requiring retrieving and synthesizing information from extremely
    long contexts.
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective*
-   **Correctness:** Extracted answer must match hidden "needle" facts.
-   **Example:**
    -   Retrieve 1 fact buried among millions of tokens and answer
        reasoning questions.
-   **Link:** https://huggingface.co/datasets/openai/mrcr

------------------------------------------------------------------------

## **1.4 CharXiv Reasoning**

-   **Description:** Scientific reasoning over arXiv papers.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** Exact-match scientific facts + derived answers.
-   **Link:** https://charxiv.github.io/

------------------------------------------------------------------------

# 2. Mathematics & Logical Reasoning

## **2.1 AIME (American Invitational Mathematics Examination)**

-   **Description:** High-school competition math requiring multi-step
    symbolic reasoning.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** Exact integer answer (1--999).
-   **Link:**
    https://artofproblemsolving.com/wiki/index.php/AIME_Problems_and_Solutions

------------------------------------------------------------------------

## **2.2 GPQA Diamond**

-   **Description:** Graduate-level quantum physics and math exam set
    for evaluating advanced domain reasoning.
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective*
-   **Correctness:** Exact or formula-level match.
-   **Link:** https://github.com/idavidrein/gpqa

------------------------------------------------------------------------

## **2.3 MathArena Apex**

-   **Description:** Apex subset targets the hardest math reasoning
    tasks across algebra, geometry, proofs.
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective + limited subjective for proofs*
-   **Correctness:** Final answer or proof validation rules.
-   **Link:** https://matharena.ai

------------------------------------------------------------------------

# 3. Multimodal Understanding (Images, Video, Screens)

## **3.1 MMMU-Pro (Massive Multi-discipline Multimodal Understanding)**

-   **Description:** University-level multimodal exam covering 30+
    disciplines.
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective*
-   **Correctness:** MCQ or exact text answers.
-   **Link:** https://mmmu-benchmark.github.io

------------------------------------------------------------------------

## **3.2 ScreenSpot-Pro**

-   **Description:** Multimodal evaluation based on GUI screenshots;
    tests ability to locate UI elements.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** Coordinates must match ground truth.
-   **Link:** https://huggingface.co/datasets/likaixin/ScreenSpot-Pro

------------------------------------------------------------------------

## **3.3 Video-MMMU**

-   **Description:** Video-based reasoning benchmark covering
    procedural, temporal, and commonsense understanding.
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective*
-   **Correctness:** MCQ or descriptive answers with exact-match
    scoring.
-   **Link:** https://videommmu.github.io/

------------------------------------------------------------------------

## **3.4 OmniDocBench 1.5**

-   **Description:** Document multimodal analysis (PDF, tables,
    handwriting).
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** Text extraction, table parsing, QA exact match.
-   **Link:** https://github.com/opendatalab/OmniDocBench

------------------------------------------------------------------------

# 4. Coding, Software Engineering & Tool Use

## **4.1 SWE-Bench Verified**

-   **Description:** Industry-grade software bug-fixing benchmark.
-   **Difficulty:** ★★★★★
-   **Evaluation:** *Objective (unit tests)*
-   **Correctness:** Patch must pass all tests.
-   **Example:**
    -   Fix a logic bug in a real GitHub project.
-   **Link:** https://www.swebench.com

------------------------------------------------------------------------

## **4.2 LiveCodeBench Pro**

-   **Description:** Evaluates real-time code generation + execution
    across multiple languages.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** All tests must pass under execution.
-   **Link:** https://livecodebench.github.io

------------------------------------------------------------------------

## **4.3 Terminal-Bench 2.0**

-   **Description:** Measures an LLM's ability to perform real terminal
    interactions end-to-end.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** Commands must complete successfully in the
    sandbox.
-   **Link:** https://www.tbench.ai/

------------------------------------------------------------------------

## **4.4 Vending-Bench 2**

-   **Description:** Environment-interaction benchmark evaluating
    planning and tool-use inside a simulated system.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective*
-   **Correctness:** Final machine state must match expected target.
-   **Link:** https://andonlabs.com/evals/vending-bench

------------------------------------------------------------------------

# 5. Knowledge & QA (Retrieval, Facts, Global Understanding)

## **5.1 FACTS Benchmark Suite**

-   **Description:** Evaluates factual consistency and hallucination
    resistance.
-   **Difficulty:** ★★★☆☆
-   **Evaluation:** *Objective*
-   **Correctness:** Exact match with verified ground truth.
-   **Link:** https://huggingface.co/spaces/launch/factbench

------------------------------------------------------------------------

## **5.2 SimpleQA Verified**

-   **Description:** Clean, unambiguous QA requiring precise factual
    responses.
-   **Difficulty:** ★★☆☆☆
-   **Evaluation:** *Objective*
-   **Correctness:** Exact match.
-   **Link:** https://huggingface.co/datasets/basicv8vc/SimpleQA

------------------------------------------------------------------------

## **5.3 Global PIQA**

-   **Description:** Large-scale commonsense and procedural reasoning
    benchmark across cultures.
-   **Difficulty:** ★★★☆☆
-   **Evaluation:** *Objective (MCQ)*
-   **Correctness:** Choose best practical solution.
-   **Link:** https://huggingface.co/datasets/mrlbenchmarks/global-piqa-nonparallel

------------------------------------------------------------------------

## **5.4 MMMLU (Multimodal MMLU)**

-   **Description:** Multimodal extension of MMLU across 57 topics.
-   **Difficulty:** ★★★★☆
-   **Evaluation:** *Objective (MCQ)*
-   **Correctness:** Single-best-answer.
-   **Link:** https://mmmu-benchmark.github.io/

------------------------------------------------------------------------
