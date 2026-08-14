# Cognitive Resource Allocation

## Adaptive Cognitive Tiering and Task-Comprehension Handshakes for Stateful Heterogeneous Artificial Intelligence Systems

### Enterprise Research Thesis, Systems Architecture, and Experimental Prospectus

- **Working designation:** CRA
- **Primary mechanisms:** Adaptive Cognitive Tiering (ACT), Task-Comprehension Handshake (TCH)
- **Author:** Samuel Lawson — Sovereign Systems Research Program, Dark Science Division
- **Version:** 1.0 Research Baseline
- **Date:** 2026-08-13
- **License:** CC BY-NC-ND 4.0
- **Research program relationship:** Sovereign Systems Research Program
- **Architecture relationship:** Compatible with SOVEREIGN, Sovereign Orchestration Workspace, TCAIN, ATG, and BioDigital Jazz
- **Epistemic classification:** Architectural thesis and experimental prospectus; empirical superiority not yet established

**Lineage:** v0.1 (initial multi-model draft) → v0.2 (independent validation pass: citation verification, formal corrections, structural revisions; archived in this repository at `versions/`, SHA-256 as archived `589f04aa98f12e2b3ccb3bba8b637426330ad5a72aa1cb3772fcb7259745c90f`; original pre-attribution-correction hash `f9ae7db1b31565e44d93b7d2d519e2bb712c2da0730144dfdac27062a50f712e`) → **v1.0** (this document: enterprise restructure merged with all v0.2 corrections).

### Change Log: v0.2 → v1.0

1. Adopted the enterprise restructure: five-class epistemic status taxonomy (§2), ten-layer architecture (§10), twenty-entry threat model (§23), nine-condition experimental grid (§24), enterprise validation program (§32), twelve-phase engineering sequence (§33), and full appendix schema set (Appendices A–I).
2. Restored all v0.2 corrections silently dropped in the intermediate draft: plain-text mathematical notation throughout; hysteresis formalism with corrected inequality (§15.2); keystone-hypothesis dependency analysis (§25.11) and keystone-failure falsification condition (§31); generator-verifier allocation (§13.6); the operational de-escalation rule (P6, §9.11); mechanical-versus-judged comprehension checking and named handshake limitations (§11); handshake outcome disambiguation (§11.5); H1 decomposition; escalation-recall attribution rule (§26); minimal publishable unit and priority ordering (§24.3); same-model control forks in live branching (§29); operational precedent (§5.5); and the complete verified reference list with years and arXiv identifiers.
3. Restored dropped references: Smith (Contract Net), Srivastava et al. (RunAgent), Madaan et al. (Self-Refine), Shinn et al. (Reflexion), Du et al. (multiagent debate), Wang et al. (Mixture-of-Agents), Ramírez et al. (uncertainty routing), Starmer et al. (I-PASS).
4. Restored quantitative anchors: Replay Gap post-fork rewrite rates and configuration-dependent determinism; RoadmapBench task scale and best-model success rate; MetaCogAgent routing gain as an effect-size prior for power analysis.
5. Resolved notation collisions (routing-state history renamed `L_t`; the comprehension vector retains `H`); repaired the corrupted cognitive-waste formula (§22.3).
6. Recorded the v0.2→v1.0 branch divergence itself as an operational instance of handoff omission (§5.5).
7. Author attribution set to Samuel Lawson per the program registry decision, unifying the public record with the published ATG thesis; the archived v0.2 edition carries the matching correction.

---

# Table of Contents

1. Authorship and Development Provenance
2. Epistemic Status
3. Abstract
4. Executive Thesis
5. Introduction
6. Problem Definition
7. Related Work and Novelty Boundary
8. Canonical Vocabulary
9. Enterprise Design Principles and Core Invariants
10. Unified CRA Architecture
11. Task-Comprehension Handshake
12. Persistent Worker Identity
13. Adaptive Cognitive Tiering
14. Cognitive Demand and Capability Representation
15. Cognitive Resource Scheduling
16. Model Transition and State Handoff
17. Multimodal Cognitive Allocation
18. Enterprise Runtime Architecture
19. Integration with SOVEREIGN, TCAIN, ATG, and BioDigital Jazz
20. Authority, Security, and Trust Boundaries
21. Observability and Evidence Architecture
22. Cognitive Economics and Resource Accounting
23. Failure Analysis and Threat Model
24. Experimental Program
25. Research Hypotheses and Keystone Structure
26. Primary Metrics
27. Secondary Metrics
28. Statistical and Evaluator Methodology
29. Live Model-Switch Experiment
30. Ablations
31. Falsification Conditions
32. Enterprise Validation Program
33. Engineering Sequence
34. Product and Operational Implications
35. Enterprise Use Cases
36. Relationship to the Broader Cognitive Systems Thesis
37. Limitations
38. Findings
39. Conclusion
40. Appendices A–I
41. References

---

# 1. Authorship and Development Provenance

The core concept developed in this thesis begins from two observations about heterogeneous AI execution.

First, the cognitive difficulty of a complex task is not constant over its lifetime. A task can begin in a state of high ambiguity and architectural uncertainty, collapse into routine implementation, encounter a new contradiction that again requires advanced reasoning, return to mechanical execution, and finally require high-quality independent review.

Second, assigning a task to a worker does not prove that the worker has interpreted the assignment correctly. A model can competently perform the wrong work because its interpretation of objective, constraints, scope, authority, or success criteria differs from the conductor's intended task.

From those observations follows the central systems concept:

> **Machine cognitive capability should be allocated dynamically according to the evolving state of work, while task identity, authority, accumulated state, and acceptance criteria remain external to and independent of the particular model currently performing the work.**

The formalization separates that concept into two primary mechanisms:

- **Task-Comprehension Handshake (TCH)** establishes shared task understanding before consequential execution.
- **Adaptive Cognitive Tiering (ACT)** adjusts the cognitive resources assigned to that task as its requirements change.

The broader architecture is named **Cognitive Resource Allocation (CRA)**.

AI systems assisted in literature review, mathematical formalization, architectural criticism, drafting, and experimental design, under the program's standing multi-model review convention (independent drafting, adversarial review, and validation by separate systems). Such assistance does not itself establish the validity of the thesis. The research claims remain contingent on implementation, controlled comparison, reproducibility, and falsification.

---

# 2. Epistemic Status

This thesis contains five categories of statement.

## 2.1 Established external findings

Existing research demonstrates that:

- computation can be allocated adaptively according to problem difficulty;
- sparse expert routing can conditionally activate specialized computational resources;
- language-model cascades and routers can trade model cost against expected quality;
- multi-agent systems can delegate work according to estimated competence;
- switching models within an agent trajectory can materially alter subsequent behavior and therefore cannot safely be evaluated as if later trajectory state were fixed.

These findings establish precedent. They do not prove CRA.

## 2.2 Architectural interpretations

These statements describe how known mechanisms may coherently be combined:

- a persistent worker can be represented separately from its model;
- comprehension validation can precede execution;
- task-state information can inform routing;
- model allocation can move both upward and downward during one task;
- an allocation can pair a generation resource with a distinct verification resource;
- structured handoff can preserve worker state across model substitutions.

## 2.3 Research hypotheses

These are empirically testable claims:

- TCH will reduce execution failures caused by task misunderstanding;
- ACT will reduce total cost to accepted work without unacceptable quality loss;
- bidirectional tiering will outperform static assignment on non-stationary tasks;
- structured handoff will preserve continuity better than transcript transfer;
- comprehension telemetry will predict downstream difficulty.

The last two carry disproportionate weight: they are respectively a precondition and the keystone of the architecture (§25.11).

## 2.4 Engineering requirements

These are design requirements rather than scientific discoveries:

- routing must be auditable;
- authority must not silently expand during model substitution;
- deterministic evidence should dominate model judgment where possible;
- automatic routing must remain inside operator-defined provider, budget, and authority limits.

## 2.5 Unknowns

The following remain unresolved until measured:

- the optimal number of cognitive tiers;
- the best demand representation;
- the reliability of model self-assessment;
- how often model switching is economically justified;
- the amount of state required for successful handoff;
- the minimum task horizon at which CRA becomes beneficial;
- whether multimodal specialist decomposition consistently beats capable generalist models;
- how strongly routing policies generalize across model families.

No claim is made that CRA constitutes artificial general intelligence, consciousness, sentience, or autonomous self-awareness.

---

# 3. Abstract

Modern artificial-intelligence systems increasingly operate across heterogeneous language models, multimodal models, coding agents, deterministic tools, retrieval systems, and specialized reasoning processes. Yet many orchestration systems continue to assign cognitive capability at coarse granularity. A task is sent to one model, one agent retains the same model throughout execution, or a fixed ensemble is invoked regardless of how the cognitive requirements of the work evolve.

This thesis argues that such static assignment is structurally inefficient for long-running and multimodal work.

Complex tasks exhibit **non-stationary cognitive demand**. Early ambiguity may require high-capability reasoning; implementation may later become deterministic or routine; failures can create renewed complexity; specialist modalities may appear only during selected phases; and final validation may again require stronger independent reasoning.

A second source of failure arises before execution. A worker may accept a task while holding a materially incorrect interpretation of its objective, constraints, prohibited scope, authority, or completion criteria. Conventional acknowledgements such as "understood" provide little evidence that semantic task alignment has actually occurred.

This thesis proposes **Cognitive Resource Allocation (CRA)**, a stateful architecture that treats machine cognitive capability as a dynamically scheduled resource. CRA combines **Task-Comprehension Handshake (TCH)**, a bounded pre-execution protocol establishing an explicit task contract, with **Adaptive Cognitive Tiering (ACT)**, a runtime controller that escalates or de-escalates the cognitive capability assigned to a persistent worker according to evolving complexity, uncertainty, criticality, reversibility, modality, execution performance, resource availability, and operator policy. An allocation is a **(generator, verifier) pair** rather than a single model, permitting patterns such as inexpensive generation under strong or deterministic verification.

CRA separates **role identity**, **worker identity**, and **model identity**. A worker persists through its contract, state, permissions, artifacts, decisions, evidence, failures, and checkpoints. The models occupying that worker may change without changing task ownership or authority.

The resulting architecture reframes model orchestration as a resource-scheduling problem:

> **What cognitive capability is justified by the present state of the work, which available resources can supply that capability most efficiently, and can those resources be substituted without losing the task?**

Two hypotheses carry the load: that structured handoff preserves worker continuity across substitution, and that comprehension telemetry supplies a *leading* indicator of task difficulty. If both fail, CRA degenerates into known cascade routing with additional bookkeeping, and the program will record that result under that description.

