# Cognitive Resource Allocation for Heterogeneous AI Systems

## Adaptive Cognitive Tiering and Task-Comprehension Handshakes for Stateful Multi-Model Execution

**Research Thesis and Experimental Prospectus**

- **Version:** 0.2
- **Author:** Samuel Lawson — Sovereign Systems Research Program, Dark Science Division
- **Status:** Archived prior edition — fully superseded by the v1.0 Research Baseline at the repository root. Conceptual architecture and experimental prospectus; no empirical performance claim prior to controlled testing.
- **License:** CC BY-NC-ND 4.0
- **Research domain:** Multi-model artificial intelligence, agent orchestration, adaptive computation, distributed problem solving, cognitive systems engineering
- **Revision note:** v0.2 incorporates an independent validation pass — citation verification against primary sources, formal corrections, and structural revisions — per the program's standing multi-model review convention.

---

## Change Log: v0.1 → v0.2

1. All mathematical notation converted to plain-text form, eliminating the unrendered-markup defect class present throughout v0.1.
2. **Hysteresis transition condition corrected.** v0.1 omitted the inequality operator. The condition is `B_switch > C_switch + delta` (§20).
3. **Routing objective reformulated.** v0.1 double-counted quality in both a penalty term and a chance constraint. Quality now binds only as a constraint; cost is the objective (§16).
4. **Keystone-hypothesis analysis added** (§27). The hypotheses form a dependency structure, not a flat list. H8/H5 are preconditions; H6 is the keystone; the degeneration risk if the keystone fails is stated plainly, and recorded as Null H (§48).
5. **Cognitive demand estimation specified** (§11). Phase 1 demand signals are deterministic runtime measurements plus handshake telemetry. Model self-report is never the sole source. No learned router exists before Phase 3.
6. **CRA-I9 sharpened into an operational rule** (§19, §43): de-escalation is permitted only into task regions whose acceptance is deterministically checkable or independently validated.
7. **Allocation generalized from a single tier occupant to a (generator, verifier) pair** (§14). Cheap-generate/strong-verify becomes a first-class allocation pattern.
8. H1 decomposed into detection (H1a) and prediction (H1b); H5 control arms pinned to the three-arm handoff design; an attribution rule added for escalation recall (§32).
9. Handshake outcome states disambiguated (§8).
10. Ablation program partitioned into a required core and a deferred set; a minimal publishable unit is defined (§30); a hypothesis→condition→evidence map added (§37).
11. **Operational precedent section added** (§5), recording program-internal observational evidence for the two central mechanisms.
12. **Program alignment section added** (§44), mapping CRA vocabulary onto the existing TCAIN, Sovereign Orchestration Workspace, and ATG vocabulary. CRA is positioned as the program's orchestration-policy layer, not a sixth independent system.
13. The operating-system checkpoint metaphor is bounded (§46); the structured-handoff mechanism is instead grounded in the clinical shift-handoff literature (I-PASS).
14. Citations verified against primary sources; arXiv identifiers added; quantitative findings from The Replay Gap, RoadmapBench, and MetaCogAgent incorporated where they materially sharpen the argument.

---

## Abstract

Contemporary artificial intelligence systems increasingly combine multiple language models, tools, specialized agents, and execution environments. Yet most orchestration architectures treat model assignment as a static decision: a task is routed to a model, an agent retains that model throughout execution, or several models are invoked according to a fixed ensemble or debate structure. This creates two related inefficiencies. Expensive high-capability models remain assigned after a task has collapsed into deterministic or routine work; lower-capability models continue operating after unexpected complexity, ambiguity, or risk has emerged. A separate failure precedes execution entirely: an assigned worker may act on a materially incorrect interpretation of the conductor's objective while appearing to have accepted the assignment.

This thesis proposes **Cognitive Resource Allocation (CRA)**, a stateful orchestration architecture that treats machine cognitive capability as a dynamically allocatable computational resource. CRA combines two mechanisms. **Task-Comprehension Handshake (TCH)** is a bounded pre-execution protocol in which a conductor and candidate worker establish an explicit task contract containing objective, constraints, success conditions, scope, assumptions, authority, and intended method. **Adaptive Cognitive Tiering (ACT)** continuously estimates the cognitive demands of the evolving task and selects, escalates, or de-escalates the cognitive resources occupying a persistent worker role. An allocation is a *(generator, verifier)* pair rather than a single model, permitting patterns such as inexpensive generation under strong verification.

The architecture separates worker identity from model identity. A worker is defined by its task contract, state, permissions, history, artifacts, and unresolved issues; the models executing that role may change as cognitive demand changes. Movement is bidirectional across deterministic tools, lightweight local models, specialists, high-capability reasoners, and multi-model adversarial reasoning processes.

The central thesis is that multi-model systems can improve execution fidelity and cost-quality efficiency by allocating cognitive capability dynamically over task trajectories rather than statically per task or per query, provided that model transitions preserve structured state and consequential execution is preceded by explicit comprehension validation. Two hypotheses carry the load: that structured handoff preserves worker continuity across substitution (H8), and that comprehension telemetry supplies a *leading* indicator of task difficulty (H6). If both fail, CRA degenerates into known cascade routing with additional bookkeeping, and the program records that result.

This paper defines the architecture, formal model, hypotheses, experimental methodology, metrics, failure modes, and falsification criteria required to evaluate the claim. A deliberate property of the intended experimental environment — serial model hosting on a single consumer GPU — places the study in the high-switching-cost regime that well-resourced laboratories do not naturally inhabit and have little incentive to characterize.

**Keywords:** cognitive resource allocation, adaptive cognitive tiering, task comprehension, model routing, multi-model systems, agent orchestration, adaptive computation, LLM routing, persistent agent state, model switching, generator-verifier allocation

---

## 1. Introduction

Large language models differ substantially in capability, latency, cost, context capacity, modality support, tool-use reliability, structured-output behavior, and suitability for different classes of work. Modern AI systems therefore increasingly operate not around a single universal model but around heterogeneous collections of models and tools.

Existing research demonstrates several important forms of conditional computation. Adaptive Computation Time allows a neural system to allocate different amounts of internal computation to inputs of different difficulty (Graves, 2016). Sparsely gated mixture-of-experts architectures activate only selected experts for a given input (Shazeer et al., 2017). More recently, FrugalGPT, AutoMix, RouteLLM, and uncertainty-based routing methods have investigated selecting between models of differing capability and cost. These approaches establish an important principle:

> The optimal amount or source of machine computation need not be constant across inputs.

Long-running agentic work presents a harder problem than single-query routing, and the difficulty is now measured rather than merely suspected. RoadmapBench (Xu et al., 2026) grounds 115 long-horizon tasks in real open-source version upgrades — median oracle modification approximately 3,700 lines across 51 files — and finds that the strongest evaluated frontier model resolves only 39.1% of tasks. Realistic extended software development remains far from solved by any single static assignment.

A software-engineering task may begin with high ambiguity and architectural complexity, become routine after a design is selected, rise sharply in difficulty after an unexpected test failure, become mechanical again during repair, and require high-capability independent review before final acceptance. The relevant decision is therefore not merely *which model should answer this request*, but:

> What cognitive capability does the current state of this persistent task require now, and when should that capability change?

A second problem precedes model selection entirely. When an orchestrator assigns work to an AI worker, the worker may misunderstand the actual objective, required output, prohibited scope, relevant constraints, success criteria, authority boundary, architectural assumptions, or intended level of change. A conventional acknowledgement such as "understood" does not establish semantic alignment between task intent and worker interpretation.

This thesis treats these two problems as coupled. A comprehension protocol can expose ambiguity and task difficulty *before* execution; that information can then become routing telemetry. Conversely, model routing should remain dynamic because task complexity changes after execution begins. The result is the proposed architecture, Cognitive Resource Allocation.

## 2. Central Thesis

> A heterogeneous AI system can achieve higher execution fidelity and better cost-quality efficiency by treating cognitive capability as a state-dependent allocatable resource rather than a fixed property of an agent, while requiring explicit task comprehension before consequential execution and preserving worker state across model substitutions.

The thesis decomposes into four claims.

**Claim 1 — Task demand is non-stationary.** The cognitive requirements of a task change during execution. (Section 5 records program-internal observational support; controlled evidence remains outstanding.)

