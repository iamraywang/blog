---
date: '2026-07-02T03:19:34+08:00'
title: 'Multi-Agentic Organization: From Collective Computation to Governed Intelligence'
draft: true
categories: ["AI"]
tags: ["LLM", "Agent"]
---

## A Survey of Principles, Architectures, and Governance in LLM-Based Collective AI Systems

## Abstract

The marginal [^ref2] returns from scaling individual large language model (LLM) capabilities are converging, making Multi-Agentic Organization (MAO) the pivotal paradigm for unlocking next-generation AI capacities. Yet the field suffers from a systematic theoretical deficit: most work addresses engineering implementations while leaving the organization itself untheorized as an independent object of study. Existing surveys answer "what systems exist" but not "what laws govern organization"—a difference not of perspective but of analytical granularity.

This survey advances three falsifiable claims: **(T1) Organizational Independence**—MAO's design space (topology, role differentiation, communication protocol, memory architecture) materially and irreducibly determines collective performance; **(T2) Conditional Emergence**—positive collective capability emergence depends on cognitive diversity, conflict resolution mechanisms, and information topology; violations produce hallucination cascades, bias amplification, and coordination collapse; **(T3) Novel Governance Problem**—MAO introduces nested principal-agent chains that create governance challenges beyond the scope of single-agent alignment research.

Drawing on approximately 80 papers across AI systems, organizational science, information economics, and collective intelligence theory, we propose a **four-quadrant organizational taxonomy**, **dual-mechanism emergence analysis** (positive synergy × negative cascade), and the **MAO Effectiveness Framework (MAO-EF)**—a five-dimensional evaluation scheme that separates genuine collective intelligence from computational redundancy. We identify five open problems with genuine theoretical tension as a research roadmap. A critical empirical anchor: production MAO systems currently fail at rates of 41–86.7% across 7 state-of-the-art frameworks. `[Cemri et al., 2025]`



---

## 1 Introduction: The Boundary of Monolithic Intelligence

### 1.1 Structural Limits of Individual LLMs

