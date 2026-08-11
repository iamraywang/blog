---
date: '2025-04-02T03:19:34+08:00'
title: 'Practical of Building Reasoning based Applications'
math: true
categories: ["AI"]
tags: ["LLM"]
---

Remember how DeepSeek released the R1 model and dropped its technical report right around the Chinese New Year? It definitely shook things up.

The shift from DeepSeek V3 to R1 marks a fundamental transition from "fast thinking" to "slow thinking", a significant leap in how models handle complex reasoning, which same as human beings. In some ways, the release of R1 feels like a direct, highly effective answer to the path OpenAI carved out with the release of O1 late last year. Even now, OpenAI hasn't disclosed the technical implementation details of O1, which is why some people say OpenAI has become "CloseAI." DeepSeek R1's implementation is a simple and effective practical way for us to learn how to make a reasoning model.

## Why We Need Reasoning Model?

In cognitive psychology, System 1 and System 2 are two modes of thought described by psychologist Daniel Kahneman in his book "Thinking, Fast and Slow." These two systems represent the different ways our brains process information and make decisions. **System 1 (fast, intuitive, and automatic) and System 2 (slow, deliberate, and logical)**. Previous most Large Language Models (LLMs) developed until recently have functioned primarily as advanced versions of System 1. They excel at predicting the next token based on statistical patterns. However, this desgin limitation comes with a significant drawback: "hallucination." Because these models prioritize probabilistic likelihood over rigorous logical verification, they often confidently present falsehoods or baseless claims—a phenomenon often described as "confidently talking nonsense."

Reasoning models like DeepSeek R1 are designed to bridge this gap by incorporating a System 2-like mechanism. By forcing the model to generate a "chain of thought" before finalizing an answer, the system is incentivized to self-correct, verify constraints, and break down complex problems into manageable logical steps. This explicit reasoning process provides three core benefits:

1. **Superior Logical Reasoning:** While traditional models are often susceptible to intuition and statistical probability, reasoning models can break down complex problems and perform step-by-step deduction, making them exceptionally well-suited for high-difficulty mathematical calculations, debugging code, and solving complex puzzles.
2. **Significant Reduction in Hallucinations:** Through built-in self-correction and "reflection" loops, reasoning models can identify and discard erroneous intermediate steps before arriving at a final conclusion, substantially improving the accuracy and objectivity of their output.
3. **Transparent and Explainable Process:** Traditional models provide direct results, making it difficult for users to discern the underlying logic; in contrast, reasoning models expose the complete "Chain of Thought," allowing users to clearly understand the AI's analytical process for easy verification and source tracing.

We need reasoning models because they transform LLM from a statistical language model into a reliable cognitive partner capable of rigorous deliberation. In essence, while System 1 models rely on learned patterns and intuition, much like a student focused on humanities; System 2 models utilize logical deduction to navigate specific tasks, acting more like a science student who derives answers through systematic calculation and reasoning. By utilizing reasoning models, we can observe the model's thinking process before it arrives at its final answer.

## Implementation of DeepSeek R1

The implementation of DeepSeek R1 is remarkably direct and efficient. Moving away from overly complex reinforcement learning pipelines, it adopts a training paradigm based on Reinforcement Learning (RL). The core process can be summarized as follows: building upon the DeepSeek V3 base model, the system undergoes supervised fine-tuning using a large set of "cold-start" data to guide the model in learning the "Chain of Thought" output format. This is followed by iterative training using pure reinforcement learning (GRPO algorithm). By providing rewards based on the correctness of the final answer and the logical integrity of the reasoning process, the model naturally learns to optimize its own reasoning paths.

### GRPO (Group Relative Policy Optimization)

GRPO is a reinforcement learning algorithm. It was originally proposed to simplify the training process and reduce the resource consumption of Proximal Policy Optimization (PPO), which is widely used in RL optimization stage of LLMs.

Traditional reinforcement learning (such as PPO) requires an Actor model to generate responses and a Critic model to evaluate them. The Critic model typically has a parameter count comparable to that of the Actor, consuming an immense amount of memory. DeepSeek's innovative GRPO completely abandons the Critic model.

For a given question $q$, the Actor continuously samples a group of outputs $\{o_1, o_2, ..., o_G\}$. Then, a reward function (such as accuracy and formatting rules) which replace critic model is used to calculate the score $\{r_1, r_2, ..., r_G\}$ for each output. Next, the mean $\mu$ and standard deviation $\sigma$ of these scores are calculated to normalize the rewards.