**Claim 2 — Agent identity and model identity should be separable.** A persistent worker role can survive substitution of the model executing it if state, objective, authority, and lineage are represented outside the model session.

**Claim 3 — Pre-execution comprehension can provide both safety and routing information.** A structured worker interpretation can reveal misunderstanding, ambiguity, unexpected complexity, and missing constraints before execution.

**Claim 4 — Cognitive allocation should be bidirectional.** A system should be capable of both increasing and decreasing cognitive capability as task state changes.

The thesis is falsifiable. It would be weakened or rejected if controlled experiments show that: the comprehension protocol adds overhead without reducing meaningful execution errors; adaptive routing fails to reduce cost at equivalent quality; model switching introduces more state loss than benefit; static model assignment performs as well as or better than adaptive assignment; routing signals do not predict actual task difficulty; or persistent worker identity across model transitions provides no measurable advantage. Section 48 enumerates the specific null results, including the keystone-failure case.

## 3. Scope and Non-Claims

This paper proposes an orchestration architecture. It does **not** claim:

1. that model routing is novel in itself;
2. that adaptive computation is novel;
3. that multi-agent negotiation is novel;
4. that multi-model debate is novel;
5. that the proposed architecture has already demonstrated superior performance;
6. that model self-reported uncertainty is intrinsically reliable;
7. that larger models always represent higher cognitive tiers;
8. that one universal scalar can meaningfully represent model intelligence;
9. that dynamic model substitution is always beneficial;
10. that the system constitutes artificial general intelligence;
11. that a passed comprehension handshake guarantees mid-execution compliance — TCH validates interpretation at assignment time, not adherence throughout execution (§7.5).

The research contribution under investigation is the *integration* of explicit task-comprehension validation, persistent role identity, structured state transfer, task-trajectory-aware bidirectional model substitution, generator-verifier allocation, capability-aware routing, and resource optimization into one observable execution architecture. An exhaustive novelty claim would require a dedicated systematic literature review beyond the survey performed for this prospectus.

## 4. Related Work

### 4.1 Adaptive computation

Graves (2016) demonstrated that a recurrent model can dynamically vary how much computation it performs according to input requirements. The conceptual precedent: computational depth need not be constant. CRA applies a related principle at a different abstraction level — ACT-the-mechanism adjusts internal computation within a model; CRA adjusts which external cognitive resource occupies a persistent task role across time.

### 4.2 Mixture-of-experts systems

Sparsely gated mixture-of-experts systems (Shazeer et al., 2017) use learned routing to activate subsets of a larger expert network. This establishes that specialized computational capability can be conditionally selected. An MoE expert is an internal neural component; CRA operates across heterogeneous external models, tools, modalities, providers, and multi-model reasoning protocols, with worker state and project history held outside the selected model.

### 4.3 LLM cascades and routing

FrugalGPT (Chen, Zaharia, and Zou, 2023) formalized selection among language models of different costs and demonstrated that cascades substantially alter the cost-performance tradeoff. AutoMix (Aggarwal et al., 2023) routes between models based partly on *self-verification by the smaller model* — a precedent worth emphasizing, because it locates value in cheap verification rather than only in cheap generation. RouteLLM (Ong et al., 2024) learns routers from preference data, reporting large cost reductions under some conditions without benchmark-quality loss. Ramírez, Birch, and Titov (2024) show that a smaller model's uncertainty can itself decide escalation.

These systems are close conceptual ancestors of Adaptive Cognitive Tiering. CRA differs primarily in the unit of routing. Conventional routing asks *which model should answer query q*. CRA asks:

> Which cognitive resources should occupy worker role `w` at task state `S_t`?

That distinction introduces persistent role identity, task history, execution state, changing uncertainty, model-transition costs, task contracts, mid-task escalation, mid-task de-escalation, structured state handoff, and post-switch trajectory effects.

### 4.4 Multi-agent reasoning and iterative refinement

Multi-agent debate can improve performance on some reasoning and factuality tasks (Du et al., 2023). Self-Refine (Madaan et al., 2023) iterates generate-critique-refine within one model. Reflexion (Shinn et al., 2023) introduces episodic linguistic feedback across attempts. Mixture-of-Agents (Wang et al., 2024) aggregates layered outputs from multiple models. CRA is complementary: those methods answer *how additional reasoning should be produced*; CRA asks *when additional reasoning is justified, what form it should take, and when the system should stop paying for it*. A debate, adversarial reasoning node, self-refinement loop, or multi-agent synthesis process is therefore represented as a higher cognitive tier rather than as the mandatory path for every task.

### 4.5 Distributed task negotiation

The Contract Net Protocol (Smith, 1980) introduced task distribution through negotiation between nodes possessing work and nodes capable of performing it. Task-Comprehension Handshake shares this distributed-problem-solving ancestry but addresses a different failure. The principal question in TCH is not *which worker should win the contract* but:

> Does the worker's semantic interpretation of the contract match the delegator's intended task closely enough to authorize execution?

### 4.6 Metacognitive and constraint-guided agents

Recent work has moved close to explicit task-capability alignment. MetaCogAgent (Wang and Shu, 2026) equips each agent with a self-assessment unit combining verbalized uncertainty with historical capability profiles, and adaptively delegates low-confidence tasks; on its purpose-built benchmark it reports 82.4% task accuracy, 8.7% above the best routing baseline, with fewer API calls than ensemble baselines. RunAgent (Srivastava et al., 2026) enforces stepwise natural-language plan execution through constraints and rubrics while dynamically selecting among reasoning, tool use, and code execution.

These systems significantly narrow any defensible novelty claim for CRA, and this thesis does not present CRA as the invention of adaptive delegation. MetaCogAgent's reported 8.7% routing gain additionally serves this program as an **effect-size prior for power analysis** (§30). CRA's candidate contribution is the specific combination of: bilateral task-comprehension contracting; persistent worker identity independent of model identity; bidirectional tier movement throughout a task trajectory; explicit switching costs and hysteresis; structured model-to-model role handoff; generator-verifier allocation pairs; multimodal capability vectors; deterministic, historical, model-generated, and operator-defined routing signals; and evaluation of total cost to accepted work rather than call-level inference cost.

### 4.7 The model-switching problem

Dynamic substitution introduces a serious methodological problem, now quantified. The Replay Gap (Gonuguntla, 2026) forks live SWE-bench agent trajectories at controlled points, continues each fork with a different model, and compares against same-model control forks. Across roughly 900 rollouts, swaps exceeded matched control floors by +0.25 to +0.66 normalized edit distance, **rewriting 61–94% of post-fork actions**; all five observed outcome flips occurred in swap arms and zero across 359 control forks; and a log-stitching replay evaluator **mispredicted every success-relevant outcome call**. A further finding matters directly to local deployments: temperature-0 "determinism" was configuration-dependent — FP8-served controls diverged on over 90% of forks while AWQ-served controls remained near-identical.

Three consequences bind this thesis. First, model substitution must be treated as a stateful control event, never a transparent implementation detail. Second, the null position is adversarial: **switching is expensive and disruptive by default**, and CRA's handoff mechanism must demonstrate that it tames divergence, not merely assume it. Third, switching behavior must be evaluated with **live branching** (§35), never static replay, and capability profiles must be versioned against exact serving configurations including quantization (§12).

### 4.8 Long-horizon motivation

RoadmapBench's results (§1) motivate the setting: real long-horizon work contains phases of very different cognitive character — objective interpretation, architecture discovery, dependency analysis, design choice, routine implementation, test execution, anomaly discovery, architectural reconsideration, corrective implementation, and final independent review. Using the strongest model for all ten phases is unnecessarily expensive; using a weak model for all ten is unreliable. Static assignment assumes a stationary task. CRA assumes the opposite.

## 5. Operational Precedent from a Working Program

This section records observational, single-environment evidence from the Sovereign Systems Research Program's own operating history. It is motivating precedent, not controlled evidence, and no hypothesis is considered supported by it.

**Manual tiered allocation already exists in practice.** The program's standing workflow allocates different engines to drafting, independent review, and machine execution, and escalates between them on failure — a hand-executed form of the architecture proposed here. One documented process discovery is directly a routing-policy result: inserting a *machine-state preflight before prose review* caught blockers that document-level review missed, inverting the previously recommended pipeline. In CRA vocabulary: a cheap deterministic verifier placed ahead of expensive cognition dominated the reverse ordering.