The thesis defines the architecture, formal model, enterprise runtime, security boundary, observability plane, resource economics, research hypotheses, controlled experimental conditions, evaluator policy, falsification criteria, failure taxonomy, implementation sequence, and canonical data schemas required to investigate that question. A deliberate property of the intended experimental environment — serial model hosting on a single consumer GPU — places the study in the high-switching-cost regime that well-resourced laboratories do not naturally inhabit and have little incentive to characterize.

No performance advantage is claimed before experimentation.

---

# 4. Executive Thesis

The proposition can be stated in one sentence:

> **Machine cognition should be allocated as a state-dependent computational resource: consequential work should begin only after explicit task comprehension is established, and the model or reasoning process executing that work should be permitted to escalate, de-escalate, specialize, or change as cognitive demand evolves while worker state and authority remain persistent outside the model.**

This creates a division of responsibility.

**The operator owns:** objective; strategic constraints; resource policy; provider restrictions; authority; acceptance.

**The conductor owns:** task interpretation; decomposition; worker formation; dependency coordination.

**The Task-Comprehension Handshake establishes:** semantic agreement; interpreted scope; assumptions; expected method; explicit uncertainty; prohibited actions.

**The cognitive router owns:** demand assessment; tier recommendation; candidate generator and verifier selection; escalation; de-escalation; switching-cost accounting.

**The worker owns:** execution within its contract and authority envelope.

**The validator owns:** independent assessment of result evidence and acceptance criteria.

**Persistent system state owns:** continuity.

The architecture therefore distinguishes questions that are commonly collapsed:

1. What work should be performed?
2. What does the worker believe the work is?
3. What kind of cognitive capability does the work currently require?
4. Which available model or reasoning process best satisfies that requirement?
5. Does the current allocation remain justified after the task state changes?
6. Did the resulting work satisfy its contract?
7. Was the cost of obtaining accepted work better than a simpler allocation policy?

---

# 5. Introduction

## 5.1 The model is not the worker

Many AI applications still implicitly treat these expressions as equivalent:

```text
Agent = Model = Session
```

This creates a continuity problem. When the model reaches a context boundary, becomes unavailable, fails repeatedly, must be upgraded, is too expensive for remaining work, or lacks a newly required modality, replacing it can mean effectively replacing the worker.

CRA rejects this equivalence. Instead:

```text
Role  ≠  Worker  ≠  Model
```

A role identifies responsibility. A worker identifies the persistent execution state associated with one task. A model supplies temporary cognitive capability to that worker. This yields:

```text
W_i(t)    ← M_j          (worker i occupied by model j)
W_i(t+k)  ← M_l          (later, occupied by model l)

W_i(t) = W_i(t+k)        with respect to task identity, contract,
                         authority, evidence, and accumulated state
```

## 5.2 Intelligence demand varies over time

Consider a nontrivial software task:

```text
Requirement interpretation
        ↓
Architecture discovery
        ↓
Architecture decision
        ↓
Routine implementation
        ↓
Unexpected test failure
        ↓
Root-cause investigation
        ↓
Corrective implementation
        ↓
Mechanical cleanup
        ↓
Independent final review
```

The cognitive demand of these phases is clearly different. A fixed high-capability assignment can waste resources. A fixed low-capability assignment can fail when uncertainty rises. CRA therefore models cognitive demand as a trajectory rather than a label assigned once at task creation.

## 5.3 Silent misunderstanding

A second problem is independent of model strength. A strong model can solve the wrong problem extremely well.

Suppose the conductor intends:

> Repair reconnect persistence without changing the protocol.

The worker interprets:

> Replace the persistence architecture so reconnects become simpler.

Both statements concern reconnection. Only one satisfies the intended scope. This class of failure is dangerous because conventional agent logging may later classify the result as:

```text
task execution failure
```

when the actual failure occurred earlier:

```text
task interpretation failure
```

TCH makes that distinction observable.

## 5.4 Research objective

The objective of this thesis is to define and experimentally test a system that dynamically allocates heterogeneous cognitive resources to persistent workers while controlling semantic task fidelity across delegation and model transitions.

## 5.5 Operational precedent from a working program

This section records observational, single-environment evidence from the Sovereign Systems Research Program's own operating history. It is motivating precedent, not controlled evidence, and no hypothesis is considered supported by it.

**Manual tiered allocation already exists in practice.** The program's standing workflow allocates different engines to drafting, independent review, and machine execution, and escalates between them on failure — a hand-executed form of the architecture proposed here. One documented process discovery is directly a routing-policy result: inserting a *machine-state preflight before prose review* caught blockers that document-level review missed, inverting the previously recommended pipeline. In CRA vocabulary: a cheap deterministic verifier placed ahead of expensive cognition dominated the reverse ordering.

**Skipped comprehension validation is the dominant observed failure mode.** Across the program's governed execution chain, the majority of gate halts traced to a skipped confirmation-file step — an operational ancestor of the Task-Comprehension Handshake. The environment's own history indicates that omitting pre-execution confirmation is not a rare edge case but the modal failure.

**MANUAL-mode allocation is already implemented.** The Sovereign Orchestration Workspace's governed model-picker launch path — validated worker identity, workspace binding, permission envelope, lease accounting, supervised process lifecycle — is an operating implementation of the MANUAL routing mode (§15). The early engineering phases (§33) therefore build on an existing substrate rather than a green field.

**This document's own preparation produced a live handoff failure.** During drafting, a validated revision (v0.2) carrying fourteen recorded corrections was superseded by a parallel draft regenerated by a different model without the revision's structured change log. The successor draft silently dropped most of the corrections — notation repairs, a corrected formula, the keystone analysis, verified citations — and recovery required a manual delta audit against the prior version's change log. This is an uncontrolled but exact instance of the handoff-omission failure mode this thesis formalizes (§23.11): a successor initialized without structured state loses constraints and repeats or discards settled work. The incident is recorded here because a research program should not exempt its own production pipeline from its own failure taxonomy.

---

# 6. Problem Definition

CRA addresses four primary problems.

## 6.1 Static capability allocation

One model remains assigned despite changing task demand.

## 6.2 Capability mismatch

The assigned model lacks a capability required by the present task state.

## 6.3 Semantic delegation failure

The worker executes a materially incorrect interpretation.

## 6.4 Continuity loss during substitution

Switching the model causes forgotten constraints, repeated work, altered authority assumptions, decision reopening, plan divergence, and context loss.

Recent 2026 work quantifies the danger. *The Replay Gap* (Gonuguntla, 2026) forks live SWE-bench agent trajectories at controlled points, continues each fork with a different model, and compares against same-model control forks. Across roughly 900 rollouts, swaps exceeded matched control floors by +0.25 to +0.66 normalized edit distance, **rewriting 61–94% of post-fork actions**; every observed outcome flip occurred in a swap arm and none across 359 control forks; and a log-stitching replay evaluator mispredicted every success-relevant outcome. Determinism itself proved configuration-dependent: FP8-served temperature-0 controls diverged on over 90% of forks while AWQ-served controls remained near-identical.

Two consequences bind this thesis. Agentic model switching is not equivalent to changing a stateless function call — CRA treats substitution as a first-class state transition. And the null position is adversarial: **switching is expensive and disruptive by default**; the handoff mechanism must demonstrably tame divergence, not assume it away.

---

# 7. Related Work and Novelty Boundary

## 7.1 Adaptive computation

Adaptive Computation Time (Graves, 2016) demonstrated that computational depth can vary according to the difficulty of an input rather than remaining fixed. CRA generalizes the scheduling intuition to an external orchestration layer. ACT-the-mechanism asks how much internal computation this model should perform; CRA asks which external cognitive resources should occupy this persistent worker now.

## 7.2 Sparse expert routing

Sparsely gated mixture-of-experts architectures (Shazeer et al., 2017) established that conditional expert activation can greatly expand capacity without activating every expert for every input. CRA shares the principle of conditional specialization but differs in substrate: the experts may be distinct model families, local or cloud models, deterministic tools, coding models, multimodal models, long-context models, or adversarial multi-model nodes. They are not internal sub-networks of one neural architecture.

## 7.3 Model cascades and routing

FrugalGPT (Chen, Zaharia, and Zou, 2023) demonstrated the importance of selecting combinations of models according to cost and expected quality, including cascaded strategies that substantially change inference economics. AutoMix (Aggarwal et al., 2023) uses estimated reliability — notably **self-verification by the smaller model** — to determine whether work should escalate to a larger one; this locates value in cheap verification, not only cheap generation, a precedent §13.6 builds on. RouteLLM (Ong et al., 2024) learns routing between stronger and weaker models from preference data to optimize the quality-cost tradeoff. Ramírez, Birch, and Titov (2024) show that a smaller model's uncertainty can itself decide escalation.

These establish strong precedent for model routing. CRA does **not** claim novelty in choosing among models. The narrower candidate contribution is **trajectory-state routing of a persistent worker**, including comprehension validation before execution; task-contract persistence; mid-task escalation and de-escalation; role continuity; generator-verifier pairing; structured model handoff; switching-cost accounting; multimodal capability vectors; and resource optimization measured to accepted completion.

## 7.4 Distributed task negotiation

The Contract Net Protocol (Smith, 1980) introduced task distribution through negotiation between nodes possessing work and nodes capable of performing it — task assignment as an interactive process rather than fixed centralized dispatch. TCH shares this ancestry but addresses a different failure. The principal question is not *which worker should win the contract* but *does the worker's semantic interpretation of the contract match the delegator's intended task closely enough to authorize execution*.

## 7.5 Multi-agent reasoning and iterative refinement

Multi-agent debate can improve performance on some reasoning and factuality tasks (Du et al., 2023). Self-Refine (Madaan et al., 2023) iterates generate-critique-refine within one model. Reflexion (Shinn et al., 2023) introduces episodic linguistic feedback across attempts. Mixture-of-Agents (Wang et al., 2024) aggregates layered outputs from multiple models. CRA is complementary: those methods answer *how additional reasoning should be produced*; CRA asks *when additional reasoning is justified, what form it should take, and when the system should stop paying for it*. Each of these processes is representable as a Tier-4 resource rather than the mandatory path for every task.

## 7.6 Metacognitive delegation

MetaCogAgent (Wang and Shu, 2026) explicitly evaluates task-capability alignment before execution, combining verbalized uncertainty with historical capability profiles and delegating work an agent estimates exceeds its competence. On its purpose-built benchmark it reports 82.4% task accuracy — 8.7% above the best routing baseline — with fewer API calls than ensemble baselines. RunAgent (Srivastava et al., 2026) enforces stepwise natural-language plan execution through constraints and rubrics while dynamically selecting among reasoning, tool use, and code execution.

