# Cognitive Resource Allocation (CRA)

Adaptive Cognitive Tiering and Task-Comprehension Handshakes for Stateful Heterogeneous Artificial Intelligence Systems.

CRA proposes treating machine cognitive capability as a dynamically scheduled resource rather than a static per-task assignment, on the argument that complex tasks exhibit non-stationary cognitive demand. It combines a Task-Comprehension Handshake (TCH) — a bounded pre-execution protocol that establishes an explicit task contract before work begins — with Adaptive Cognitive Tiering (ACT), a runtime controller that escalates or de-escalates the capability assigned to a persistent worker as complexity, uncertainty, criticality, and resource conditions evolve. An allocation is a (generator, verifier) pair rather than a single model, and CRA separates role, worker, and model identity so the models occupying a worker can change without losing task ownership or authority. No performance advantage is claimed before controlled experimentation.

- **Author:** Samuel Lawson — Sovereign Systems Research Program, Dark Science Division
- **License:** CC BY-NC-ND 4.0
- **Status:** Architectural thesis and experimental prospectus. Empirical superiority not yet established; no performance advantage is claimed before controlled experimentation.

## Canonical document — cite this version

- [`COGNITIVE_RESOURCE_ALLOCATION_THESIS_v1.0.md`](./COGNITIVE_RESOURCE_ALLOCATION_THESIS_v1.0.md) — **v1.0 Research Baseline**
  - SHA-256: `5b9e9e2ec3e7ca466369e48bd0ca75fcaa76faa602dc79120b65e2935b03ccc1`

## Archived editions

- [`versions/COGNITIVE_RESOURCE_ALLOCATION_THESIS_v0.2.md`](./versions/COGNITIVE_RESOURCE_ALLOCATION_THESIS_v0.2.md) — validated prior edition, fully contained in v1.0; preserved for the audit trail.
  - SHA-256: `589f04aa98f12e2b3ccb3bba8b637426330ad5a72aa1cb3772fcb7259745c90f`

**Lineage:** v0.1 (initial multi-model draft) → v0.2 (independent validation pass) → v1.0 (enterprise restructure merged with all v0.2 corrections). Full change logs are recorded in each document's front matter.

## Program context

CRA is a component of the Sovereign Systems Research Program, not a standalone system. It is the **orchestration-policy layer**: it sits between the Sovereign Orchestration Workspace (governed execution substrate) and TCAIN (deep adversarial cognition, invoked as CRA's Tier 4), with ATG supervising project trajectory from above. Related program theses: SOVEREIGN, [TCAIN](https://github.com/darksciencedivision-ctrl/trajectory-constrained-adversarial-intelligence-nodes), [ATG](https://github.com/darksciencedivision-ctrl/adversarial-trajectory-graphs), BioDigital Jazz.