**Skipped comprehension validation is the dominant observed failure mode.** Across the program's governed execution chain, the majority of gate halts traced to a skipped confirmation-file step — an operational ancestor of the Task-Comprehension Handshake. The environment's own history indicates that omitting pre-execution confirmation is not a rare edge case but the modal failure.

**MANUAL-mode allocation is already implemented.** The Sovereign Orchestration Workspace's governed model-picker launch path — validated worker identity, workspace binding, permission envelope, lease accounting, supervised process lifecycle — is an operating implementation of §23's MANUAL mode. Phase 1 of the implementation strategy (§41) therefore builds on an existing substrate rather than a green field.

These observations shaped the architecture and justify testing it. They do not substitute for the controlled program in §§28–37.

## 6. Proposed Architecture

Seven principal components:

1. Task Formation
2. Task-Comprehension Handshake
3. Task Contract
4. Cognitive Demand Estimator
5. Capability Registry
6. Adaptive Cognitive Router
7. Persistent Worker State

The complete control path:

```text
Operator Objective
        ↓
Task Formation
        ↓
Task-Comprehension Handshake
        ↓
Accepted Task Contract
        ↓
Cognitive Demand Estimation
        ↓
Tier + (Generator, Verifier) Selection
        ↓
Worker Execution
        ↓
State Checkpoint
        ↓
Demand Reassessment
        ↓
Continue / Escalate / De-escalate / Block
        ↓
Execution
        ↓
Independent Validation
        ↓
Accept / Revise / Reject
```

## 7. Task-Comprehension Handshake

### 7.1 Purpose

TCH is a bounded pre-execution protocol intended to expose semantic disagreement before consequential work begins. The conductor issues a structured task packet. The candidate worker must not merely acknowledge it; it must produce an interpretation containing: understood objective; expected output; intended approach; relevant artifacts; assumptions; unresolved ambiguities; risks; scope boundaries; actions explicitly not required; and expected completion state. The conductor then compares worker interpretation against intended task state.

### 7.2 Task packet

```text
T = (O, R, C, S, F, A, P, B)
```

where `O` = objective; `R` = required output; `C` = constraints; `S` = success conditions; `F` = forbidden scope; `A` = relevant artifacts; `P` = permissions and authority; `B` = resource budget.

### 7.3 Worker interpretation

```text
I = (O', R', C', S', F', M, U, K)
```

where primed elements are the worker's interpretations of the corresponding packet elements; `M` = intended method; `U` = uncertainty and ambiguity report; `K` = assumptions and known risks.

### 7.4 Comprehension vector — mechanical and judged components

The system evaluates a comprehension vector:

```text
H = (h_o, h_r, h_c, h_s, h_f, h_a)
```

representing objective fidelity, output fidelity, constraint coverage, success-condition fidelity, scope fidelity, and assumption disclosure.

v0.2 partitions these dimensions by how they can be checked:

- **Mechanically checkable:** constraint coverage (`h_c`) — did the interpretation enumerate every constraint identifier in `C`; scope fidelity (`h_f`) — did it echo the complete forbidden list and add nothing to authorized scope; artifact reference resolution — do all referenced artifacts in the plan exist in `A`. These checks are deterministic and require no model judgment.
- **Judgment-requiring:** objective fidelity (`h_o`), output fidelity (`h_r`), success-condition fidelity (`h_s`), and assumption adequacy (`h_a`) require semantic comparison, performed by the conductor.

CRA must not collapse `H` into one scalar. A worker that correctly understands five dimensions but misses one critical prohibition should not receive a passing average.

### 7.5 Known limitations of the handshake

Two limitations are inherent and are named here rather than discovered later.

**Restatement is not compliance.** TCH validates interpretation at assignment time. It does not guarantee adherence during execution; instruction drift can occur after a perfect restatement. H1 is therefore decomposed (§26): H1a tests whether TCH *detects* pre-execution misinterpretation; H1b tests whether restatement quality *predicts* execution compliance at all.

**The judge is partly an LLM.** The judgment-requiring dimensions of `H` are evaluated by the conductor, importing the evaluator-reliability limits of §33 into the gate itself. Mitigations: maximize the mechanically checkable share of `H`; log conductor comprehension judgments for audit against outcomes; and treat the handshake as one control among several rather than a sufficient guarantee. A capable model can also produce plausible-sounding assumptions without genuine understanding (parroting, §38.2); requiring method, artifacts, prohibited-scope echo, and expected completion state raises the bar without eliminating the risk.

## 8. Handshake Outcomes

The protocol returns one of four states, disambiguated by *where the defect lies*:

```text
TASK_CONTRACT_ACCEPTED
    Interpretation matches intent within tolerance. Execution authorized.

TASK_CONTRACT_REVISION_REQUIRED
    Defect lies in the worker's interpretation. Conductor corrects and reissues.

TASK_PACKET_DEFECTIVE
    Defect lies in the packet itself (internal ambiguity or contradiction).
    Conductor must repair the packet; the worker is not at fault.
    (v0.1 name: TASK_BLOCKED_AMBIGUOUS.)

TASK_REQUIRES_OPERATOR_CLARIFICATION
    Defect lies in intent or authority — a question only the operator can
    answer. Escalates outside the conductor's authority.
```

The handshake is intentionally bounded. Routine work should ordinarily require one exchange; a maximum iteration count prevents comprehension validation from becoming an infinite negotiation loop.

## 9. Task Contract

After successful comprehension validation, the system freezes an explicit task contract — the authoritative execution reference for the worker. Representative schema:

```yaml
task_id: CRA-00184

objective:
  Repair worker-session reconnection.

success_conditions:
  - reconnect preserves existing worker identity
  - no duplicate process is created
  - regression test passes

constraints:
  - preserve current session protocol
  - no dependency changes
  - no interface redesign

forbidden_scope:
  - terminal architecture replacement
  - unrelated persistence migration

worker_plan:
  - reproduce failure
  - isolate defect
  - patch minimum affected surface
  - add regression test
  - run targeted suite

assumptions:
  - current session schema remains authoritative

authority:
  filesystem_write: bounded
  dependency_change: false
  release_promotion: false

status:
  TASK_CONTRACT_ACCEPTED
```

The contract belongs to the task, not to the model.

## 10. Persistent Worker Identity

CRA distinguishes three entities that conventional agent systems merge:

```text
Role  ≠  Worker  ≠  Model
```

- **Role** — the functional responsibility (e.g., `Backend Implementation Engineer`).
- **Worker** — the persistent task-bearing execution identity (e.g., `WORKER-07`).
- **Model** — the cognitive engine currently occupying that worker (e.g., `MODEL-A`).

At time `t`, worker `W_i` is occupied by model `M_a`; at a later time, by `M_b`. The worker remains `W_i`. Its continuity comes from the task contract, permissions, artifact state, verified facts, decisions, failed attempts, unresolved issues, checkpoints, and provenance. The model is replaceable.

## 11. Cognitive Demand Representation

A task is not assigned a universal difficulty score. Demand is a vector:

```text
D_t = (d_reason, d_code, d_vision, d_context, d_tools, d_uncertainty, d_criticality)
```

Dimensions vary by domain. A software-engineering deployment might add architecture, debugging, deterministic transformation, security reasoning, and schema reliability. A multimodal deployment adds vision, audio, document understanding, spatial reasoning, and temporal media reasoning.

**Who computes `D_t` — specified.** In Phases 1–2 the estimator draws only on:

1. **deterministic runtime signals** — test failures, retry counts, validator rejections, diff size, budget consumption, checkpoint latency;
2. **handshake telemetry** — ambiguity count, assumption count, constraint disagreements, disclosed risks from the TCH interpretation (§17–18);
3. **historical task-family profiles** — recorded outcomes for comparable contracts;
4. **operator annotations** — explicit criticality or difficulty declarations.

Model self-reported difficulty is admissible only as one weighted input among these and never as the sole source (CRA-I5). No learned demand estimator or learned router exists before Phase 3; Phase 1–2 routing is hand-tuned rules over these signals. The hypotheses in §26 are accordingly framed against a *reasonable heuristic router*, a claim that can actually be tested, rather than an optimal one.