This substantially narrows any claim that CRA invents self-aware or constraint-guided delegation. CRA instead investigates whether capability estimation can operate **continuously across one evolving task**, with the same worker surviving changes in model assignment. MetaCogAgent's reported 8.7% routing gain additionally serves this program as an **effect-size prior for power analysis** (§28.2).

## 7.7 Long-horizon engineering

RoadmapBench (Xu et al., 2026) grounds 115 long-horizon tasks in real open-source version upgrades across 17 repositories and 5 languages — median oracle modification approximately 3,700 lines across 51 files — and finds the strongest evaluated frontier model resolves only 39.1% of tasks. Such tasks are well suited to testing CRA because their cognitive demands change over extended execution.

## 7.8 Honest novelty boundary

CRA should not claim ownership of: model routing; adaptive computation; mixtures of experts; metacognition; agent delegation; task contracts; multimodal specialization; checkpointing; uncertainty estimation; or model cascades.

The provisional contribution is their specific integration into:

> **a stateful cognitive scheduler that establishes bilateral task comprehension, preserves worker identity outside the model, performs bidirectional capability reassignment across a changing task trajectory as generator-verifier pairs, and evaluates the allocation by total cost and quality of accepted work.**

That claim remains provisional pending a systematic prior-art review and empirical testing.

---

# 8. Canonical Vocabulary

- **Cognitive Resource** — any bounded computational capability capable of contributing to reasoning or execution: deterministic program; lightweight model; specialist model; frontier model; multimodal model; retrieval system; multi-model reasoning node.
- **Worker** — a persistent task-bearing execution identity defined by task contract, state, authority, history, artifacts, evidence, unresolved issues, and resource policy.
- **Role** — the functional responsibility associated with a worker.
- **Cognitive Tier** — an abstract class of capability required by a task state.
- **Cognitive Demand** — the current multidimensional requirement imposed by the task.
- **Allocation** — the (generator, verifier) resource pair currently assigned to a worker (§13.6).
- **Task-Comprehension Handshake** — a bounded pre-execution process requiring explicit demonstration of task understanding.
- **Task Contract** — the accepted representation of the worker's objective, constraints, success criteria, scope, authority, and intended execution boundary.
- **Adaptive Cognitive Tiering** — bidirectional adjustment of cognitive capability during task execution.
- **Escalation** — movement toward greater or more specialized cognitive capability.
- **De-escalation** — movement toward less expensive capability once higher capability is no longer justified.
- **Cognitive Handoff** — the transfer of persistent worker state from one model execution context to another.
- **Cognitive Waste** — use of more expensive cognitive capability than was necessary to achieve the accepted result.
- **Under-Tiering** — assigning insufficient capability, producing avoidable failure, rework, or escalation.
- **Cost to Accepted Work** — total resources consumed from task formation through successful acceptance.

---

# 9. Enterprise Design Principles and Core Invariants

## 9.1 Principles

**P1. State belongs to the system.** The model is not the canonical store.

**P2. Authority belongs to the worker contract.** Changing models must not change permissions.

**P3. Understanding precedes consequential execution.** Semantic alignment is an executable condition, not an assumed courtesy.

**P4. Capability is selected by requirement.** Model prestige is not routing policy.

**P5. Routing is reversible.** The system must move both upward and downward.

**P6. Downward movement is conservative — and rule-bound.** The sufficiency of a cheaper resource for the *remaining* work is a counterfactual that cannot be cheaply tested in advance. The operational rule: **de-escalate only into task regions whose acceptance is deterministically checkable or independently validated.** Where the verifier is deterministic, an under-capable generator's failure is caught rather than shipped, and the cost of a wrong de-escalation collapses from task damage to bounded retry cost. Absent such a check, retain the current tier regardless of estimated sufficiency.

**P7. Deterministic evidence dominates where possible.** Tests, hashes, schemas, permissions, and direct telemetry should not be replaced by model opinion.

**P8. Switching has cost.** A model transition is not free in either computation or trajectory stability (§15.2).

**P9. No-op is legitimate.** A mature router must be able to conclude that the present allocation is already appropriate.

**P10. Every subsystem must earn its complexity.** If TCH, ACT, or model switching does not outperform simpler strategies under controlled comparison, it should be narrowed or removed. This is consistent with the BioDigital Jazz engineering principle that expensive control machinery must justify itself through measured benefit.

## 9.11 Core invariants

The principles above are directions; the following are enforceable conditions.

- **CRA-I1** — No consequential worker begins execution without an accepted task contract.
- **CRA-I2** — Worker identity is independent of model identity.
- **CRA-I3** — Model substitution must not erase accepted task state.
- **CRA-I4** — Every routing decision is recorded with its evidence.
- **CRA-I5** — Model self-assessment alone cannot determine cognitive tier.
- **CRA-I6** — Operator provider, authority, and resource limits dominate automatic routing.
- **CRA-I7** — A worker may request escalation without being classified as failed.
- **CRA-I8** — Model substitution cannot expand worker authority.
- **CRA-I9** — De-escalation is permitted only into task regions whose acceptance is deterministically checkable or independently validated (the P6 rule, stated as an invariant).
- **CRA-I10** — Validation remains logically separate from execution.
- **CRA-I11** — Task contracts preserve unresolved ambiguity rather than fabricating certainty.
- **CRA-I12** — Resource optimization cannot override the minimum acceptance-quality threshold.

---

# 10. Unified CRA Architecture

CRA contains ten logical layers.

- **Layer 0: Human Policy** — objective authority; allowed providers; privacy; cost ceilings; maximum tier; irreversible-action policy; acceptance authority.
- **Layer 1: Project State** — the durable context surrounding tasks.
- **Layer 2: Task Formation** — the conductor converts project need into a bounded task packet.
- **Layer 3: Task-Comprehension Handshake** — worker interpretation is compared against intended task semantics.
- **Layer 4: Task Contract** — accepted understanding becomes persistent state.
- **Layer 5: Cognitive Demand Estimation** — the system estimates what abilities the current state requires.
- **Layer 6: Resource Routing** — a tier and a concrete (generator, verifier) allocation are selected.
- **Layer 7: Worker Execution** — the selected resources operate within the worker's authority.
- **Layer 8: Checkpoint and Reassessment** — task state, uncertainty, failure, progress, and resource use are measured.
- **Layer 9: Validation and Acceptance** — independent evidence determines whether the task has completed satisfactorily.

The control cycle:

```text
FORM → UNDERSTAND → CONTRACT → ASSESS → ALLOCATE → EXECUTE → OBSERVE
     → REASSESS → CONTINUE / ESCALATE / DE-ESCALATE / BLOCK → VALIDATE
```

---

# 11. Task-Comprehension Handshake

## 11.1 Purpose

TCH is designed to identify disagreement before mutation. It specifically targets: misunderstood objective; constraint omission; unauthorized scope; wrong artifact selection; misunderstood success criteria; hidden assumptions; authority ambiguity; unnecessary redesign.

## 11.2 Task formulation

```text
T = (O, Y, C, S, F, A, P, B)
```

where `O` = objective; `Y` = required output; `C` = constraints; `S` = success criteria; `F` = forbidden scope; `A` = relevant artifacts; `P` = authority; `B` = budget.

## 11.3 Worker interpretation

Worker `W` produces:

```text
I_W = (O', Y', C', S', F', M, U, R)
```

where primed elements are the worker's interpretations of the corresponding packet elements; `M` = intended method; `U` = unresolved uncertainty; `R` = risks and assumptions.

## 11.4 Comprehension vector — mechanical and judged components

```text
H = [h_O, h_Y, h_C, h_S, h_F, h_P, h_A]
```

for objective fidelity, output fidelity, constraint fidelity, success fidelity, forbidden-scope fidelity, authority fidelity, and artifact relevance.

The dimensions partition by how they can be checked:

- **Mechanically checkable:** constraint fidelity (`h_C`) — did the interpretation enumerate every constraint identifier in `C`; forbidden-scope fidelity (`h_F`) — did it echo the complete forbidden list and add nothing to authorized scope; artifact relevance (`h_A`) — do all referenced artifacts exist in `A`; authority fidelity (`h_P`) — does the acknowledged envelope match `P` exactly. These checks are deterministic and require no model judgment.
- **Judgment-requiring:** objective fidelity (`h_O`), output fidelity (`h_Y`), and success fidelity (`h_S`) require semantic comparison, performed by the conductor.

CRA does not reduce `H` to one scalar. A single critical constraint miss can invalidate an otherwise excellent interpretation.

## 11.5 Outcomes

Four states, disambiguated by *where the defect lies*:

```text
TASK_CONTRACT_ACCEPTED
    Interpretation matches intent within tolerance. Execution authorized.

TASK_CONTRACT_REVISION_REQUIRED
    Defect lies in the worker's interpretation. Conductor corrects and reissues.

TASK_PACKET_DEFECTIVE
    Defect lies in the packet itself (internal ambiguity or contradiction).
    Conductor must repair the packet; the worker is not at fault.

TASK_REQUIRES_OPERATOR_CLARIFICATION
    Defect lies in intent or authority — a question only the operator can
    answer. Escalates outside the conductor's authority.
```

## 11.6 Boundedness

The handshake itself can become bureaucracy. Therefore: reversible trivial tasks may use abbreviated TCH; normal consequential work should target one exchange; a bounded retry count must exist; repeated disagreement escalates to clarification rather than infinite negotiation.

## 11.7 Known limitations

Two limitations are inherent and are named here rather than discovered later.

**Restatement is not compliance.** TCH validates interpretation at assignment time. It does not guarantee adherence during execution; instruction drift can occur after a perfect restatement. H1 is therefore decomposed (§25): H1a tests whether TCH *detects* pre-execution misinterpretation; H1b tests whether restatement quality *predicts* execution compliance at all.

**The judge is partly an LLM.** The judgment-requiring dimensions of `H` are evaluated by the conductor, importing the evaluator-reliability limits of §28 into the gate itself. Mitigations: maximize the mechanically checkable share of `H`; log conductor comprehension judgments for audit against outcomes; treat the handshake as one control among several. A capable model can also produce plausible-sounding assumptions without genuine understanding (§23.1); requiring method, artifacts, prohibited-scope echo, and expected completion state raises the bar without eliminating the risk.

---

# 12. Persistent Worker Identity

A worker is represented as:

```text
W = (T, C, A, X, E, D, U, G, R)
```

where `T` = task identity; `C` = accepted contract; `A` = authority; `X` = current state; `E` = evidence; `D` = decisions; `U` = unresolved issues; `G` = execution history; `R` = resource state.

The model is represented separately as `M_t`. The executing system is the composition:

```text
W ⊗ M_t
```

A model swap changes `M_t`, not `W`. This gives **persistent role continuity without persistent model dependence.**

---

# 13. Adaptive Cognitive Tiering