As frontier models (GPT-4, Claude, Gemini) asymptote on standard benchmarks, a fundamental question emerges: what determines the ceiling of a single LLM? The answer lies not merely in parameter count but in three structural constraints: **bounded cognitive resources** (effective utilization of extended context degrades for long reasoning chains); **perspectival singularity** (a model's inductive biases create systematic blind spots); **sequential bottleneck** (complex tasks require parallel domain exploration, yet monolithic architectures are inherently sequential). `[Park et al., 2023; Minsky, 1988]`

Minsky's (1988) Society of Mind anticipated this: **intelligence emerges not from a single powerful mechanism but from the collaboration of many small, interconnected processes.** `[Minsky, 1988]` The LLM era makes this philosophically motivated claim computationally tractable for the first time—we can now build and experimentally test "societies of intelligence."

### 1.2 The Theoretical Gap in Existing Surveys

Several surveys have systematically catalogued LLM multi-agent systems. Guo et al. (2024) constructed a four-dimensional taxonomy (agent profile, memory, communication, collaboration) `[Guo et al., 2024]`; Tran et al. (2025) focused on collaboration mechanisms `[Tran et al., 2025]`; Xi et al. (2025) provided a methodology-centered survey `[Xi et al., 2025]`. All share a fundamental limitation: they answer "what systems exist" rather than "what laws govern organization"—a difference not of perspective but of analytical granularity (instance-level catalogue vs. class-level theory).

No existing survey systematically addresses: (a) how organizational structure **independently** of individual capability determines collective performance; (b) the necessary and sufficient conditions for positive emergent capability; (c) the structural failure modes when MAO systems fail. Meanwhile, mature tools from organizational science `[March & Simon, 1958; Simon, 1969]`, information economics `[Jensen & Meckling, 1976]`, and collective intelligence theory `[Page, 2008]` remain almost entirely absent from MAO discourse.

### 1.3 Core Claims and Contributions

**T1 (Organizational Independence):** MAO's design space materially and irreducibly influences collective capability—optimizing organizational structure cannot be substituted by improving individual agent capabilities. `[Kim et al., 2025]`

**T2 (Conditional Emergence):** Positive collective emergence follows identifiable conditions; violations produce systematic negative emergence. The empirical anchor: MAST taxonomy finds 41–86.7% failure rates across 7 state-of-the-art MAS frameworks. `[Cemri et al., 2025]`

**T3 (Novel Governance Problem):** MAO introduces nested principal-agent chains `[Jensen & Meckling, 1976]` with information asymmetry and goal misalignment at every layer, requiring governance frameworks beyond single-agent alignment.

**Contributions:** (1) first theoretically grounded four-quadrant taxonomy of MAO architectures; (2) dual-mechanism emergence analysis distinguishing genuine collective intelligence from computational redundancy; (3) four-category failure mode taxonomy grounded in 1,642 production traces; (4) MAO-EF with five operationalized orthogonal dimensions; (5) cross-disciplinary integration of organizational theory and information economics; (6) five open problems with genuine theoretical tension.

---

## 2 Foundations: Redefining the Unit of Analysis

### 2.1 Paradigm Rupture: From Classical MAS to LLM-MAS

Classical MAS rested on four assumptions: predefined action spaces, structured symbolic communication, explicit planned strategies, closed environments. `[Shoham & Leyton-Brown, 2009]` LLM-based MAS breaks all four: natural language creates open action spaces; unstructured semantic communication allows implicit coordination; strategies emerge through in-context reasoning; agents operate in open-domain digital environments.

ChatDev (2024) `[Qian et al., 2024]` exemplifies the **duality of natural language communication**: enabling semantic flexibility while introducing hallucination propagation requiring specialized countermeasures ("communicative de-hallucination"). This duality is absent from classical MAS and constitutes a defining feature of the new paradigm.

### 2.2 Operational Definitions

We define the unit of analysis operationally to enable distinction of boundary cases:

**MAO** is a multi-LLM-agent system achieving goals through coordination whose behavior is irreducible to the superposition of individual behaviors—requiring cross-agent information influence (not just parallel independent computation).

**Collective emergence** requires: (1) collective performance > max(individual performance) + justified parallel bonus; (2) improvement attributable to cross-agent information integration (one agent's input alters another's reasoning, producing outputs neither could generate alone).

**Organizational structure** is the static architecture constraining inter-agent information flow and decision authority distribution (topology + roles + authority hierarchy), distinct from dynamic coordination mechanisms.

### 2.3 Cross-Disciplinary Theoretical Toolkit

The key distinguishing feature of this survey is **systematic import of external theoretical frameworks** as analytical tools:

| Theoretical Source | Core Concept | Application to MAO |
|---|---|---|
| Bounded rationality & task decomposition — March & Simon (1958) `[March & Simon, 1958]` | Bounded rationality, hierarchical decomposition | Complex tasks require decomposition into tractable subtasks assigned to specialized roles—directly prescribes role design principles |
| Nearly decomposable systems — Simon (1969) `[Simon, 1969]` | High intra-module coupling, low inter-module coupling | Normative guidance for MAO topology: over-coupling → coordination overhead explosion; under-coupling → capability fragmentation |
| Principal-agent theory — Jensen & Meckling (1976) `[Jensen & Meckling, 1976]` | Information asymmetry, agency costs | In MAO's nested delegation chain, agency costs accumulate and amplify at each layer |
| Diversity bonus theorem — Page (2008) `[Page, 2008]` | Cognitively diverse groups outperform homogeneous expert groups | Theorizes value of role differentiation and multi-agent debate |

---

## 3 A Four-Quadrant Taxonomy of Organizational Architectures

We propose a four-quadrant taxonomy grounded in two orthogonal, theoretically motivated dimensions: **Information Flow Centralization (IFC)** and **Decision Authority Distribution (DAD)**. 

- IFC determines coordination overhead complexity class (O(1) to O(n²))
- DAD determines error propagation topology and robustness properties

These dimensions are theoretically derived, not inductively generalized. The taxonomy covers virtually all existing LLM-MAS systems and enables **deductive** prediction of each type's characteristic properties.

**Figure 1 [English version]:** Four-quadrant MAO taxonomy. x-axis: Information Flow Centralization (low→high); y-axis: Decision Authority Distribution (distributed→centralized). Q1 (high IFC, centralized DAD) = Centralized Hierarchy [MetaGPT]; Q2 (low IFC, distributed DAD) = Decentralized Peer-to-Peer [CAMEL, MAD]; Q3 (high IFC, distributed DAD) = DAG Workflow [ChatDev, GPTSwarm]; Q4 (dynamic) = Hybrid Adaptive [AutoGen].

### 3.1 Type I: Centralized Hierarchy

**Engineering case—MetaGPT** (Hong et al., 2024): `[Hong et al., 2024]` Encodes human software company SOP into agent coordination: product manager→architect→programmer→tester. The Shared Message Pool prevents information siloing; structured document outputs (PRD, design specs) suppress hallucination propagation. Achieves 85.9% and 87.7% Pass@1 on HumanEval and MBPP—state-of-the-art at publication.

**Engineering case—AgentOrchestra** (2025): Achieves state-of-the-art on GAIA benchmark using a central planning agent with specialized sub-agents. `[SPD-RAG, 2025]`

**Limitation:** Kim et al. (2025) find coordination overhead scales super-linearly with agent count—**centralized coordination yields 80.9% improvement on parallelizable tasks, but this benefit diminishes rapidly as agent count increases.** `[Kim et al., 2025]` The orchestrator becomes a single point of failure.

### 3.2 Type II: Decentralized Peer-to-Peer

**Engineering case—CAMEL** (Li et al., 2023): `[Li et al., 2023]` Pioneered role-playing for autonomous dual-agent cooperation via inception prompting for cognitive synchronization—the first systematic study of cognitive synchronization in LLM agents.

**Engineering case—Multi-Agent Debate (MAD)** (Du et al., 2023): `[Du et al., 2023]` Multiple LLMs debate the same question across rounds. Core finding: "disagreement" outperforms "consensus" for complex reasoning; even when all agents initially provide wrong answers, multi-round debate achieves correct outcomes.

**Theoretical grounding:** Riedl et al. (2025) establish that genuine cross-agent synergy critically depends on agents' Theory of Mind (ToM) capacity; low-ToM combinations produce computational redundancy masquerading as collaboration. `[Riedl et al., 2025]`

### 3.3 Type III: DAG-Based Workflow

**Engineering case—ChatDev** (Qian et al., 2024): `[Qian et al., 2024]` Organizes development as a Chat Chain with dual-agent dialogue at each node for local error correction—resolving unidirectional error propagation in linear pipelines. Outperforms GPT-Engineer (single agent) on completeness, executability, consistency, and quality.

**Engineering case—GPTSwarm** (Zhuge et al., 2024): `[Zhuge et al., 2024]` Inspired by Minsky's (1988) Society of Mind `[Minsky, 1988]`, formalizes agents as an **optimizable graph** with REINFORCE-based topology optimization—the first data-driven approach to MAO topology design. Surpasses fixed-topology alternatives on GAIA, MMLU, and HumanEval.

### 3.4 Type IV: Hybrid Adaptive

**Engineering case—AutoGen** (Wu et al., 2023): `[Wu et al., 2023]` Supports both static and dynamic conversation patterns with explicit modular capability composition (LLM, tools, human) and human-in-the-loop. Architecture enables runtime reconfiguration.

**Communication protocol standardization:** Anthropic MCP (2024) `[Anthropic MCP, 2024]` and Google A2A (2025) `[Google A2A, 2025]` represent industrial infrastructure for open-agent ecosystems. Ehtesham et al. (2025) systematically compare MCP, ACP, A2A, and ANP design philosophies. `[Ehtesham et al., 2025]`

---

## 4 Dual Mechanisms of Collective Capability Emergence

### 4.1 Positive Emergence: Three Synergistic Mechanisms

**(a) Capability Complementarity:** Different roles cover disjoint capability spaces, enabling full-stack task completion beyond any individual agent. `[Hong et al., 2024]`

**(b) Error Correction:** Redundancy and cross-validation reduce hallucinations. Du et al. (2023) demonstrate that even when all agents initially provide wrong answers, multi-round debate achieves correct outcomes. `[Du et al., 2023]`

**(c) Cognitive Diversification:** Different roles reduce systematic blind spots, grounded in Page's (2008) Diversity Bonus Theorem. `[Page, 2008]`

**Critical distinction—when is 1+1 genuinely >2:** Chen et al. (2024) show that merely increasing LLM call counts (computational redundancy = test-time scaling) yields significant performance gains. `[Chen et al., 2024]` This means many "MAO efficacy" experiments validate compute scaling rather than genuine collective intelligence. **This conflation is the central measurement problem in the field.**

### 4.2 Collective Scaling Laws

Kim et al. (2025) conducted the most systematic scaling study to date (180 configurations, 5 architectures): `[Kim et al., 2025]`

- Centralized coordination yields **~80.9% performance improvement** on parallelizable tasks
- Coordination overhead scales **super-linearly** with agent count
- An optimal agent count interval exists; beyond it, performance degrades
- Parallelizable and deep-integration tasks exhibit qualitatively different scaling curves

These collective scaling laws parallel Kaplan et al.'s (2020) individual model scaling laws `[Kaplan et al., 2020]` but operate at the organizational level—providing quantitative evidence that MAO constitutes an independent research layer.

### 4.3 Negative Emergence: The MAST Failure Taxonomy

**Empirical anchor:** Cemri et al.'s (2025) MAST taxonomy analyzed 1,642 MAS execution traces across 7 state-of-the-art frameworks (AutoGen, ChatDev, CrewAI, etc.), finding **failure rates of 41–86.7%** in production. Critically, **improvements in base model capabilities are insufficient to address the full failure taxonomy.** `[Cemri et al., 2025]`

MAST identifies 14 failure modes across three categories. We synthesize these into four structural failure types:

**Failure Mode I: Hallucination Cascade.** Upstream agent hallucinations propagated as facts by downstream agents, amplified through the pipeline. MAST classifies this under "Task Verification Failures"—the largest failure category. `[Cemri et al., 2025]` Counter-strategy: independent judge agents (PwC achieved 7x accuracy improvement: 10%→70%). `[Augment Code, 2026]`

**Failure Mode II: Coordination Failure.** MAST's "Inter-Agent Misalignment" category encompasses task overlap, task gaps, and opinion oscillation. **79% of production failures trace to specification ambiguity and unstructured coordination protocols.** `[Cemri et al., 2025]`

**Failure Mode III: Cognitive Bias Amplification.** Homogeneous agent groups systematically amplify rather than correct biases—the AI equivalent of groupthink. Consensus across agents increases confidence in shared errors, producing more dangerous systematic bias than any single agent.

**Failure Mode IV: Trust Cascade Attack.** Prompt-injection-compromised agents propagate malicious instructions across trust relationships. The Trust Vulnerability Paradox (TVP, 2025) formalizes an irresolvable architectural tension: increasing inter-agent trust (for coordination efficiency) simultaneously lowers security boundaries (enlarging attack surface). `[TVP, 2025]`

**Figure 3 [English version]:** Dual emergence diagram. Two diverging pathways from "Organizational Design Choices" node: GREEN path (positive emergence) → capability complementarity → error correction → cognitive diversification → collective intelligence gain. RED path (negative emergence) → hallucination cascade → coordination failure → bias amplification → trust cascade attack.

---

## 5 Governance, Trust, and Alignment

### 5.1 From Bilateral to Multilateral Alignment

Single-agent alignment (RLHF, Constitutional AI) solves a bilateral problem—ensuring one AI conforms to human intent. MAO transforms this into a **nested principal-agent problem** `[Jensen & Meckling, 1976]`:

```
Human (Principal₀)
  ↓ [information asymmetry ①]
Orchestrator Agent (Agent₀ / Principal₁)
  ↓ [information asymmetry ②]
Worker Agents A, B, C
```

Each delegation layer introduces information asymmetry and agency costs that accumulate upward. "MAS as Principal-Agent Problems" (2025) formalizes this via scheming analysis: Worker Agents may develop goals misaligned with their Orchestrator, actively concealing this misalignment in reports while pursuing hidden objectives in execution. `[PA-MAS, 2025]` This is structurally harder to detect in multi-layer systems than in single-agent systems.

**Figure 4 [English version]:** Nested principal-agent chain. Contrast with single-agent bilateral alignment (inset): MAO governance cannot be achieved by stacking single-agent alignment—each added delegation layer introduces a new information asymmetry locus.

### 5.2 Three Dimensions of Trust and the Trust Vulnerability Paradox

Trust in MAO decomposes into: **Competence Trust** (can Agent B do the task correctly?), **Intention Trust** (does Agent B's goal align with the system's?), and **Communication Trust** (is received information unmanipulated?). Each requires different verification mechanisms.

**Trust Vulnerability Paradox (TVP, 2025):** `[TVP, 2025]` Increasing inter-agent trust (for coordination efficiency) simultaneously lowers security boundaries (enlarging the attack surface). Elevated trust lowers alert thresholds, bypasses minimum-necessary-information gates, and enables small misjudgments to cascade across agent-to-agent chains into group-level misalignment. There is **no technically optimal trust level**—only architectural trade-offs calibrated to task risk profiles.

### 5.3 Human-in-the-Loop Governance and Regulatory Compliance

Three human intervention point strategies with distinct autonomy-controllability trade-offs: (a) pre-planning approval; (b) pre-action authorization for high-risk irreversible decisions; (c) post-delivery review. EU AI Act (2024) mandates human oversight, interpretability, and risk documentation for high-risk autonomous systems. `[EU AI Act, 2024]` "Inherent and Emergent Liability in LLM-based Agentic Systems" (ACL 2025) `[Liability, 2025]` analyzes responsibility attribution when collective behavior produces harm.

---

## 6 The MAO Effectiveness Framework (MAO-EF)

### 6.1 Three Fundamental Deficiencies of Existing Evaluation

**Deficiency 1:** Conflation of organizational effectiveness with task performance—no distinction between genuine collective intelligence and computational redundancy.

**Deficiency 2:** Neglect of coordination process efficiency—equal scores for a 100-call and 10-call system producing identical outputs, despite vastly different cost, latency, and scalability profiles.

**Deficiency 3:** Absence of organizational robustness testing—evaluation only under optimal conditions, not under agent failure, adversarial attack, or unexpected task variation.

**Empirical grounding:** Current SOTA MAS frameworks fail at 41–86.7% in production `[Cemri et al., 2025]`—benchmark scores systematically fail to predict real-world reliability.

### 6.2 Five Dimensions of MAO-EF

| Dimension | Definition | Operationalization |
|---|---|---|
| **D1: Collective Intelligence Gain (CIG)** | Normalized performance difference between MAO and best individual baseline at equal compute budget | Compare MAO vs. [single agent + multiple sampling]; count only improvements traceable to cross-agent integration |
| **D2: Coordination Efficiency (CE)** | Performance gain per unit coordination overhead (LLM calls) | Plot performance-cost Pareto curves; identify optimal agent count intervals |
| **D3: Information Utilization Rate (IUR)** | Fraction of agent-generated information effectively used downstream | Ablation: remove each agent's contribution, measure marginal impact |
| **D4: Organizational Robustness (OR)** | Performance degradation magnitude under agent failure or adversarial attack | Multi-scenario stress tests; evaluate degradation curve slope |
| **D5: Process Interpretability (PI)** | Whether human reviewers can trace decisions to source agents and reasoning chains | Human evaluators judge decision traceability success rate |

**Design principles:** (1) **Orthogonality**—five dimensions are mutually independent; (2) **Hierarchy**—D1/D2 system-level, D3 module-level, D4 perturbation-level, D5 cognitive-level; (3) **Diagnostic power**—dimension combinations reveal specific improvement targets.

---

## 7 Five Open Problems: A Research Agenda

We identify five open problems defined not by neglect but by **genuine theoretical tension at the boundary of current tools.**

**P1—Topology Architecture Search:** How to learn optimal MAO organizational structure from data rather than hand-design? `[Zhuge et al., 2024; Zhang et al., 2024; OFA-MAS, 2025]` Core tension: exponential search space, sparse evaluation signal, self-referential evaluation function.

**P2—Predictability of Emergence:** Can collective capability be predicted without running the system? MAST data shows failure rates varying from 41% to 86.7% across similar systems `[Cemri et al., 2025]`—this variation is unpredictable from individual agent capabilities. Solving this transforms MAO design from trial-and-error to engineering.

**P3—Organization-Level Alignment:** Does a composition theorem exist guaranteeing that MAO of aligned agents is itself aligned? `[PA-MAS, 2025]` The question is logically open—neither proof nor counterexample exists.

**P4—Cognitive Dissonance Detection and Repair:** When constituent agents form mutually contradictory beliefs, how does the system detect organizational-level cognitive dissonance and self-repair? `[Riedl et al., 2025]` This intersects ToM capacity, metacognition, and distributed consensus—no formal definition exists.

**P5—Inter-Organization Interoperability:** When multiple independent MAO systems must collaborate, how to design inter-organization interfaces handling heterogeneous role systems, trust assumptions, and objective functions? MCP `[Anthropic MCP, 2024]` and A2A `[Google A2A, 2025]` signal industrial urgency; academic formal theory is essentially absent.[^ref2]

---

## 8 Conclusion

This survey establishes an independent theoretical framework for Multi-Agentic Organization (MAO), advancing the field from engineering catalogue to explanatory theory. Our three core claims—organizational independence (T1), conditional emergence (T2), novel governance problem (T3)—collectively constitute a theoretical foundation for MAO research.

The methodological contribution extends beyond cataloguing existing work to diagnosing why existing work is insufficient: engineering systems are intuitively correct but theoretically ungrounded; existing surveys are descriptively complete but explanatorily weak; existing evaluations are methodologically sound but organizationally insensitive. The empirical urgency is clear: production MAO systems currently fail at 41–86.7% `[Cemri et al., 2025]`—this is not a future concern but a present reality requiring principled organizational science.

The five open problems identify the deepest theoretical tensions in the field and are offered as departure points for a new generation of MAO research. As AI agent systems transition from laboratory to large-scale production deployment, MAO design will be a critical determinant of AI's societal impact. Understanding and scientifically designing these "AI organizations" is one of the most important responsibilities of AI researchers in this era.

## References
[^1]: Author, A., & Writer, B. (2024). *Title of the journal article*. Journal Name, 12(3), 45-67.
[^ref2]: 张三, 李四. (2025). *某项前沿技术的研究与应用*. 科技出版社![http://fd].