## 12. Model Capability Representation

Each candidate model `m` has a capability profile:

```text
Q_m = (q_m1, q_m2, ..., q_mn)
```

and a resource profile:

```text
R_m = (c_m, l_m, v_m, k_m)
```

where `c_m` = monetary or compute cost; `l_m` = expected latency; `v_m` = memory or hardware requirement; `k_m` = context capacity or related operational limit.

Capability profiles come from controlled qualification and historical performance, not marketing claims — and are **versioned against exact deployment configurations**, including quantization and serving stack. The Replay Gap's finding that FP8-served runs diverged where AWQ-served runs did not (§4.7) demonstrates that a model name does not identify a behavioral object; the (weights, quantization, serving configuration) triple does.

## 13. Cognitive Tiers

Tiers are routing abstractions, not hard-coded model rankings.

- **Tier 0 — Deterministic execution.** No generative model. Hash computation, file copy, build commands, deterministic formatting, test execution, schema validation.
- **Tier 1 — Lightweight cognition.** Bounded classification, simple transformations, narrow summarization, routine edits.
- **Tier 2 — Standard specialist cognition.** Ordinary coding, conventional debugging, structured technical analysis, standard research synthesis.
- **Tier 3 — Advanced cognition.** Architecture, ambiguous debugging, multi-constraint design, difficult synthesis, consequential planning.
- **Tier 4 — Deep or adversarial cognition.** Not necessarily a single model: multi-model debate, adversarial reasoning, independent verification, structured multi-agent synthesis. Within this research program, the reference Tier-4 implementation is a **TCAIN node** (§44); CRA is, among other things, TCAIN's invocation policy — the formal answer to *when* an adversarial reasoning node is justified.

Thus `Tier ≠ Model`. The tier describes required capability; the router selects the most suitable available implementation.

## 14. Allocation as Generator–Verifier Pairs

v0.1 implicitly assumed that changing an allocation means changing the *generator*. Frequently the correct move is to change the *verifier*. Verification of a candidate output is often cheaper than generation, so the cost-optimal use of a strong model is frequently to review a weak model's work rather than to produce the work itself. AutoMix's small-model self-verification (§4.3) is the single-model ancestor of this pattern.

v0.2 therefore defines an allocation at each checkpoint as a pair:

```text
allocation_t = (g_t, v_t)
```

where `g_t` is the generation resource and `v_t` the verification resource. Canonical patterns:

| Pattern | Generator | Verifier | Typical use |
|---|---|---|---|
| Bulk implementation | Tier 1–2 | Tier 3 review or Tier 0 tests | Routine edits under supervision |
| Hard synthesis, checkable | Tier 3 | Tier 0 deterministic tests | Design work with executable acceptance |
| Consequential judgment | Tier 3 | Tier 3, lineage-disjoint | High-impact decisions without deterministic checks |
| Deep reasoning | Tier 4 (TCAIN node) | External validator | Adversarial multi-model work |

The de-escalation rule of §19 is naturally expressed in this vocabulary: lowering `g` is safe precisely when `v` is deterministic or independent.

## 15. Adaptive Cognitive Routing

At checkpoint `t`, the router observes:

```text
S_t = (T, X_t, U_t, F_t, P_t, R_t)
```

where `T` = task contract; `X_t` = current artifact and execution state; `U_t` = uncertainty; `F_t` = failures and anomalies; `P_t` = progress; `R_t` = resource consumption.

A routing policy:

```text
pi(S_t, H, Q, Omega)  →  (tier_t, g_t, v_t)
```

where `H` = comprehension telemetry; `Q` = capability registry; `Omega` = operator policy and resource limits.

## 16. Routing Objective

The naive objective — minimize model-call cost — is insufficient: a cheap model that repeatedly fails may cost more overall than one expensive successful call. CRA defines the relevant economic quantity as `C_accepted`: the total resource cost required to reach *accepted* work, including inference cost, local compute, wall-clock time, retries, rework, model switches, verifier calls, failed artifacts, and operator intervention.

The v0.2 objective (correcting the v0.1 double-count of quality in both a penalty term and a constraint):

```text
minimize over (g, v) in F_t:   E[ C_accepted(g, v, S_t) ]

subject to:                    P( Quality >= Q_min ) >= alpha
                               E[ Latency ] <= L_max        (where a latency bound applies)
```

Quality binds **only** as a constraint; it does not also appear in the objective. Latency is either priced into `C_accepted` via a declared wall-clock cost rate or bounded separately — one mechanism per deployment, declared in advance. `F_t` is the set of policy-permitted allocations. This remains a conceptual objective: its quantities are estimated, not known, and Phase 1–2 approximates it with rules (§20), not optimization.

## 17. Bidirectional Tiering

A typical task trajectory:

```text
HIGH     architecture discovery
 ↓
MEDIUM   implementation planning
 ↓
LOW      mechanical implementation
 ↑
HIGH     unexpected contradiction
 ↓
MEDIUM   repair
 ↓
LOW      cleanup
 ↑
HIGH     independent final review
```

De-escalation is an optimization mechanism; escalation is a recovery mechanism. Both are essential.

## 18. Escalation Signals

Upward-routing signals include: repeated failure; newly discovered architectural conflict; increased uncertainty; conflicting evidence; unexpected dependency; validator rejection; worker-reported capability insufficiency; high-impact decision; rapidly expanding scope; repeated rework; disagreement with conductor interpretation.

A worker may emit, without being classified as failed:

```text
CAPABILITY_INSUFFICIENT
CONTEXT_INSUFFICIENT
SPECIALIST_REQUIRED
AMBIGUITY_TOO_HIGH
```

**A structural observation that motivates the keystone analysis (§27):** nearly every signal above is a *lagging* indicator — the system learns the task is hard by paying for failure first. The only *leading* indicator in the architecture is comprehension telemetry from the handshake: ambiguity count, assumption count, constraint disagreement, disclosed risk. Whether that telemetry actually predicts downstream difficulty is hypothesis H6, and much of the architecture's distinctiveness rides on it.

## 19. De-Escalation Signals and the Deterministic-Validation Rule

Downward-routing signals include: architecture frozen; ambiguity resolved; remaining work bounded; correctness defined by deterministic tests; low novelty; high reversibility; low recent failure rate; stable constraints; successful decomposition into routine subtasks.

De-escalation carries an asymmetric verification problem: the sufficiency of a *cheaper* model for the *remaining* work cannot be cheaply tested in advance — it is a counterfactual. v0.2 therefore replaces the v0.1 direction ("stronger evidence for downward movement") with an operational rule:

> **De-escalate only into task regions whose acceptance is deterministically checkable or independently validated.** Absent such a check, retain the current tier regardless of estimated sufficiency.

Where the validator is deterministic, an under-capable generator's failure is caught, not shipped; the cost of a wrong de-escalation collapses from task damage to bounded retry cost. In generator-verifier vocabulary (§14): lower `g` only where `v` is Tier 0 or independent. This rule is codified as revised invariant CRA-I9 (§43).

## 20. Hysteresis and Tier Stability

Uncontrolled adaptive routing oscillates (`Tier 2 → 3 → 2 → 3 ...`), wasting resources and destroying continuity. A transition requires:

```text
B_switch > C_switch + delta
```

where `B_switch` is estimated benefit of changing allocation, `C_switch` the switching cost, and `delta` a stability margin. (v0.1 omitted the inequality operator; corrected here.)

**Composition of `C_switch`.** Switching cost is not merely handoff tokens. It comprises: handoff-packet construction; successor ingestion of the packet; **model load/unload wall-clock time** — dominant on single-GPU serial hosting, where a tier change is a full unload/load cycle measured in tens of seconds to minutes; divergence risk, with the Replay Gap's 61–94% post-fork action rewrites as the adversarial prior; and post-switch re-verification. Hysteresis parameters are therefore **hardware-dependent and must be declared per deployment**. A consequence worth stating: the scientifically interesting hysteresis regime is precisely high-`C_switch`, serially hosted execution — a regime that cluster-equipped laboratories do not experience and have little incentive to characterize, and which the intended experimental environment inhabits natively.

**Estimating `B_switch` is a counterfactual problem**, so Phases 1–2 do not attempt it directly. They use proxy triggers:

- **Escalate** when: `k` consecutive failed checkpoints, or a validator rejection, or an explicit worker insufficiency signal (`k` small, e.g., 2).
- **De-escalate** when: `m` consecutive clean checkpoints **and** the deterministic-validation rule of §19 is satisfied **and** a minimum residency period has elapsed (`m` larger than `k`, e.g., 3+).

The asymmetry implements CRA-I9: a mistaken escalation mainly costs resources; a mistaken de-escalation can damage the task.

## 21. Structured Model Handoff

A model transition must not rely on dumping the previous transcript into the successor. The canonical handoff packet:

```yaml
worker_id:
task_contract:
current_state:
completed_actions:
verified_facts:
current_artifacts:
decisions:            # frozen; successor may not reopen without new evidence
assumptions:
unresolved_issues:    # open; successor may engage
failed_attempts:
relevant_evidence:
next_expected_action:
authority_limits:
resource_state:
```

The distinction between `decisions` (frozen) and `unresolved_issues` (open) is load-bearing: it is the packet's defense against successor reinterpretation (§38.10), in which a new model relitigates settled questions without new evidence.

Transition sequence:

```text
Model A → structured checkpoint → checkpoint validation → Model A released
        → Model B assigned → state acknowledgement → execution continues
```

This creates a testable distinction between **session continuity** (keeping the same model conversation alive) and **worker continuity** (preserving task identity despite replacing the model). CRA is principally concerned with the latter.

**The correct analogy is a shift handoff, not a process checkpoint.** An operating-system checkpoint is a lossless byte copy; a CRA handoff is semantic compression — lossy by construction. The closer analog is the clinical or aviation shift handoff, and that literature is encouraging: the I-PASS program (Starmer et al., 2014) found that a structured handoff bundle materially reduced medical errors and preventable adverse events across nine hospitals relative to unstructured signout. Structured state transfer between agents of comparable capability is an empirically supported intervention in human systems; H8 tests whether the result transfers to model workers.

## 22. Multimodal Cognitive Resource Allocation

CRA generalizes beyond text. A task may involve natural language, source code, images, audio, video, diagrams, PDFs, spreadsheets, logs, and structured data; a single model may not be optimal across all required capabilities. A capability-aware decomposition might route image inspection to a vision specialist, repository reasoning to a coding specialist, log analysis to a diagnostic specialist, and architectural synthesis to an advanced reasoner. The system does not merely choose which model answers; it allocates cognitive modalities and specializations to components of the work.

## 23. Operator Policy

Automatic routing remains subordinate to explicit operator constraints. CRA supports at least:

- **MANUAL** — the operator fixes the allocation. Useful for benchmarking, reproducibility, testing, and preference. *(An operating implementation of this mode already exists in the program's Workspace substrate; see §5 and §41.)*
- **ASSISTED** — the router recommends; the operator confirms.
- **ADAPTIVE** — the router changes allocations automatically within a predefined policy envelope.

Example policy envelope:

```yaml
providers:
  local: allowed
  frontier: allowed

preference:
  local_first: true

budget:
  max_frontier_calls: 8
  max_monetary_cost: 5.00

tiers:
  minimum: 0
  maximum: 4

automatic_deescalation: true
automatic_escalation: true
```

## 24. Authority Separation

One component must not simultaneously define the task, judge comprehension, choose the executing model, execute the work, judge the output, and approve the result. CRA separates:

```text
CONDUCTOR   Task interpretation and decomposition
WORKER      Task execution
ROUTER      Cognitive resource recommendation
VALIDATOR   Result evaluation
OPERATOR    Reserved acceptance authority
```

Implementations may combine components for efficiency, but the logical responsibilities remain distinguishable and auditable.

## 25. Research Questions

- **RQ1** — Does TCH reduce execution errors caused by misunderstood objectives, constraints, or scope?
- **RQ2** — Can ACT reduce total resource cost while preserving accepted-task quality relative to fixed strongest-model execution?
- **RQ3** — Does bidirectional re-tiering outperform one-way escalation or static routing on tasks whose complexity changes during execution?
- **RQ4** — Do signals collected during the comprehension handshake predict eventual task difficulty, rework, or escalation?
- **RQ5** — Does persistent worker identity preserve task continuity across model substitutions better than restarting the worker after each model change?
- **RQ6** — Does structured state handoff outperform raw transcript transfer during model switching?
- **RQ7** — Does capability-aware specialist routing outperform model-size-based routing?
- **RQ8** — For multimodal tasks, does modality-specific routing improve cost-adjusted performance over one general multimodal model throughout?

## 26. Hypotheses

- **H1a — Comprehension detection.** TCH will detect materially incorrect pre-execution interpretations (seeded and naturally occurring) at a rate exceeding its false-positive burden, relative to direct assignment.
- **H1b — Comprehension-compliance prediction.** Restatement quality at handshake time will predict execution-time compliance (scope violations, constraint breaches) — a distinct and weaker claim than H1a, stated separately because restatement is not compliance (§7.5).
- **H2 — Adaptive efficiency.** Full CRA will reduce total cost per accepted task relative to always using the strongest available model, without materially reducing success rate.
- **H3 — Escalation recovery.** Dynamic upward escalation will reduce repeated failure and rework relative to fixed low-cost execution.
- **H4 — De-escalation efficiency.** Dynamic downward tiering after complexity collapses will reduce cost and latency relative to retaining the strongest model throughout.
- **H5 — Persistent role continuity.** A worker retaining structured task state across substitution will outperform a worker reset on model change. Control arms pinned to the three-arm design: structured packet (C5) vs. raw transcript (A9) vs. reset (A10).
- **H6 — Handshake predictive power.** Comprehension-stage ambiguity count, assumption count, constraint disagreement, and disclosed risk will predict downstream escalation and rework better than initial task labels alone.
- **H7 — Specialist routing advantage.** Routing on multidimensional capability profiles will outperform routing on model size or aggregate benchmark rank.
- **H8 — Structured handoff advantage.** Structured state packets will produce lower post-switch divergence attributable to lost constraints or repeated work than raw transcript handoff.

## 27. Keystone Hypothesis Structure

The hypotheses above are not peers; they form a dependency tree, and the architecture's viability hangs on two of them.

**H8 and H5 are preconditions, not results.** If structured handoff does not preserve worker state across substitution, H2, H3, and H4 are untestable — every switch destroys the trajectory being optimized. The Replay Gap sets the adversarial prior: swaps rewrote 61–94% of post-fork actions in live branching. The null position is that switching is disruptive by default; the handoff mechanism must demonstrably tame it. H8 is accordingly the **first experiment** — it is also the cheapest, requiring two local models and no router.

**H6 is the keystone.** Section 18 observes that every escalation signal except handshake telemetry is a lagging indicator. If H6 fails — if comprehension telemetry does not predict difficulty — then ACT possesses no leading signal, escalation reduces to escalation-on-failure, and the architecture degenerates into a cascade with checkpoints: territory already occupied by FrugalGPT and AutoMix. CRA's residual novelty would shrink to bidirectionality plus persistence bookkeeping. This is stated plainly here, and recorded as Null H in §48, because a research program should know in advance which single result would hollow it out.

H6 is also **observational and nearly free**: collect the interpretation on every task *without gating on it*, then correlate handshake telemetry with downstream escalation, rework, and outcome. No router is required. It is therefore the first CRA result obtainable, concurrent with H8.

**H1–H4 and H7 are payoff hypotheses**, testable only after the preconditions hold. The resulting experiment order:

```text
H8 (handoff)  →  H6 (observational telemetry)  →  H1a (TCH ablation)  →  H2/H3/H4 (routing)
```

## 28. Experimental Conditions

- **C0** — Strongest fixed model performs the entire task.
- **C1** — Low-cost fixed model performs the entire task.
- **C2** — Static specialist, manually chosen per task family, fixed.
- **C3** — Adaptive tiering only (no TCH).
- **C4** — Handshake only (TCH; fixed model).
- **C5** — Full CRA: TCH + ACT + persistent worker identity + structured handoff.
- **C6** *(optional, later)* — Deep multi-model tier: CRA may escalate selected states into multi-model adversarial reasoning (a TCAIN node).

## 29. Experimental Domains

- **Domain A — Software repair.** Bounded bugs, regression repair, configuration correction, API compatibility defects. Scored by tests, artifact integrity, unauthorized changes. **Domain A is the minimal-publishable-unit domain** (§30).
- **Domain B — Multi-constraint engineering changes.** Multi-component modifications, architecture-preserving refactors, dependency migrations. Scored by tests, change-scope compliance, requirements traceability, blinded human review where necessary.
- **Domain C — Multimodal engineering.** Screenshot + code defect; diagram + specification review; log output + repository; visual UI defect + source.
- **Domain D — Long-horizon tasks with engineered non-stationarity.** High ambiguity → routine work → injected anomaly → recovery → final validation. These specifically test whether bidirectional routing matters.

## 30. Experimental Design

The **task**, not the model call, is the primary experimental unit. Where feasible, paired comparisons run the same task under multiple conditions.

Preregistration covers: task corpus; model versions and serving configurations (including quantization, per §12); provider configuration; tool access; initial state; budgets; routing policy; stopping policy; primary outcomes; exclusion rules; and statistical analysis. A pilot first estimates outcome variance; the definitive sample size follows power analysis rather than an attractive round number. **Effect-size priors for the power analysis:** MetaCogAgent's 8.7% routing gain over its best baseline for cost/accuracy effects; the Replay Gap's divergence magnitudes for switch-disruption effects. Non-inferiority testing on quality requires more power than superiority testing on cost; the pilot must size for the former.

**Minimal publishable unit.** Because the full program (seven conditions, four domains, twelve ablations, live branching) exceeds any single-operator resource envelope, the preregistered minimum is:

- Domain A only;
- conditions C0, C1, C5;
- core ablations A1, A9, A10 (§36);
- H8 and H6 first, per §27;
- pilot of 10–15 tasks for variance estimation, then powered main run;
- live branching at 2–3 checkpoints on a preregistered task subset;
- primary comparisons: C5 vs. C0 (cost, with quality non-inferiority) and A9 vs. C5 (handoff).

Everything beyond this is expansion, contingent on the minimal unit's results.

## 31. Primary Outcome Measures

**Accepted task success rate** — the proportion of tasks producing an artifact that passes required acceptance conditions.

**Total cost per accepted task:**

```text
CAE = ( sum of C_total ) / N_accepted
```

including rework, switching, and validation — not merely inference.

## 32. Secondary Metrics

- **Comprehension accuracy** — initial interpretations passing without correction.
- **Contract revision rate** — interpretations requiring revision.
- **Scope-violation rate** — executions modifying unauthorized artifacts or objectives.
- **Escalation precision** — escalations in which the higher tier materially improved the trajectory.
- **Escalation recall** — capability-attributable failures preceded by escalation. **Attribution rule:** a failure is capability-attributable when a subsequent escalation *with no other intervention* — same contract, same state, same tools — resolves it.
- **De-escalation precision** — lower tiers completing remaining work without re-escalation.
- **Re-tier frequency**; **tier thrashing** (oscillating transitions); **cognitive waste** (resources spent at a higher tier where a validated lower tier would have succeeded); **under-tier failure** (rework or failure from insufficient capability).
- **State-loss error** — post-switch errors caused by lost constraints, repeated work, or forgotten decisions.
- **Operator intervention rate.**

## 33. Evaluator Independence

Subjective evaluation is a major validity risk. Evaluation priority order:

1. deterministic tests;
2. executable invariants;
3. artifact comparison;
4. blinded human evaluation;
5. model-based semantic evaluation.

Where model judges are used: contestant identities hidden; answer ordering randomized; judges lineage-disjoint from contestants where feasible; multiple judges for consequential subjective metrics; disagreement retained; and a frozen human-reviewed subset calibrating judge reliability. A model judge must not silently become the scientific authority for whether another model is "better." These requirements apply equally to the conductor's comprehension judgments (§7.5), which are logged and audited against outcomes.

## 34. Statistical Analysis

Primary preregistered comparisons: C5 vs. C0 for efficiency at non-inferior quality; C5 vs. C2 for benefit over competent static specialist assignment. Appropriate methods include paired bootstrap confidence intervals, permutation tests, mixed-effects models treating task family and model combination as variance sources, non-inferiority testing for quality, effect-size reporting, and survival or time-to-completion analysis where useful. Secondary hypothesis testing uses multiplicity controls rather than presenting every favorable metric independently. Raw results are preserved regardless of whether the primary hypothesis succeeds.

## 35. Live Branching for Model-Switch Evaluation

Because substitution alters the subsequent trajectory (§4.7), switching is never evaluated primarily through static replay. For selected checkpoints:

```text
                 State S_t
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
      Continue M_A        Switch to M_B
          │                   │
          ▼                   ▼
       live run            live run
```

The environment is reconstructed from the same checkpoint; both branches proceed independently; same-model control forks isolate sampling noise, following the Replay Gap protocol. Measured: subsequent action divergence, artifact divergence, outcome difference, cost difference, constraint preservation.

## 36. Ablation Program

Aggregate success would not reveal causality. v0.2 partitions the ablations.

**Core (required for the minimal publishable unit):**

- **A1 — No task handshake.** Direct assignment. (Tests TCH; maps to H1a.)
- **A9 — Raw transcript handoff.** (Tests structured packets; maps to H8.)
- **A10 — Reset worker on model change.** (Tests persistent identity; maps to H5.)

**Deferred (contingent on minimal-unit results):**

- A2 — Restatement only (no assumptions/scope exposure); A3 — no assumption disclosure; A4 — no historical capability profile; A5 — self-assessment-only router; A6 — no hysteresis (measures thrashing); A7 — escalation only; A8 — de-escalation only; A11 — model-size routing vs. capability vectors (maps to H7); A12 — no resource accounting.

Each deferred ablation retains its rationale here so the deferral is a resourcing decision, not a deletion.

## 37. Hypothesis–Condition–Evidence Map

| Hypothesis | Tested by | Evidence form | Priority |
|---|---|---|---|
| H8 handoff | A9 vs. C5; live branching | Post-switch divergence, state-loss errors | **First** (precondition) |
| H6 telemetry | Observational, all runs | Correlation of TCH telemetry with escalation/rework | **First** (keystone; no dedicated condition) |
| H5 continuity | A10 vs. C5 | Outcome + state-loss comparison, three-arm | Second (precondition) |
| H1a detection | A1 vs. C4; seeded misinterpretations | Detection rate vs. false-positive burden | Second |
| H1b prediction | Observational | Restatement quality → compliance correlation | Second |
| H2 efficiency | C5 vs. C0 | CAE at quality non-inferiority | Third (payoff) |
| H3 recovery | C5 vs. C1 | Rework, under-tier failure | Third |
| H4 de-escalation | C5 vs. C0, tier-residency analysis | Cost, cognitive waste | Third |
| H7 specialist routing | A11 | Deferred | Deferred |

## 38. Failure Modes

- **38.1 Handshake bureaucracy.** The protocol costs more than the task. *Mitigation:* task classes permit abbreviated or bypassed handshakes for reversible low-impact work.
- **38.2 Parroted comprehension.** The worker repeats the packet without understanding. *Mitigation:* require method, assumptions, artifacts, prohibited-scope echo, and expected completion state; mechanical checks per §7.4; residual risk acknowledged in §7.5.
- **38.3 Conductor misinterpretation.** A perfectly aligned worker faithfully executes the conductor's wrong interpretation. *Mitigation:* the operator objective remains superior to the conductor-derived contract.
- **38.4 Premature de-escalation.** *Mitigation:* the deterministic-validation rule (§19) and minimum residency.
- **38.5 Strong-model addiction.** The router selects the highest tier "for safety." *Mitigation:* measure marginal value and cognitive waste.
- **38.6 Cost addiction.** Over-optimizing for cheap models creates rework. *Mitigation:* optimize `C_accepted` under a quality floor.
- **38.7 Tier thrashing.** *Mitigation:* hysteresis, minimum residency, switch penalties (§20).
- **38.8 Self-assessment manipulation.** A model claims uncertainty to obtain escalation, or confidence beyond capability. Note the incentive structure cuts both ways: if disclosed uncertainty triggers reassignment, honest disclosure is punished; if it attracts budget, it is rewarded. *Mitigation:* self-assessment is one signal among deterministic, historical, and external indicators (CRA-I5), and escalation precision is audited per worker.
- **38.9 Handoff loss.** *Mitigation:* structured checkpoint, validation, successor acknowledgement, rollback capability.
- **38.10 Successor reinterpretation.** A new model relitigates accepted decisions without new evidence. *Mitigation:* frozen `decisions` vs. open `unresolved_issues` in the handoff packet (§21).
- **38.11 Capability-profile staleness.** Behavior changes across versions, quantizations, prompts, hardware, and serving stacks. *Mitigation:* profiles versioned against exact deployment configurations (§12).
- **38.12 Router Goodharting.** A learned router optimizes measured metrics rather than useful work. *Mitigation:* hidden evaluation sets, multiple metrics, deterministic acceptance conditions, periodic routing ablations — and no learned router before Phase 3 at all.

## 39. Security and Integrity Considerations

CRA expands the attack surface because models may be granted different tools and authority levels. Routing must consider permissions, not only competence. The capability and authority systems remain separate:

```text
Capability(Model)  ≠  Authority(Worker)
```

A model may be capable of modifying a deployment environment while the worker role remains prohibited from doing so. **Model substitution must not silently increase authority:** the successor inherits the worker's authority envelope, not its own default capabilities (CRA-I8).

## 40. Multimodal Security Implications

External images, documents, webpages, logs, and retrieved text can contain adversarial instructions or misleading evidence. A multimodal router distinguishes task content, instructions, retrieved evidence, untrusted embedded text, and executable authority. No model converts an instruction discovered inside an artifact into system authority merely because it can understand the modality.

## 41. Implementation Strategy

**Phase 1 — Deterministic prototype.** Build: task contract schema; worker comprehension report; conductor validation with mechanical `H` components; three cognitive tiers; manual tier-model mappings; upward escalation on proxy triggers; routing event log; structured handoff packet. **No learned router.** *Substrate note:* the program's Workspace already provides governed worker launch, identity, authority envelopes, lease accounting, and supervised lifecycle (§5) — an operating MANUAL mode. Phase 1 deltas against that substrate are the contract schema, the comprehension report, the handoff packet, and the routing event log, not a green-field runtime.

**Phase 2 — Instrumented adaptive routing.** Add: capability registry; resource ledger; automatic tier recommendations; downward tiering under the §19 rule; hysteresis with declared hardware-dependent parameters; historical model performance; structured successor acknowledgement.

**Phase 3 — Experimental validation.** Implement C0–C5. Run fixed baselines, the core ablations, full CRA, and model-switch branch experiments. Freeze the evaluation corpus before analyzing results. Execute the minimal publishable unit (§30) before any expansion.

**Phase 4 — Multimodal extension.** Add routing dimensions for vision, audio, video, code, long-context documents, structured data; test specialist decomposition against a general multimodal baseline.

**Phase 5 — Deep-tier integration.** Allow Tier 4 to invoke a multi-model reasoning architecture (a TCAIN node) when single-model cognition is insufficient — only after lower tiers and switching behavior are empirically understood.

## 42. Runtime State Machine

```text
TASK_CREATED
      ↓
TASK_INTERPRETATION
      ↓
CONTRACT_PENDING
      ↓
 ┌───────────────┐
 │ accepted?     │
 └───────┬───────┘
         │
     YES │ NO
         │  └→ REVISION / PACKET_REPAIR / OPERATOR_CLARIFICATION
         ▼
CONTRACT_ACCEPTED
         ↓
DEMAND_ASSESSMENT
         ↓
ROUTING_PENDING
         ↓
ALLOCATION_ASSIGNED          # (generator, verifier) pair
         ↓
EXECUTING
         ↓
CHECKPOINT
         ↓
 ┌──────────────────────────────┐
 │ Continue / Escalate /        │
 │ De-escalate / Block          │
 └──────────────┬───────────────┘
                ↓
             EXECUTING
                ↓
             VALIDATION
                ↓
      ACCEPT / REVISE / REJECT
```

## 43. Core Invariants

- **CRA-I1** — No consequential worker begins execution without an accepted task contract.
- **CRA-I2** — Worker identity is independent of model identity.
- **CRA-I3** — Model substitution must not erase accepted task state.
- **CRA-I4** — Every routing decision is recorded with its evidence.
- **CRA-I5** — Model self-assessment alone cannot determine cognitive tier.
- **CRA-I6** — Operator provider, authority, and resource limits dominate automatic routing.
- **CRA-I7** — A worker may request escalation without being classified as failed.
- **CRA-I8** — Model substitution cannot expand worker authority.
- **CRA-I9** *(revised)* — De-escalation is permitted only into task regions whose acceptance is deterministically checkable or independently validated; absent such a check, the current tier is retained regardless of estimated sufficiency.
- **CRA-I10** — Validation remains logically separate from execution.
- **CRA-I11** — Task contracts preserve unresolved ambiguity rather than fabricating certainty.
- **CRA-I12** — Resource optimization cannot override the minimum acceptance-quality threshold.

## 44. Program Alignment and Terminology

CRA is a component of the Sovereign Systems Research Program, not a sixth independent system. Pending the program charter, the following vocabulary mapping is normative for CRA documents; where two terms conflict, the program term governs.

| CRA term | Program term | Owning document |
|---|---|---|
| Task contract | Objective contract | TCAIN thesis §6.1 |
| Worker | Sovereign node | Orchestration Workspace §5.3 |
| Conductor | Conductor | Shared |
| Validator | Gate / external validator | Workspace gate system; TCAIN §6.10 |
| Handoff packet | Checkpoint / handoff snapshot | SOVEREIGN phase-handoff convention |
| Tier 4 invocation | TCAIN node launch | TCAIN thesis |
| C_accepted | Cost per accepted work | Unified evaluation plane |
| TCH | Confirmation-file lifecycle (operational ancestor) | SOVEREIGN governance chain |

**Layer position.** In the program's control stack, CRA is the **orchestration-policy layer**: it sits between the substrate (the Orchestration Workspace, which supplies governed processes, identity, leases, and authority) and deep cognition (TCAIN nodes, which supply Tier-4 reasoning). ATG supervises project trajectory from above; CRA routes cognitive resources within tasks. CRA is thereby the formal answer to a question raised in program review — *not every intelligent operation should be a TCAIN node* — by specifying when one is justified.

## 45. Expected Scientific Contribution

If supported experimentally, CRA contributes a framework for treating inference capability as a schedulable resource over persistent task trajectories:

```text
Traditional:
    Agent = Model

CRA:
    Agent/Worker = Persistent Task State + Role + Authority
    Model        = Replaceable Cognitive Executor
    Allocation   = (Generator, Verifier) pair
```

The orchestration system then reasons separately about: what work exists; what the worker is allowed to do; what the worker currently understands; what cognitive capability the work requires; which resources supply that capability; and when that assignment should change.

## 46. Cognitive Scheduling as a Systems Abstraction

Operating systems allocate CPU time, memory, storage, devices, and priority; distributed systems allocate nodes, bandwidth, replicas, and jobs. CRA proposes an analogous abstraction: a cognitive system can allocate reasoning depth, specialization, context capacity, modality support, and model capability according to task state. Language models become heterogeneous cognitive processors; the orchestration layer becomes a cognitive scheduler; the task contract becomes the execution specification; the persistent worker becomes the process identity; the validator becomes an acceptance boundary.

The analogy has a hard edge, stated rather than glossed: an OS checkpoint is a lossless byte copy, while a CRA handoff is lossy semantic compression. At that edge the correct analog is the human shift handoff (§21), with its own empirical literature, not process migration. The abstraction remains useful because it shifts engineering attention away from model personality and toward measurable allocation, state, authority, and cost.

## 47. Commercial and Engineering Significance

If successful, CRA is useful where several model classes are available; inference costs vary substantially; local hardware is constrained; tasks persist; models specialize; complex work contains routine phases; interruptions occur; and human oversight is required. Applications include software engineering, scientific research, technical architecture, multimodal analysis, long-running research assistants, private local AI workstations, industrial engineering, and agent orchestration platforms.

The commercial advantage is not "uses many models." It is: *the system spends expensive cognition only where the work demonstrates that it is needed, while preserving task continuity and requiring workers to demonstrate understanding before they act.* A further differentiator follows from §20: characterization of the high-switching-cost regime — serial hosting, constrained VRAM — describes the deployment reality of most private and on-premise operators, and is unstudied by laboratories for whom switching is nearly free.

## 48. Negative Results and Falsification

A scientifically useful implementation must permit CRA to fail. Possible null results:

- **Null A** — TCH reduces misunderstanding but consumes more time and inference than the errors it prevents.
- **Null B** — ACT reduces call-level cost but increases rework, yielding no reduction in total accepted-task cost.
- **Null C** — Model substitution causes enough trajectory divergence that persistent role switching is unreliable.
- **Null D** — Comprehension telemetry does not predict task difficulty.
- **Null E** — A well-chosen static specialist performs as well as dynamic routing.
- **Null F** — The strongest model remains sufficiently cost-effective that adaptive de-escalation has negligible practical value.
- **Null G** — Model capability profiles fail to transfer across task variants.
- **Null H — Keystone failure.** H6 and H8 both fail. CRA then degenerates into cascade routing with persistence bookkeeping, and its residual contribution is limited to the contract and authority layer. This outcome would be published as such, under that description.

Any of these findings materially narrows the architecture. The research program preserves failed runs and publishes the outcome independently of whether CRA is supported.

## 49. Discussion

The key theoretical claim of Cognitive Resource Allocation is not that intelligence can be perfectly measured. It is that different cognitive resources have different opportunity costs, and the need for those resources changes during work. The system treats intelligence provision as an allocation problem under uncertainty.

Task-Comprehension Handshake contributes an unusual source of state information to that problem. A worker that identifies three unresolved ambiguities, a conflict between requirements, an unexpected dependency, and a prohibited change necessary for its proposed method has already provided evidence that the task is cognitively different from one in which all requirements are explicit, a deterministic test defines success, the architecture is frozen, and the implementation consists of three bounded edits. The handshake therefore serves simultaneously as a comprehension-control mechanism, an uncertainty detector, a complexity probe, and a routing input — and the last of these is the keystone (§27): it is the architecture's only leading indicator, and the hypothesis that it works (H6) is the one on which the routing contribution stands or falls.

Adaptive Cognitive Tiering extends the reasoning across the trajectory. The system does not permanently conclude that a task is easy or hard. It repeatedly asks whether the present state still justifies its current allocation — of both the generator and the verifier.

## 50. Conclusion

This thesis proposes Cognitive Resource Allocation, a stateful orchestration architecture for heterogeneous AI systems, combining: Task-Comprehension Handshake; explicit task contracts; persistent worker identity; model-independent role continuity; multidimensional capability profiles; Adaptive Cognitive Tiering; bidirectional escalation and de-escalation under the deterministic-validation rule; generator-verifier allocation; structured model handoff; resource accounting; and independent validation.

The central research claim:

> The cognitive capability assigned to a task should vary with the evolving demands of that task, while the identity, objective, authority, and accumulated state of the worker remain persistent outside the model.

The execution loop:

```text
UNDERSTAND → CONTRACT → ASSESS → ALLOCATE → EXECUTE → OBSERVE → RE-TIER → HAND OFF WHEN NEEDED → VALIDATE
```

The problem is no longer merely *which AI is best*, nor *how many models should debate*. It becomes: **what form and amount of machine cognition is justified by the present state of the work, which available resources can supply it most efficiently, and how can those resources be changed without losing the task itself?**

If controlled experiments demonstrate that CRA reduces misunderstanding, rework, and total cost while preserving or improving accepted-task quality, the result supports a broader systems principle: machine cognition can be engineered as a dynamically scheduled resource rather than treated as an indivisible property of a fixed artificial agent. If the experiments fail — including the specific keystone failure of Null H — the architecture provides equally useful evidence about the limits of model substitution, self-assessment, semantic task contracting, and adaptive routing. Either outcome moves the concept from orchestration intuition to testable cognitive-systems engineering.

---

## References

- Aggarwal, P., et al. (2023). *AutoMix: Automatically Mixing Language Models.* arXiv:2310.12963. Reliability-informed routing among differently sized models, using self-verification by the smaller model.
- Chen, L., Zaharia, M., & Zou, J. (2023). *FrugalGPT: How to Use Large Language Models While Reducing Cost and Improving Performance.* arXiv:2305.05176. LLM cascade strategies for cost-performance optimization.
- Du, Y., Li, S., Torralba, A., Tenenbaum, J. B., & Mordatch, I. (2023). *Improving Factuality and Reasoning in Language Models through Multiagent Debate.* arXiv:2305.14325.
- Gonuguntla, A. (2026). *The Replay Gap: Static Evaluation of Model Switching in LLM Agents Scores the Wrong World.* arXiv:2608.08239. Live branching on SWE-bench trajectories; swaps rewrite 61–94% of post-fork actions; static replay mispredicts every success-relevant outcome; serving-configuration-dependent determinism (FP8 vs. AWQ).
- Graves, A. (2016). *Adaptive Computation Time for Recurrent Neural Networks.* arXiv:1603.08983.
- Madaan, A., et al. (2023). *Self-Refine: Iterative Refinement with Self-Feedback.* arXiv:2303.17651.
- Ong, I., et al. (2024). *RouteLLM: Learning to Route LLMs with Preference Data.* arXiv:2406.18665.
- Ramírez, G., Birch, A., & Titov, I. (2024). *Optimising Calls to Large Language Models with Uncertainty-Based Two-Tier Selection.* Uncertainty-driven routing and cascading between differently capable models.
- Shazeer, N., et al. (2017). *Outrageously Large Neural Networks: The Sparsely-Gated Mixture-of-Experts Layer.* arXiv:1701.06538.
- Shinn, N., et al. (2023). *Reflexion: Language Agents with Verbal Reinforcement Learning.* arXiv:2303.11366.
- Smith, R. G. (1980). *The Contract Net Protocol: High-Level Communication and Control in a Distributed Problem Solver.* IEEE Transactions on Computers, C-29(12), 1104–1113.
- Srivastava, A., Khojastepour, M. A., Chakradhar, S., & Ulukus, S. (2026). *RunAgent: Interpreting Natural-Language Plans with Constraint-Guided Execution.* arXiv:2605.00798.
- Starmer, A. J., et al., for the I-PASS Study Group (2014). *Changes in Medical Errors after Implementation of a Handoff Program.* New England Journal of Medicine, 371, 1803–1812. Structured shift-handoff bundle reducing medical errors and preventable adverse events; empirical grounding for structured state transfer between agents.
- Wang, C., & Shu, Y. (2026). *MetaCogAgent: A Metacognitive Multi-Agent LLM Framework with Self-Aware Task Delegation.* arXiv:2605.17292. Self-assessed task-capability alignment; 8.7% gain over best routing baseline on MetaCog-Eval; used here as an effect-size prior.
- Wang, J., et al. (2024). *Mixture-of-Agents Enhances Large Language Model Capabilities.* arXiv:2406.04692.
- Xu, X., et al. (2026). *RoadmapBench: Evaluating Long-Horizon Agentic Software Development Across Version Upgrades.* arXiv:2605.15846. 115 tasks, 17 repositories, 5 languages; median modification ~3,700 lines across 51 files; strongest evaluated model resolves 39.1%.

---

## Canonical Definitions

**Cognitive Resource Allocation (CRA):** A stateful AI orchestration architecture in which persistent worker roles operate under explicit task contracts and are dynamically assigned heterogeneous cognitive resources — as generator-verifier pairs — according to evolving task demand, capability requirements, uncertainty, consequence, resource constraints, and observed execution performance.

**Task-Comprehension Handshake (TCH):** A bounded pre-execution protocol requiring a worker to demonstrate its interpretation of objective, constraints, scope, assumptions, authority, method, and success conditions before consequential execution is authorized.

**Adaptive Cognitive Tiering (ACT):** A bidirectional runtime routing mechanism that escalates or de-escalates the cognitive capability assigned to a persistent worker as the task's complexity, uncertainty, risk, modality, and execution state change — with de-escalation permitted only into deterministically checkable or independently validated regions.

**Core principle:** The work persists. The role persists. The state persists. The model does not have to.