## 13.1 Tier 0: Deterministic

No generative model. Hashing; compilation; tests; schema validation; file transforms.

## 13.2 Tier 1: Lightweight

Classification; extraction; narrow edits; routine summarization.

## 13.3 Tier 2: Standard Specialist

Conventional coding; debugging; structured synthesis; routine technical analysis.

## 13.4 Tier 3: Advanced Reasoning

Architecture; novel debugging; high-ambiguity work; multi-constraint planning.

## 13.5 Tier 4: Deep Cognitive Process

May be the strongest single model; debate; multi-model review; a **TCAIN node** (the program's reference Tier-4 implementation); or another adversarial reasoning system. CRA is, among other things, TCAIN's invocation policy — the formal answer to *when* an adversarial reasoning node is justified.

The number of tiers is provisional. The architecture requires ordered capability classes, not exactly five labels.

## 13.6 Allocation as generator-verifier pairs

Changing an allocation does not always mean changing the *generator*; frequently the correct move is to change the *verifier*. Verification of a candidate output is often cheaper than generation, so the cost-optimal use of a strong model is frequently to review a weak model's work rather than to produce the work itself. AutoMix's small-model self-verification (§7.3) is the single-model ancestor of this pattern.

An allocation at each checkpoint is therefore a pair:

```text
allocation_t = (g_t, v_t)
```

| Pattern | Generator | Verifier | Typical use |
|---|---|---|---|
| Bulk implementation | Tier 1–2 | Tier 3 review or Tier 0 tests | Routine edits under supervision |
| Hard synthesis, checkable | Tier 3 | Tier 0 deterministic tests | Design work with executable acceptance |
| Consequential judgment | Tier 3 | Tier 3, lineage-disjoint | High-impact decisions without deterministic checks |
| Deep reasoning | Tier 4 (TCAIN node) | External validator | Adversarial multi-model work |

The de-escalation rule (P6/CRA-I9) is naturally expressed here: lowering `g` is safe precisely when `v` is deterministic or independent.

---

# 14. Cognitive Demand and Capability Representation

## 14.1 Demand vector

At state `t`:

```text
D_t = [d_r, d_c, d_v, d_l, d_u, d_k, d_n, d_x]
```

where dimensions may represent reasoning; coding; vision; long context; uncertainty; criticality; novelty; execution/tool complexity.

**Who computes `D_t` — specified.** In the early phases (§33, Phases 1–8) the estimator draws only on: (1) **deterministic runtime signals** — test failures, retry counts, validator rejections, diff size, budget consumption, checkpoint latency; (2) **handshake telemetry** — ambiguity count, assumption count, constraint disagreements, disclosed risks; (3) **historical task-family profiles**; (4) **operator annotations**. Model self-reported difficulty is admissible only as one weighted input and never as the sole source (CRA-I5). No learned demand estimator or learned router exists before the controlled experimental phase; early routing is hand-tuned rules over these signals, and the hypotheses (§25) are accordingly framed against a *reasonable heuristic router* — a claim that can actually be tested — rather than an optimal one.

## 14.2 Model capability vector

```text
Q_m = [q_r, q_c, q_v, q_l, q_s, q_t, q_e]
```

representing empirically estimated capability: reasoning; coding; vision; context; structured output; tool use; evidence fidelity.

## 14.3 Operational profile

```text
O_m = (cost, latency, memory, throughput, availability)
```

Capability and operational profiles come from controlled qualification and observed history, not marketing claims — and are **versioned against exact deployment configurations, including quantization and serving stack**. The Replay Gap's FP8-versus-AWQ determinism finding (§6.4) demonstrates that a model name does not identify a behavioral object; the (weights, quantization, serving configuration) triple does.

## 14.4 Authority is separate

Worker authority is `A_W`. The crucial invariant:

```text
Q_m  does not imply  A_W
```

Higher capability never implies greater permission.

---

# 15. Cognitive Resource Scheduling

## 15.1 Routing function

The router receives:

```text
S_t = (D_t, Q, O, A_W, B_t, L_t, F_t)
```

where `B_t` = remaining budget; `L_t` = routing and execution history; `F_t` = failures. (v1.0 renames history from `H_t` to `L_t` to remove the collision with the comprehension vector.)

The routing policy `pi(S_t)` returns:

```text
r_t = (tier_t, g_t, v_t, a_t)
```

where `a_t` is a routing action:

```text
KEEP
ESCALATE
DE_ESCALATE
SPECIALIZE
SWITCH
BLOCK
REQUEST_OPERATOR
```

Routing modes: **MANUAL** (operator fixes the allocation — already implemented on the program's Workspace substrate, §5.5), **ASSISTED** (router recommends, operator confirms), **ADAPTIVE** (router acts within the policy envelope).

## 15.2 Switching economics and hysteresis

Uncontrolled adaptive routing oscillates (`Tier 2 → 3 → 2 → 3 ...`), wasting resources and destroying continuity. A transition requires:

```text
B_switch > C_switch + delta
```

where `B_switch` is the estimated benefit of changing allocation, `C_switch` the switching cost, and `delta` a stability margin.

**Composition of `C_switch`.** Switching cost is not merely handoff tokens. It comprises: handoff-packet construction; successor ingestion; **model load/unload wall-clock time** — dominant on single-GPU serial hosting, where a tier change is a full unload/load cycle measured in tens of seconds to minutes; divergence risk, with the Replay Gap's 61–94% post-fork rewrites as the adversarial prior; and post-switch re-verification. Hysteresis parameters are therefore **hardware-dependent and declared per deployment**. A consequence worth stating: the scientifically interesting hysteresis regime is precisely high-`C_switch`, serially hosted execution — a regime cluster-equipped laboratories do not experience and have little incentive to characterize, and which the intended experimental environment inhabits natively.

**Estimating `B_switch` is a counterfactual problem**, so the early phases do not attempt it directly. They use proxy triggers:

- **Escalate** when: `k` consecutive failed checkpoints, or a validator rejection, or an explicit worker insufficiency signal (`k` small, e.g., 2).
- **De-escalate** when: `m` consecutive clean checkpoints **and** the P6/CRA-I9 rule is satisfied **and** a minimum residency period has elapsed (`m` larger than `k`, e.g., 3+).

The asymmetry is deliberate: a mistaken escalation mainly costs resources; a mistaken de-escalation can damage the task.

---

# 16. Model Transition and State Handoff

## 16.1 Model switching is trajectory-changing

CRA assumes model substitution can affect future state materially; the branching-rollout evidence (§6.4) supports treating every substitution as a controlled state transition rather than an implementation detail.

## 16.2 Required handoff packet

A successor receives structured state, not an unbounded conversation dump. Minimum contents:

```text
worker identity
task contract
current objective
completed work
current artifact state
verified facts
accepted decisions        (frozen; successor may not reopen without new evidence)
rejected decisions
assumptions
unresolved issues         (open; successor may engage)
failed attempts
evidence references
authority
resource state
next expected action
```

The frozen/open distinction is load-bearing: it is the packet's defense against successor reinterpretation (§23.13), in which a new model relitigates settled questions without new evidence.

## 16.3 Transition sequence

```text
CURRENT MODEL → FREEZE CHECKPOINT → GENERATE HANDOFF → VALIDATE HANDOFF
             → RELEASE MODEL → ASSIGN SUCCESSOR → SUCCESSOR ACKNOWLEDGEMENT
             → CONTINUE
```

## 16.4 Successor acknowledgement

The successor explicitly identifies: task objective; current state; next action; invariants; unresolved issues; authority. This acts as a second comprehension check after substitution.

## 16.5 The correct analogy is a shift handoff, not a process checkpoint

An operating-system checkpoint is a lossless byte copy; a CRA handoff is semantic compression — lossy by construction. The closer analog is the clinical or aviation shift handoff, and that literature is encouraging: the I-PASS program (Starmer et al., 2014) found that a structured handoff bundle materially reduced medical errors and preventable adverse events across nine hospitals relative to unstructured signout. Structured state transfer between agents of comparable capability is an empirically supported intervention in human systems; H6 tests whether the result transfers to model workers.

---

# 17. Multimodal Cognitive Allocation

CRA becomes particularly important when work crosses modalities. A task may require source code + screenshot + PDF specification + logs + audio explanation. A single generalist model may process everything, but CRA allows specialist decomposition:

```text
SCREENSHOT → vision specialist
SOURCE     → coding specialist
LOGS       → diagnostic specialist
SPEC       → document reasoner
combined state → architecture synthesizer
```

This distinguishes **task routing** (one model receives the entire task) from **capability allocation** (different cognitive resources receive different portions of one persistent task while writing to a common state). The latter is the stronger CRA interpretation.

---

# 18. Enterprise Runtime Architecture

## 18.1 Reference package

```text
cra/
├── contracts/
│   ├── task_contract.py
│   ├── authority_contract.py
│   └── resource_policy.py
├── comprehension/
│   ├── handshake.py
│   ├── interpretation.py
│   ├── fidelity_checker.py
│   └── clarification.py
├── workers/
│   ├── identity.py
│   ├── state.py
│   ├── checkpoint.py
│   └── handoff.py
├── capabilities/
│   ├── model_profile.py
│   ├── modality_profile.py
│   ├── qualification.py
│   └── history.py
├── routing/
│   ├── demand_estimator.py
│   ├── tier_policy.py
│   ├── model_selector.py
│   ├── verifier_selector.py
│   ├── hysteresis.py
│   └── switch_evaluator.py
├── execution/
│   ├── executor.py
│   ├── deterministic.py
│   ├── tool_adapter.py
│   └── model_adapter.py
├── validation/
│   ├── deterministic_checks.py
│   ├── semantic_checks.py
│   └── acceptance.py
├── evidence/
│   ├── event_store.py
│   ├── resource_ledger.py
│   └── provenance.py
├── policy/
│   ├── escalation.py
│   ├── deescalation.py
│   ├── provider_policy.py
│   └── security_policy.py
├── experiments/
├── runs/
├── schemas/
└── tests/
```

## 18.2 Event sourcing

Every consequential event is immutable:

```text
TASK_CREATED
INTERPRETATION_SUBMITTED
CONTRACT_ACCEPTED
MODEL_ASSIGNED
MODEL_ESCALATED
MODEL_DEESCALATED
MODEL_SWITCHED
CHECKPOINT_CREATED
VALIDATION_FAILED
TASK_ACCEPTED
```

Event sourcing provides replay; causal analysis; cost attribution; state reconstruction; routing evaluation; and security audit. BioDigital Jazz independently adopts the same event-sourced principle for project state, arguing that immutable state changes enable rollback, replay, and causal investigation.

---

# 19. Integration with SOVEREIGN, TCAIN, ATG, and BioDigital Jazz

CRA should not become another competing top-level architecture. It occupies a specific systems layer.

BioDigital Jazz defines a hierarchy in which human authority sets objectives, a project state and evidence plane records the evolving work, TCAIN generates adversarial pressure, ATG arbitrates project-level control, and the controlled autonomous system performs the actual bounded work. CRA fits primarily **inside the controlled execution system**, while exposing telemetry upward.

```text
HUMAN OPERATOR
      ↓
TRAJECTORY CONTRACT
      ↓
ATG
      ↓
TCAIN PRESSURE / PROJECT CONTROL
      ↓
SOVEREIGN CONTROLLED SYSTEM
      │
      ├── CRA TASK FORMATION
      ├── TCH
      ├── ACT
      ├── WORKERS
      └── MODEL / TOOL ALLOCATION
      ↓
ARTIFACTS + EVIDENCE
```

## 19.1 Relationship to TCAIN

TCAIN is represented as a high cognitive tier. CRA may escalate `Tier 2 specialist → Tier 3 reasoner → Tier 4 TCAIN node`. TCAIN therefore becomes expensive cognition invoked selectively rather than universal overhead.

## 19.2 Relationship to ATG

ATG asks: *is the project on course?* CRA asks: *what cognitive resource should perform the current work?* ATG may influence CRA indirectly by increasing criticality or requesting stronger verification. ATG does not micromanage specific model assignment.

## 19.3 Relationship to SOVEREIGN

SOVEREIGN owns canonical project state; worker identity; contract state; resource ledger; capability registry; evidence; routing history. CRA becomes the **cognitive scheduling subsystem**.

## 19.4 Relationship to the Multi-Model Workspace

The Workspace is the natural operator-facing surface for CRA. It can display:

```text
WORKER-07
Role: Backend Engineer
Task: Reconnect persistence

Task Contract: ACCEPTED
Current Tier: STANDARD
Generator: qwen-family coder
Verifier: deterministic test suite
Uncertainty: LOW
Routing Mode: ADAPTIVE
```

Later:

```text
ARCHITECTURAL CONTRADICTION DETECTED

Tier: STANDARD → ADVANCED
Reason: Test result contradicts session ownership assumption.
```

This turns automatic routing into inspectable engineering rather than invisible magic.

**Vocabulary mapping (normative pending the program charter; where terms conflict, the program term governs):** CRA *task contract* ↔ program *objective contract* (TCAIN); CRA *worker* ↔ *Sovereign node* (Workspace); CRA *validator* ↔ *gate / external validator*; CRA *handoff packet* ↔ *checkpoint / handoff snapshot* (SOVEREIGN convention); CRA *Tier-4 invocation* ↔ *TCAIN node launch*; CRA *cost to accepted work* ↔ unified evaluation plane *cost per accepted work*; TCH ↔ the *confirmation-file lifecycle* (operational ancestor).

---

# 20. Authority, Security, and Trust Boundaries

## 20.1 Model capability is not authority

A successor inherits the worker's permission envelope. Never `stronger model → stronger permissions`.

## 20.2 External content is data

Multimodal artifacts may contain malicious or misleading instructions. Images, PDFs, code comments, issue text, webpages, and logs are treated as untrusted content.

## 20.3 Security enforcement is external

Prompt instructions are not sufficient security controls. Filesystem, network, process, and credential restrictions must be enforced by the host execution layer. BioDigital Jazz reaches the same conclusion for high-impact autonomous use: model prompts may guide behavior, but operating-system permissions must enforce actual capability boundaries.

## 20.4 Model swap cannot expand authority

Formally:

```text
A(W, M_a) = A(W, M_b) = A_W
```

unless an authorized external policy mutation explicitly changes `A_W`.

---

# 21. Observability and Evidence Architecture

Each routing decision should answer:

```text
Why was this cognitive tier selected?
Why this generator, and why this verifier?
Why now?
Why was the previous allocation insufficient or excessive?
What did switching cost?
Did quality improve?
Did the worker preserve its contract?
```

A minimum routing record contains:

```yaml
routing_decision:
  task_id:
  worker_id:
  state_id:
  previous_tier:
  recommended_tier:
  selected_generator:
  selected_verifier:
  demand_vector:
  capability_match:
  triggers:
  alternatives_considered:
  estimated_switch_cost:
  operator_policy:
  confidence:
  timestamp:
```

The resulting history supports benchmarking; debugging; operator explanation; cost analysis; router calibration; and research.

---

# 22. Cognitive Economics and Resource Accounting

## 22.1 Wrong objective

The system must not optimize `min C_call`, because cheap calls can create expensive failures.

## 22.2 Correct economic object

```text
C_A = C_inference + C_compute + C_switch + C_validation
    + C_retry + C_rework + C_operator
```

where `C_A` is total cost to accepted work. The engineering objective:

```text
minimize  E[C_A]
subject to  P(Q >= Q_min) >= alpha
```

and all authority constraints. Quality binds **only** as a constraint; it does not also appear in the objective (double-counting quality in both a penalty and a constraint leaves the optimization underdetermined). Where a latency bound applies, it enters either as a declared wall-clock cost rate inside `C_A` or as a second constraint — one mechanism per deployment, declared in advance.

## 22.3 Cognitive waste

```text
W_C = C_actual − C_minimum_sufficient
```

The exact minimum cannot normally be observed directly; it is estimated through controlled counterfactual runs.

## 22.4 Under-tier cost

```text
C_U = C_rework + C_retry + C_delay
```

attributable to insufficient capability. CRA seeks a stable region between **over-tier** (too expensive) and **under-tier** (too unreliable).

---

# 23. Failure Analysis and Threat Model

- **23.1 False comprehension.** Worker mirrors conductor language without understanding. *Control:* require method, assumptions, scope, affected artifacts, completion condition; mechanical `H` checks (§11.4).
- **23.2 Conductor misunderstanding.** Worker correctly understands an incorrect conductor interpretation. *Control:* operator objective remains superior authority.
- **23.3 Router capture.** Routing model repeatedly favors itself or a preferred provider. *Control:* deterministic metrics, blinded capability evaluation, operator constraints.
- **23.4 Strong-model addiction.** Every uncertain state escalates permanently. *Control:* de-escalation, marginal-value measurement, cost accounting.
- **23.5 Cheap-model addiction.** Router pursues savings beyond the quality floor. *Control:* non-negotiable acceptance constraints (CRA-I12).
- **23.6 Tier thrashing.** Frequent switches waste resources and destroy continuity. *Control:* hysteresis, minimum residency, switch penalties (§15.2).
- **23.7 Premature de-escalation.** Capability lowered before uncertainty resolves. *Control:* the P6/CRA-I9 deterministic-validation rule.
- **23.8 Escalation failure.** Weak model persists despite insufficiency. *Control:* worker-requested and validator-triggered escalation.
- **23.9 Capability-profile error.** Benchmark profile does not predict real work. *Control:* continual comparison of expected versus observed performance.
- **23.10 Capability-profile staleness.** Version, quantization, prompt, or runtime changes behavior. *Control:* deployment-specific, versioned profiles (§14.3).
- **23.11 Handoff omission.** Critical decision or constraint disappears during substitution. *Control:* canonical handoff schema and successor acknowledgement. (Observed live during this document's own preparation; §5.5.)
- **23.12 Handoff poisoning.** Outgoing model misrepresents state. *Control:* build handoff from canonical state and deterministic telemetry where possible rather than trusting self-summary alone.
- **23.13 Successor reinterpretation.** New model reopens accepted decisions without new evidence. *Control:* frozen decisions vs. unresolved issues (§16.2).
- **23.14 Modality misrouting.** Vision-heavy work routed to a model with weak visual reliability. *Control:* modality-specific qualification.
- **23.15 Provider outage.** Selected resource becomes unavailable. *Control:* equivalent-tier fallback.
- **23.16 Privacy violation.** Adaptive router sends local-sensitive work to a frontier provider. *Control:* provider policy as a hard pre-routing filter.
- **23.17 Budget starvation.** Early over-tiering consumes resources needed later. *Control:* remaining-budget state in routing.
- **23.18 Metric gaming.** Router optimizes its own score rather than accepted work. *Control:* hidden evaluation, counterfactual trials, multi-dimensional outcomes.
- **23.19 Evaluation circularity.** The same model family routes, executes, and evaluates itself. *Control:* evaluator independence (§28.5).
- **23.20 Bureaucratic overhead.** TCH and ACT make simple work slower. *Control:* compare against direct execution; bypass for lightweight reversible work.
- **23.21 Self-assessment manipulation.** A worker games self-reporting — claiming uncertainty to shed tasks or attract budget, or confidence beyond capability. The incentive cuts both ways: if disclosed uncertainty triggers reassignment, honest disclosure is punished; if it attracts resources, it is rewarded. *Control:* self-assessment is one signal among deterministic, historical, and external indicators (CRA-I5), and escalation precision is audited per worker.

The overarching enterprise risk mirrors the principal BioDigital Jazz risk: a mechanism introduced to improve control can become a source of cost, delay, and self-justifying complexity. Such layers must be measured against simpler baselines and removed if they fail to earn their cost (P10).

---

# 24. Experimental Program

## 24.1 Evaluation principle

CRA is not validated by elegant routing diagrams, successful demonstrations, anecdotal cost savings, one favorable benchmark, or model agreement. It must outperform simpler allocation policies under controlled comparison. This follows the same experimental discipline adopted by BioDigital Jazz: sophisticated architecture is not evidence unless matched-budget comparisons demonstrate an advantage.

## 24.2 Conditions

- **C0: Strongest Fixed Model** — one highest-capability permitted model performs the full task.
- **C1: Cheapest Fixed Model** — one low-cost model performs the full task.
- **C2: Static Specialist** — a competent specialist selected at task start, fixed.
- **C3: Static Tiered Pipeline** — predefined stage tiers without adaptive reassessment.
- **C4: TCH Only** — comprehension validated; allocation fixed.
- **C5: ACT Only** — adaptive routing without the handshake.
- **C6: ACT + TCH** — full allocation without persistence/handoff machinery.
- **C7: Full CRA** — TCH + ACT + persistent worker identity + structured handoff.
- **C8: CRA + Deep Tier** — CRA may escalate to multi-model/TCAIN reasoning.

## 24.3 Minimal publishable unit and priority ordering

The full grid — nine conditions, seventeen ablations, ten hypotheses, four domains, live branching — exceeds any single-operator resource envelope. The full grid is the aspiration register; the following is the binding plan.

**Minimal publishable unit (preregistered):**

- one task domain: bounded software repair (deterministic test acceptance);
- conditions **C0, C1, C7**;
- core ablations **A1, A12, A13** (§30);
- experiment order per the keystone structure (§25.11): **H6 first** (handoff; cheapest, two local models, no router), **H7 concurrent** (observational telemetry; no dedicated condition needed), then H1, then H2/H3;
- pilot of 10–15 tasks for variance estimation, then a powered main run;
- live branching at 2–3 checkpoints on a preregistered task subset, with same-model control forks;
- primary comparisons: C7 vs. C0 (cost, with quality non-inferiority) and A12 vs. C7 (handoff).

Everything beyond this is expansion, contingent on the minimal unit's results.

---

# 25. Research Hypotheses and Keystone Structure

## 25.1–25.10 Hypotheses

- **H1: Comprehension.** Decomposed: **H1a** — TCH detects materially incorrect pre-execution interpretations (seeded and naturally occurring) at a rate exceeding its false-positive burden, relative to direct assignment (C4/C7 vs. C0–C3). **H1b** — restatement quality at handshake time predicts execution-time compliance (scope violations, constraint breaches) — a distinct and weaker claim, stated separately because restatement is not compliance (§11.7).
- **H2: Cost efficiency.** C7 reduces total cost per accepted task relative to C0 without materially reducing accepted-task quality.
- **H3: Dynamic allocation.** C7 outperforms C2 and C3 on tasks containing deliberately changing cognitive demand.
- **H4: Escalation recovery.** Adaptive escalation reduces repeated failure compared with fixed lower-tier execution.
- **H5: De-escalation efficiency.** Adaptive de-escalation reduces unnecessary high-tier resource consumption.
- **H6: Worker continuity.** Persistent worker identity with structured handoff outperforms worker reset after model substitution. Control arms pinned to the three-arm design: structured packet (C7) vs. raw transcript (A12) vs. reset (A13).
- **H7: TCH predictive value.** Handshake telemetry predicts downstream failure, escalation, and rework beyond initial task-family labels.
- **H8: Capability routing.** Multidimensional capability profiles outperform model-size or generic-rank routing.
- **H9: Multimodal specialization.** Capability decomposition improves accepted cost-quality performance on mixed-modality tasks compared with a single generalist model.
- **H10: Deep-tier selectivity.** Selective escalation to multi-model reasoning achieves better efficiency than invoking deep orchestration on every task.

## 25.11 Keystone structure and dependency ordering

The hypotheses are not peers; they form a dependency tree, and the architecture's viability hangs on two of them.

**H6 is a precondition, not a result.** If structured handoff does not preserve worker state across substitution, H2–H5 are untestable — every switch destroys the trajectory being optimized. The Replay Gap sets the adversarial prior: swaps rewrote 61–94% of post-fork actions in live branching. The null position is that switching is disruptive by default; the handoff mechanism must demonstrably tame it. H6 is accordingly the **first experiment** — also the cheapest, requiring two local models and no router.

**H7 is the keystone.** Nearly every escalation signal in the architecture is a *lagging* indicator — the system learns the task is hard by paying for failure first. The only *leading* indicator is comprehension telemetry from the handshake. If H7 fails, ACT possesses no leading signal, escalation reduces to escalation-on-failure, and the architecture degenerates into a cascade with checkpoints — territory already occupied by FrugalGPT and AutoMix. CRA's residual novelty would shrink to bidirectionality plus persistence bookkeeping. This is stated plainly here, and recorded as a falsification condition (§31), because a research program should know in advance which single result would hollow it out.

H7 is also **observational and nearly free**: collect the interpretation on every task *without gating on it*, then correlate handshake telemetry with downstream escalation, rework, and outcome. No router required. It is therefore the first CRA result obtainable, concurrent with H6.

**H1–H5 and H8–H10 are payoff hypotheses**, testable only after the preconditions hold. Resulting order:

```text
H6 (handoff) → H7 (observational telemetry) → H1a (TCH ablation) → H2/H3/H4/H5 (routing)
```

**Hypothesis → condition → evidence map:**

| Hypothesis | Tested by | Evidence form | Priority |
|---|---|---|---|
| H6 continuity | A12/A13 vs. C7; live branching | Post-switch divergence, state-loss errors | **First** (precondition) |
| H7 telemetry | Observational, all runs | TCH telemetry → escalation/rework correlation | **First** (keystone) |
| H1a detection | A1 vs. C4; seeded misinterpretations | Detection rate vs. false-positive burden | Second |
| H1b prediction | Observational | Restatement quality → compliance correlation | Second |
| H2 efficiency | C7 vs. C0 | Cost per accepted task at quality non-inferiority | Third |
| H3 dynamic | C7 vs. C2/C3 | Non-stationary task outcomes | Third |
| H4 escalation | C7 vs. C1 | Rework, under-tier failure | Third |
| H5 de-escalation | C7 vs. C0, tier-residency analysis | Cost, cognitive waste | Third |
| H8 capability routing | A7 | Deferred | Deferred |
| H9 multimodal | Phase 9 program | Deferred | Deferred |
| H10 deep tier | C8 vs. C7 | Deferred | Deferred |

---

# 26. Primary Metrics

- **Accepted Completion Rate** — fraction of tasks satisfying all critical contract conditions.
- **Cost per Accepted Task** — `CPA = (sum of C_A) / N_accepted`.
- **Comprehension Error Rate** — fraction of initial worker interpretations containing material contract errors.
- **Scope Violation Rate** — unauthorized work relative to contract.
- **Rework Rate** — work discarded or redone because of execution or allocation failure.
- **Escalation Precision** — fraction of escalations producing measurable downstream benefit.
- **Escalation Recall** — capability-attributable failures preceded by escalation. **Attribution rule:** a failure is capability-attributable when a subsequent escalation *with no other intervention* — same contract, same state, same tools — resolves it.
- **De-Escalation Precision** — fraction of de-escalations completing without capability-driven re-escalation.
- **State Preservation Rate** — fraction of critical worker state preserved across model transitions.
- **Operator Burden** — number and duration of human interventions.

---

# 27. Secondary Metrics

Contract revision count; ambiguity detection; constraint recall; switch frequency; switch latency; post-switch divergence; tier residence time; cognitive waste; under-tier failure cost; model-family sensitivity; modality-routing accuracy; validator disagreement; token cost; GPU time; local/cloud utilization; task latency; router confidence calibration.

---

# 28. Statistical and Evaluator Methodology

## 28.1 Pre-registration

Before definitive runs, freeze: task corpus; model versions and serving configurations (including quantization, §14.3); sampling; routing rules; capability profiles; primary comparison; success criteria; exclusion rules; stopping rules.

## 28.2 Power

A pilot estimates variance; definitive task count follows power analysis. No threshold such as "5% improvement" is scientifically meaningful without demonstrating that the experiment can distinguish it from noise. **Effect-size priors:** MetaCogAgent's 8.7% routing gain over its best baseline for cost/accuracy effects; the Replay Gap's divergence magnitudes for switch-disruption effects. Non-inferiority testing on quality requires more power than superiority testing on cost; the pilot must size for the former.

## 28.3 Pairing

The same tasks should be attempted under multiple conditions where feasible.

## 28.4 Evaluator hierarchy

Prefer, in order: deterministic tests; artifact invariants; objective measurements; blinded human evaluation; model judges.

## 28.5 Judge independence

Where model judging is unavoidable: hide contestant identity; randomize order; use lineage-disjoint judges where possible; use multiple judges; retain disagreement; calibrate against known-answer tasks. These requirements apply equally to the conductor's comprehension judgments (§11.7), which are logged and audited against outcomes.

## 28.6 Multiple hypotheses

Secondary findings require multiplicity correction. The paper should not transform twenty measured dimensions into twenty independent chances to declare victory.

---

# 29. Live Model-Switch Experiment

Because switching changes trajectories, CRA requires branching rollouts, never static log-stitching. At a selected state:

```text
               STATE S_t
                  │
        ┌─────────┼─────────┐
        │         │         │
   retain M_A  switch M_B  retain M_A
        │         │        (control fork,
        ▼         ▼         fresh sampling)
    branch A   branch B    branch A'
```

All branches inherit the same filesystem state, task contract, evidence, budget, and checkpoint. **Same-model control forks are mandatory** — without them, swap effects cannot be separated from sampling and replay noise; this is the Replay Gap protocol, and its FP8/AWQ finding shows the noise floor itself is serving-configuration-dependent and must be measured, not assumed.

Measured: action divergence; artifact divergence; result quality; cost; constraint preservation; completion.

---

# 30. Ablations

Remove or modify one mechanism at a time.

**Core (required for the minimal publishable unit):**

- **A1** — No handshake (direct assignment; tests TCH; maps to H1a).
- **A12** — Transcript handoff instead of structured handoff (maps to H6).
- **A13** — Reset worker identity on swap (maps to H6, three-arm design).

**Deferred (contingent on minimal-unit results; rationale retained so deferral is a resourcing decision, not a deletion):**

- A2 — simple restatement only; A3 — no assumption disclosure; A4 — no forbidden-scope field; A5 — no self-reported uncertainty; A6 — no historical capability information; A7 — model-size routing only (maps to H8); A8 — escalation only; A9 — de-escalation only; A10 — no hysteresis (measures thrashing); A11 — no switch-cost model; A14 — no deterministic telemetry in routing; A15 — no resource budget; A16 — no multimodal specialization; A17 — always invoke deep tier (maps to H10).

---

# 31. Falsification Conditions

The central thesis is weakened if:

- TCH adds overhead without reducing consequential misunderstanding;
- C7 does not lower cost to accepted work relative to competent static assignment;
- quality falls materially under adaptive de-escalation;
- switching creates unacceptable state loss;
- structured handoff performs no better than transcript transfer;
- cognitive-demand measures do not predict task difficulty;
- capability profiles fail to generalize even within fixed deployment configurations;
- adaptive routing merely shifts cost into retries and validation;
- full CRA only wins because it consumes more compute;
- benefits disappear outside one model family;
- human intervention increases rather than decreases;
- short and long tasks show no meaningful difference in CRA utility.

**Keystone failure (Null H):** H6 and H7 both fail. CRA then degenerates into cascade routing with persistence bookkeeping, and its residual contribution is limited to the contract and authority layer. This outcome would be published as such, under that description.

Negative findings should narrow the system. They should not be explained away by adding another architecture layer.

---

# 32. Enterprise Validation Program

Scientific validity and production validity are related but different. Enterprise CRA additionally requires proof of:

- **EV-1 Reproducibility** — the same run manifest reconstructs the same configuration.
- **EV-2 Recovery** — worker state survives application restart.
- **EV-3 Provider failure** — loss of the current model does not destroy task identity.
- **EV-4 Policy integrity** — adaptive routing cannot cross provider or privacy limits.
- **EV-5 Authority integrity** — model switching cannot increase permissions.
- **EV-6 Cost ceilings** — hard resource ceilings are enforced.
- **EV-7 State lineage** — every accepted artifact is traceable to worker, models, prompts, tools, evidence, and validation.
- **EV-8 Clean fallback** — adaptive mode can be disabled; manual/static execution remains available.
- **EV-9 Long-duration operation** — routing state and worker continuity remain valid over extended projects.
- **EV-10 Security review** — prompt injection, handoff poisoning, provider leakage, and privilege inheritance are independently tested.

---

# 33. Engineering Sequence

- **Phase 0: Contract the experiment.** Freeze schemas, hypotheses, baselines, evidence requirements.
- **Phase 1: Task-Comprehension Handshake.** Task packet; interpretation; acceptance; revision; operator clarification. No adaptive routing yet.
- **Phase 2: Persistent worker identity.** Move worker state outside model sessions. *(Substrate note: the Workspace's governed node runtime already supplies identity, authority envelopes, leases, and supervised lifecycle; §5.5.)*
- **Phase 3: Manual cognitive tiers.** LIGHT / STANDARD / ADVANCED / DEEP with manually assigned models. *(MANUAL mode is operational on the substrate.)*
- **Phase 4: Structured handoff.** Test model substitutions while routing remains manual. **This phase produces the H6 result.**
- **Phase 5: Instrumented demand estimator.** Collect ambiguity; failures; dependency counts; uncertainty; artifact changes; task family; historical model performance. Recommendations only — no autonomous swaps. **Telemetry collection here produces the H7 observational result.**
- **Phase 6: Assisted routing.** Operator approves tier changes.
- **Phase 7: Adaptive escalation.** Automatic upward movement on proxy triggers.
- **Phase 8: Adaptive de-escalation.** Conservative downward routing under P6/CRA-I9, with hysteresis and minimum residency.
- **Phase 9: Multimodal allocation.** Modality-aware decomposition.
- **Phase 10: Deep cognitive tier.** Integrate TCAIN or equivalent high-cost reasoning.
- **Phase 11: Controlled experimental program.** Run the minimal publishable unit first (§24.3), then C0–C8 and remaining ablations as resources permit.
- **Phase 12: Enterprise hardening.** Only after measured value: packaging; deployment; security; monitoring; failover; documentation.

---

# 34. Product and Operational Implications

If validated, CRA changes the definition of a multi-model workspace.

Without CRA: *a workspace allows the operator to access several AI models.*

With CRA: **a workspace maintains persistent AI workers and dynamically allocates appropriate machine cognition to them according to the evolving demands of the work.**

That is a materially stronger systems category. The operator views a worker as:

```text
WORKER-12
Role: Systems Engineer
Objective: Resolve persistent-session race

State: EXECUTING
Contract: ACCEPTED
Tier: STANDARD
Generator: Local coding specialist
Verifier: Targeted test suite
```

Later:

```text
REASONING ESCALATION

Trigger: Two contradictory runtime traces invalidate
the current ownership assumption.

Tier: STANDARD → ADVANCED
Worker identity: UNCHANGED
```

Later:

```text
ARCHITECTURE RESOLVED

Tier: ADVANCED → STANDARD
Reason: Remaining mutations are bounded and
deterministically testable.
```

The visible object is the worker. The model becomes infrastructure. A further product consequence follows from §15.2: the high-switching-cost regime CRA characterizes — serial hosting, constrained VRAM — describes the deployment reality of most private and on-premise operators, and is unstudied by laboratories for whom switching is nearly free.

---

# 35. Enterprise Use Cases

- **Software engineering** — architecture discovery; repository migration; bug repair; release preparation; long-running implementation.
- **Scientific research** — literature analysis; hypothesis management; simulation review; evidence synthesis.
- **Cybersecurity** — log analysis; code inspection; threat modeling; remediation design.
- **Data systems** — schema work; pipeline debugging; data quality investigation.
- **Multimodal engineering** — UI screenshots plus source code; schematics plus documentation; video plus telemetry; reports plus data.
- **Regulated technical work** — where local deployment, auditable state, model provenance, and human acceptance are required.

---

# 36. Relationship to the Broader Cognitive Systems Thesis

BioDigital Jazz describes intelligence as the controlled evolution of a project from human input to accepted output, with state transitions, evidence, adversarial pressure, and external trajectory control rather than a single prompt-to-answer inference.

CRA adds a lower-level proposition:

> **If intelligence is expressed through the controlled evolution of work, then the computational intelligence used to produce each transition should itself be dynamically allocated according to the requirements of that transition.**

The theses operate at complementary levels:

```text
BioDigital Jazz:  What trajectory should the project follow?
CRA:              What cognition should power this part of that trajectory?
TCAIN:            When ordinary cognition is insufficient,
                  how should deeper adversarial reasoning occur?
ATG:              When should the project be corrected?
SOVEREIGN:        What persistent system owns the state,
                  evidence, continuity, and authority boundaries?
```

Together:

```text
HUMAN INTENT → PROJECT TRAJECTORY → TASK CONTRACT
            → COGNITIVE RESOURCE ALLOCATION → WORKER EXECUTION
            → EVIDENCE → TRAJECTORY EVALUATION → ACCEPTED OUTPUT
```

---

# 37. Limitations

- **37.1** Cognitive capability is difficult to measure; benchmarks incompletely represent deployment competence.
- **37.2** Task difficulty is partially latent; the system may not know a task is hard until it fails.
- **37.3** Switching can itself be harmful; a more capable model may create a different, worse trajectory.
- **37.4** Model identity matters; different models do not behave like interchangeable CPU cores.
- **37.5** Structured state may omit subtle context; handoff compression can erase information.
- **37.6** Cost models change; provider pricing, hardware efficiency, and latency shift over time.
- **37.7** Multimodal capability is highly nonuniform.
- **37.8** Enterprise success is domain dependent; CRA may help long-horizon software tasks while harming short routine workloads.
- **37.9** Human-defined contracts can be wrong; comprehension alignment does not guarantee objective correctness.
- **37.10** Increased observability creates increased engineering complexity; CRA may be too expensive to justify in some environments.

---

# 38. Findings

## 38.1 Known facts

- Adaptive computation and conditional expert activation established that computational resources need not be applied uniformly.
- Model-routing research demonstrated meaningful cost-quality tradeoffs between heterogeneous LLMs.
- Metacognitive delegation provides recent precedent for capability self-assessment and historical competence in task assignment.
- Live model switching can substantially alter downstream agent behavior — 61–94% of post-fork actions rewritten in controlled branching — making model-transition engineering a genuine trajectory problem rather than an API substitution.

## 38.2 Architectural findings

- Worker identity can be logically separated from model identity.
- TCH and ACT solve different but complementary problems.
- Handshake information is potentially useful routing telemetry — and it is the architecture's only leading indicator.
- Bidirectional tiering is more general than escalation-only cascades.
- Allocation as generator-verifier pairs subsumes single-occupant tiering.
- Deep multi-model reasoning functions naturally as a high cognitive tier.
- The architecture fits inside SOVEREIGN rather than requiring another independent control plane.
- The Multi-Model Workspace is the natural operator surface.

## 38.3 Assumptions

- Persistent state can represent a task sufficiently well to survive model substitution.
- Model capability profiles can provide useful routing information.
- Semantic comprehension can be measured well enough to prevent some execution errors.
- Routing benefit can exceed switching overhead on sufficiently complex work.

## 38.4 Unknowns

Optimal tier granularity; optimal switching threshold; minimum profitable task horizon; required handoff detail; router generalization; model-self-assessment reliability; relative value of capability specialization versus raw model strength.

## 38.5 Principal engineering risk

The largest risk is that cognitive scheduling becomes more complex than the work it schedules. If CRA introduces excessive handshakes, frequent model swaps, large state packets, expensive validators, and router bureaucracy without improving accepted-output economics, it has failed its own thesis.

## 38.6 Overall finding

CRA is **conceptually coherent, technically implementable, experimentally falsifiable, and architecturally compatible with the broader Sovereign research program**. It is not yet experimentally demonstrated. Its value will be determined by whether it can produce **equal or better accepted work, with lower total cognitive resource cost and lower semantic execution error, than competent static model assignment** — and its two load-bearing results, handoff preservation and telemetry prediction, are the cheapest experiments in the program.

---

# 39. Conclusion

The central assumption behind many current AI systems is that a model is the operative unit of intelligence. Cognitive Resource Allocation proposes a different systems abstraction.

The persistent unit is the **work**. The persistent computational identity is the **worker**. The worker carries objective, contract, authority, evidence, history, and state. A model temporarily contributes cognition to that worker.

If the task becomes harder, the resource can escalate. If the task becomes routine, it can de-escalate. If a different modality emerges, it can specialize. If one model fails, another can assume the role. If uncertainty becomes high enough, a multi-model adversarial system can be invoked. The task itself survives all of those changes.

The complete CRA cycle:

```text
UNDERSTAND → CONTRACT → ASSESS → ALLOCATE → EXECUTE → OBSERVE
           → REASSESS → ESCALATE / DE-ESCALATE / SPECIALIZE
           → HAND OFF → VALIDATE → ACCEPT
```

The broader proposition is not *use cheap models whenever possible*, nor *always escalate hard problems to the biggest model*. It is:

> **Allocate the least costly cognitive capability that is demonstrably sufficient for the current state of the work, increase that capability when evidence shows insufficiency, decrease it only where acceptance is deterministically checkable, and preserve the worker's identity and authority independently of whichever models currently supply the cognition.**

Traditional computing systems schedule processors. Distributed systems schedule machines. Cloud systems schedule containers. CRA proposes that heterogeneous AI systems schedule **cognition**.

The final scientific obligation is not another architectural description. It is implementation followed by controlled comparison — beginning with the two experiments this document identifies as load-bearing and cheap. If CRA survives that comparison, it provides a principled systems layer between durable autonomous work and the rapidly changing population of models capable of performing it. If it fails, the failure will establish useful boundaries around model substitution, semantic contracting, adaptive routing, and the degree to which artificial cognitive resources can actually be treated as interchangeable infrastructure.

Either result is research.

---

# Appendix A. Canonical Task Contract

```yaml
task_contract:
  task_id: ""
  version: 1
  worker_id: ""

  objective:
    statement: ""
    required_outputs: []

  success_conditions: []

  scope:
    in_scope: []
    out_of_scope: []
    forbidden_actions: []

  constraints:
    hard: []
    soft: []

  artifacts:
    relevant: []
    expected_mutations: []

  assumptions: []

  authority:
    filesystem: ""
    network: ""
    tools: []
    external_side_effects: false
    promotion: false

  resource_policy:
    routing_mode: adaptive
    local_only: false
    allowed_providers: []
    max_tier: 4
    max_cost: null

  completion:
    acceptance_authority: ""
    critical_criteria: []

  status: CONTRACT_PENDING
```

# Appendix B. Worker Comprehension Report

```yaml
worker_comprehension:
  task_id: ""
  worker_id: ""

  interpreted_objective: ""
  expected_output: ""

  intended_method: []

  interpreted_constraints: []
  interpreted_forbidden_scope: []

  artifacts_expected_to_touch: []

  assumptions: []
  ambiguities: []
  risks: []

  expected_completion_condition: ""

  self_assessment:
    complexity: null
    uncertainty: null
    capability_sufficient: null
    specialist_required: []

  acknowledgement:
    authority_understood: false
    scope_understood: false
```

# Appendix C. Routing Decision Record

```yaml
routing_decision:
  routing_id: ""
  task_id: ""
  worker_id: ""
  state_id: ""

  current:
    tier: null
    generator: ""
    verifier: ""

  demand:
    reasoning: null
    coding: null
    vision: null
    context: null
    uncertainty: null
    criticality: null
    novelty: null
    reversibility: null

  recommendation:
    action: KEEP
    target_tier: null
    target_generator: ""
    target_verifier: ""

  triggers: []
  alternatives_considered: []

  hysteresis:
    consecutive_failures: null
    consecutive_clean_checkpoints: null
    residency_elapsed: null
    minimum_residency_met: null

  economics:
    expected_switch_cost: null
    expected_remaining_cost_current: null
    expected_remaining_cost_target: null

  policy_check:
    provider_allowed: false
    budget_allowed: false
    authority_unchanged: true
    deterministic_validation_available: null   # required true for DE_ESCALATE

  confidence: null
  timestamp: ""
```

# Appendix D. Cognitive Handoff Packet

```yaml
cognitive_handoff:
  handoff_id: ""
  worker_id: ""
  task_id: ""

  from_model: ""
  to_model: ""

  contract_hash: ""
  state_hash: ""

  completed_actions: []
  current_artifacts: []

  verified_facts: []
  accepted_decisions: []      # frozen; reopening requires new evidence
  rejected_decisions: []

  assumptions: []
  unresolved_issues: []       # open; successor may engage
  failed_attempts: []

  evidence_refs: []

  current_plan: []
  next_expected_action: ""

  authority:
    permissions: []

  resource_state: {}

  successor_acknowledgement:
    objective: ""
    next_action: ""
    invariants: []
    unresolved_issues: []
    accepted: false
```

# Appendix E. Capability Profile

```yaml
capability_profile:
  profile_id: ""
  provider: ""
  model: ""
  version: ""
  quantization: ""
  runtime: ""

  capabilities:
    general_reasoning: null
    coding: null
    debugging: null
    architecture: null
    synthesis: null
    critique: null
    vision: null
    audio: null
    long_context: null
    schema_compliance: null
    tool_use: null
    evidence_fidelity: null

  operational:
    latency: null
    throughput: null
    memory_requirement: null
    monetary_cost: null

  reliability:
    task_success: null
    retry_rate: null
    scope_violation_rate: null
    handoff_failure_rate: null

  evidence:
    benchmark_runs: []
    live_runs: []

  last_qualified: ""
```

# Appendix F. Minimum Run Manifest

```yaml
run_manifest:
  run_id: ""
  task_id: ""
  experimental_condition: ""

  task_contract_hash: ""
  initial_state_hash: ""

  workers: []

  models:
    - worker_id: ""
      provider: ""
      model: ""
      version: ""
      quantization: ""
      serving_stack: ""
      base_lineage: ""
      capability_profile_hash: ""

  routing_policy:
    version: ""
    content_hash: ""

  prompts:
    - role: ""
      content_hash: ""

  tools: []

  budgets:
    tokens: null
    wall_clock: null
    monetary_cost: null

  routing_events: []
  model_switches: []
  checkpoints: []

  validation:
    deterministic: []
    human: []
    model_judges: []

  output_artifacts: []
  evidence_artifacts: []

  final_status: ""
```

# Appendix G. Canonical Event Envelope

```yaml
event:
  event_id: ""
  event_type: ""
  project_id: ""
  task_id: ""
  worker_id: ""
  run_id: ""

  parent_state_hash: ""
  resulting_state_hash: ""

  actor:
    role: ""
    model: ""

  authority_class: ""

  payload: {}

  evidence_refs: []

  resource_usage:
    tokens: null
    latency: null
    cost: null

  timestamp: ""
```

# Appendix H. Canonical Claim Ledger

```yaml
claim_ledger:

  - claim_id: CRA-K001
    class: known_fact
    statement: >
      Conditional computation and model routing have established
      precedent for dynamically allocating computational capability.
    evidence_refs: [Graves 2016, Shazeer 2017, Chen 2023, Ong 2024]
    status: supported

  - claim_id: CRA-K002
    class: known_fact
    statement: >
      Live model substitution rewrites the majority of post-switch
      agent actions and cannot be evaluated by static replay.
    evidence_refs: [Gonuguntla 2026]
    status: supported

  - claim_id: CRA-A001
    class: architectural_interpretation
    statement: >
      Worker identity can be represented independently of model identity.
    evidence_refs: []
    status: proposed

  - claim_id: CRA-H001
    class: hypothesis
    statement: >
      Task-Comprehension Handshake will reduce material task
      misunderstanding relative to direct assignment.
    experiment: H1
    status: untested

  - claim_id: CRA-H002
    class: hypothesis
    statement: >
      Adaptive Cognitive Tiering will lower total cost to accepted
      work while maintaining required quality.
    experiment: H2
    status: untested

  - claim_id: CRA-H006
    class: hypothesis
    role: precondition
    statement: >
      Structured handoff preserves worker continuity across model
      substitution better than transcript transfer or worker reset.
    experiment: H6
    status: untested

  - claim_id: CRA-H007
    class: hypothesis
    role: keystone
    statement: >
      Handshake telemetry predicts downstream difficulty, escalation,
      and rework. Failure of this claim degenerates ACT into cascade
      routing (Null H).
    experiment: H7
    status: untested

  - claim_id: CRA-U001
    class: unknown
    statement: >
      The minimum task horizon at which CRA produces positive
      net value is unknown.
    status: open
```

# Appendix I. Canonical Definition

**Cognitive Resource Allocation (CRA)** is a stateful orchestration architecture in which persistent AI workers operate under explicit task contracts and are dynamically assigned heterogeneous cognitive resources — as generator-verifier pairs — according to evolving task complexity, uncertainty, criticality, modality, execution performance, resource availability, and operator policy.

**Task-Comprehension Handshake (TCH)** is the bounded pre-execution protocol through which a worker demonstrates its interpretation of objective, output, constraints, prohibited scope, assumptions, authority, method, and completion criteria before consequential execution begins.

**Adaptive Cognitive Tiering (ACT)** is the bidirectional routing mechanism that increases, decreases, specializes, or replaces the cognitive capability assigned to that worker — with de-escalation permitted only into deterministically checkable or independently validated regions — while preserving the worker's task state and authority independently of the model.

The canonical systems principle:

> **The objective persists.
> The work persists.
> The worker persists.
> The evidence persists.
> The authority persists.
> The model is replaceable.**

---

# References

- Aggarwal, P., et al. (2023). *AutoMix: Automatically Mixing Language Models.* arXiv:2310.12963. Reliability-informed escalation using self-verification by the smaller model.
- Chen, L., Zaharia, M., & Zou, J. (2023). *FrugalGPT: How to Use Large Language Models While Reducing Cost and Improving Performance.* arXiv:2305.05176. LLM cascades as cost-performance optimization.
- Du, Y., Li, S., Torralba, A., Tenenbaum, J. B., & Mordatch, I. (2023). *Improving Factuality and Reasoning in Language Models through Multiagent Debate.* arXiv:2305.14325.
- Gonuguntla, A. (2026). *The Replay Gap: Static Evaluation of Model Switching in LLM Agents Scores the Wrong World.* arXiv:2608.08239. Live branching on SWE-bench trajectories; swaps rewrite 61–94% of post-fork actions; static replay mispredicts every success-relevant outcome; serving-configuration-dependent determinism (FP8 vs. AWQ).
- Graves, A. (2016). *Adaptive Computation Time for Recurrent Neural Networks.* arXiv:1603.08983.
- Madaan, A., et al. (2023). *Self-Refine: Iterative Refinement with Self-Feedback.* arXiv:2303.17651.
- Ong, I., et al. (2024). *RouteLLM: Learning to Route LLMs with Preference Data.* arXiv:2406.18665.
- Ramírez, G., Birch, A., & Titov, I. (2024). *Optimising Calls to Large Language Models with Uncertainty-Based Two-Tier Selection.* Uncertainty-driven routing between differently capable models.
- Shazeer, N., et al. (2017). *Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer.* arXiv:1701.06538.
- Shinn, N., et al. (2023). *Reflexion: Language Agents with Verbal Reinforcement Learning.* arXiv:2303.11366.
- Smith, R. G. (1980). *The Contract Net Protocol: High-Level Communication and Control in a Distributed Problem Solver.* IEEE Transactions on Computers, C-29(12), 1104–1113.
- Srivastava, A., Khojastepour, M. A., Chakradhar, S., & Ulukus, S. (2026). *RunAgent: Interpreting Natural-Language Plans with Constraint-Guided Execution.* arXiv:2605.00798.
- Starmer, A. J., et al., for the I-PASS Study Group (2014). *Changes in Medical Errors after Implementation of a Handoff Program.* New England Journal of Medicine, 371, 1803–1812. Structured shift-handoff bundle reducing medical errors; empirical grounding for structured state transfer between agents.
- Wang, C., & Shu, Y. (2026). *MetaCogAgent: A Metacognitive Multi-Agent LLM Framework with Self-Aware Task Delegation.* arXiv:2605.17292. 82.4% task accuracy, +8.7% over best routing baseline; used here as an effect-size prior.
- Wang, J., et al. (2024). *Mixture-of-Agents Enhances Large Language Model Capabilities.* arXiv:2406.04692.
- Xu, X., et al. (2026). *RoadmapBench: Evaluating Long-Horizon Agentic Software Development Across Version Upgrades.* arXiv:2605.15846. 115 tasks, 17 repositories, 5 languages; median modification ~3,700 lines across 51 files; strongest evaluated model resolves 39.1%.

**Program reference:** *The Evolution of Intelligence from Input to Output: BioDigital Jazz* — the ATG-TCAIN trajectory-control framework whose epistemic-status discipline, state/evidence architecture, matched-budget experimental requirement, failure analysis, and run-manifest approach serve as architectural compatibility references in this thesis.