$$A_i = \frac{r_i - \mu}{\sigma}$$

Here, $A_i$ represents the advantage. GRPO directly updates the Actor model parameters using this group relative advantage. By dropping the Critic model, it saves a massive amount of memory.

### How to Inject Reasoning Capabilities into a Basic Language Model

So, the problem here is how to generate groups of reasoning outputs during training from a non-reasoning model like V3. Deepseek use a simple method, use a prompt template to generate groups of reasoning outputs from V3 model. The prompt template used in R1-zero just like following:

```
A conversation between User and Assistant.
The user asks a question, and the Assistant solves it.
The assistant first thinks about the reasoning process 
in the mind and then provides the user with the answer. 
The reasoning process and answer are enclosed within 
<think>...</think> and <answer>...</answer> tags, respectively, i.e., 
<think> reasoning process here </think> <answer> answer here </answer>. 
User: prompt. Assistant:
```

By leveraging the GRPO training algorithm and guiding the model with a simple reasoning prompt, we can imbue the V3 model with foundational reasoning capabilities, though its performance at this initial stage remains limited. This approach feels remarkably similar to the logic behind AlphaGo Zero, and it is highly likely that the "R1-Zero" naming convention was inspired by that.

### From R1-zero to R1

Although DeepSeek-R1-Zero exhibits strong reasoning capabilities, it faces several issues. DeepSeek-R1-Zero struggles with challenges like poor readability, and language mixing, as DeepSeek-V3-Base is trained on multiple languages, especially English and Chinese. 

To address these limitations and enhance the model's capabilities, the DeepSeek team curated a small set of high-quality "cold-start" data, consisting of several thousand chain-of-thought samples derived from the R1-Zero outputs. They used this data to perform supervised fine-tuning on the DeepSeek V3 model, followed by a subsequent iteration of GRPO reinforcement learning. Now we get the middle stage model R1-coldstart RL model.

To further enhance the model's capabilities and enable it to intelligently decide when to engage in deep thinking versus when to provide a direct response, the team used the R1-coldstart model to generate additional sampled CoT data. This was combined with a subset of non-reasoning data to perform further Supervised Fine-Tuning and Reinforcement Learning on the V3-Base model, ultimately resulting in the final released R1 model.

### Model Distillation: Scaling Down for Practicality

While the 671B parameter DeepSeek-R1 and V3 models represent the state-of-the-art in performance, their massive MoE (Mixture-of-Experts) architecture demands significant computational resources, making them challenging to deploy in resource-constrained environments. To bridge this gap, the DeepSeek team leveraged the reasoning capabilities of the R1 model to distill knowledge into smaller, more efficient models. By using R1 to generate high-quality chain-of-thought data, they performed knowledge distillation on smaller, open-source architectures like Qwen. This process successfully imbues smaller models—ranging from 1.5B to 70B parameters with reasoning capabilities.

The following flowchart illustrates the three stages of DeepSeek's method from V3 to R1. The models enclosed in solid-line boxes represent the officially released versions, while those in dashed-line boxes represent the intermediate models generated during the training process. For more implementation details please check the original paper [DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948)

![deepseekv3tor1](images/deepseekv3tor1.svg)

## Optimize Reasoning based Applications with DeepSeek R1 Insights

Now that we have a grasp of the mechanics behind DeepSeek R1, the question shifts to how we can leverage these reasoning capabilities in real-world applications. Many enterprise and analytical tasks demand high precision, rigorous logic, and a near-zero tolerance for "hallucinated" facts. Traditional LLMs, while fluent, often fall short in these mission-critical domains due to their reliance on pattern matching rather than systematic verification. By integrating reasoning models, we can fundamentally elevate performance in tasks where the cost of error is high.

Optimizing applications for deep reasoning capabilities generally follows a three-stage workflow, mirroring the iterative improvements seen in the R1 development process:

1. **Synthetic Data Generation:** Utilize the DeepSeek R1 model to generate high-quality training samples tailored to your specific domain. This involves prompting the model to produce detailed Chain-of-Thought (CoT) reasoning paths alongside accurate final answers. Crucially, apply a filtering process to retain only the most accurate and logically sound reasoning chains.
2. **Supervised Fine-Tuning (SFT):** Perform supervised fine-tuning on a base model—such as DeepSeek R1 itself, or more computationally efficient alternatives like Qwen or Llama using the curated, high-quality dataset. This stage anchors the model in the specific reasoning patterns required for your task.
3. **Reinforcement Fine-Tuning (RFT):** Finally, subject the SFT-tuned model to an additional phase of Reinforcement Fine-Tuning. By applying task-specific reward signals, you further refine the model's "thinking" process, hardening its ability to perform deep, deliberate reasoning precisely when needed for your application's unique constraints.

The following flowchart illustrates these three stages in detail:

![deepseekv3tor1_application](images/deepseekv3tor1_application.svg)

To illustrate how we can inject deep reasoning capabilities into traditional applications, let’s walk through a real case study from a project I have been developing over the past few months for XXX bank.

The application focuses on corporate credit rating for bank lending. The original system relied on a traditional machine learning approach, utilizing a LightGBM model to process over 400 distinct features to determine a credit score. While effective at predicting risk, this conventional method acts as a "black box," providing a final numerical rating without offering any insight into the underlying factors driving that decision. To overcome this, our objective was to leverage a large reasoning model to automatically analyze these 400+ features and uncover the deeper correlations that influence corporate creditworthiness. By integrating this reasoning capability, the system not only generates a credit level but also provides a comprehensive, logical explanation for the rating, offering actionable insights that bank staff can easily interpret and justify in their professional assessments.

To implement this, we first transform structured financial data into a natural language narrative that an LLM can reason over.

Consider a raw data record example for a corporate borrower:

**Raw Feature Data (JSON):**
```
{
  "company_name": "TechFlow Dynamics",
  "debt_to_equity": 2.1,
  "net_profit_margin": 0.05,
  "industry_growth": 0.12,
  "litigation_history": 0
}
```

**Constructed Natural Language Prompt:**

> "Analyze the credit risk for TechFlow Dynamics. The company has a debt-to-equity ratio of 2.1, a net profit margin of 5%, operates in an industry with 12% growth, and has no litigation history. Provide a credit rating and rationale."

We feed this prompt into DeepSeek R1 to generate the reasoning chain:

**Prompt to R1:**
> "Think step-by-step: Evaluate the financial health of the company based on the provided metrics and conclude with a credit rating of A, B, or C."

**R1 Output (Chain of Thought & Answer):**
> **\<think\>**
> The debt-to-equity ratio of 2.1 suggests a high leverage level, which is a risk factor. However, a 5% net profit margin indicates stable, albeit thin, profitability. The industry growth of 12% is strong, providing a tailwind. Zero litigation history suggests good legal standing and internal governance. Balancing high leverage with strong growth and clean history.
> **\</think\>**
> **\<answer\>**
> B
> **\</answer\>**

To create a high-quality SFT dataset, we compare the R1 output against our ground-truth historical labels. Only those samples where the R1 reasoning is logically sound and the result matches the bank's historical decision (e.g., 'B') are retained. This curated set of `<think>` and `<answer>` pairs becomes the training data that teaches our specialized model to replicate the bank's expert credit analysis process.

After fine-tuning the base model with this synthetic dataset, the model developed a robust capability to analyze corporate credit ratings and provide detailed, logical explanations for its decisions. Compared to the traditional LightGBM model, this reasoning-based approach achieved a 5% improvement in predictive accuracy, demonstrating the significant value of integrating structured Chain-of-Thought reasoning into domain-specific financial applications.

Finally, to further enhance model accuracy and the precision of the reasoning process, we implemented a reinforcement fine-tuning phase using GRPO. Unlike the initial SFT stage, this process does not rely on pre-existing static reasoning paths. Instead, the model is tasked with dynamically generating multiple CoT paths during training in GRPO optimization stage. 

In addition to standard format and outcome validation, consistent with the original R1 training methodology, we used a custom constraint to actively mitigate hallucinations: a data-consistency verification rule. This rule ensures that any numerical or factual data referenced within the model's generated reasoning chain must strictly match the values present in the original raw enterprise data. By enforcing this alignment between the "thought process" and the source truth, we compelled the model to ground its logic in verified facts. This refinement led to an additional 8% improvement in predictive accuracy, demonstrating the power of iterative, constraint-driven reinforcement learning in high-stakes domain applications.

We believe it is essential to design more sophisticated Chain-of-Thought verification mechanisms that incorporate domain-specific business knowledge. By enabling business experts to define the rules and standards for what constitutes superior reasoning and high-quality business interpretation, we can refine the model during the training and optimization phases to cultivate truly professional analytical capabilities. This is a long-term endeavor that bridges the gap between foundational reasoning models and deep, domain-specific expertise.
