# Open Questions — Dynamic Bucket Tree of Permutation (D-BTP)

**Project:** Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document type:** Open research questions and collaboration agenda  
**Status:** Research hypotheses and design questions; not validated performance claims  
**Version:** 1.0.0-draft  
**Last updated:** 2026-11-23

## 1. Purpose and scope

D-BTP extends Bucket Tree of Permutation (BTP) from structural matching and unaligned-AND similarity toward dynamically generated, constraint-guided structural hypotheses. A bucket is a versioned hypothesis state; candidate relations may be generated in response to its current commitments, constraints, evidence, and directional policy. Directional fields influence both **which hypotheses are generated** and **which receive attention**; new evidence can subsequently revise those fields.

This document catalogs unresolved questions rather than claiming answers. It is intended to help researchers select tractable experiments, publish counterexamples, develop conformance tests, and relay reusable findings. A question's presence here does not imply that D-BTP has solved it or that the proposed mechanism will outperform simpler alternatives.

The central research challenge is to determine **when dynamic generation and coupled directional selection yield measurable benefits, at what computational and epistemic cost, and under what correctness guarantees**.

## 2. How to use this question registry

Each question has a stable identifier (`OQ-...`), a research question, a reason it matters, and a suggested falsification or evaluation route. IDs should remain stable across revisions. Questions are grouped by theme, not ranked by presumed importance. Researchers are encouraged to report negative results and counterexamples alongside positive results.

Suggested outcome states for future tracking: `open`, `under investigation`, `partially resolved`, `resolved under assumptions`, and `superseded`. Any claim of resolution should name the assumptions, evidence, implementation version, datasets, and remaining limitations.

## 3. Foundations: what is genuinely new?

### OQ-FND-001 — Boundary between static and dynamic BTP
**Question:** Which task classes require state-dependent candidate discovery rather than a sufficiently rich initial candidate pool?  
**Why it matters:** Dynamic generation may merely defer work that a static method could perform efficiently.  
**Probe:** Compare identical constraint and scoring semantics under fixed candidate lists, lazy enumeration, and genuinely state-conditioned generation; report coverage, runtime, memory, and solution quality.

### OQ-FND-002 — Expressiveness of structural hypotheses
**Question:** What minimal representation supports node pairs, many-to-one relations, latent actors, conditional links, and newly invented structural types without making consistency checking intractable?  
**Probe:** Specify a typed hypothesis algebra and measure representational coverage against verification cost.

### OQ-FND-003 — Equivalence of search histories
**Question:** When do two different acceptance/rejection histories denote the same future-relevant bucket state?  
**Probe:** Prove sufficient equivalence conditions and compare exact state hashing with approximate deduplication; identify unsafe merges.

### OQ-FND-004 — Structural search versus inference
**Question:** Which conclusions are feasibility results, which are probabilistic evidence assessments, and which are causal or identity claims?  
**Probe:** Define output contracts that explicitly label each claim type and test whether users can distinguish them.

## 4. Dynamic buckets and candidate generation

### OQ-DYN-001 — Generator completeness
**Question:** Can a dynamic generator guarantee discovery of every relevant candidate under finite assumptions?  
**Probe:** Specify fairness and exhaustiveness assumptions; construct adversarial tasks where a plausible generator misses the optimum.

### OQ-DYN-002 — Quiescence versus closure
**Question:** How can the system distinguish a temporarily empty candidate frontier from a provably closed search space?  
**Probe:** Design closure certificates and test whether delayed evidence or plugin changes invalidate apparent completion.

### OQ-DYN-003 — Reopening rejected hypotheses
**Question:** When should new evidence or altered assumptions permit a previously rejected hypothesis to be reconsidered?  
**Probe:** Separate logically impossible candidates from policy-deprioritized and evidence-disfavored candidates; evaluate revision rules.

### OQ-DYN-004 — Candidate explosion
**Question:** Which generation controls reduce combinatorial growth without hiding promising hypotheses?  
**Probe:** Compare beam limits, adaptive branching, constraint-first filtering, novelty thresholds, and diversity portfolios under equal budgets.

### OQ-DYN-005 — Generator provenance
**Question:** What minimal metadata makes a dynamically generated candidate reproducible across agents and software versions?  
**Probe:** Replay candidate streams using state hashes, plugin versions, random seeds, and policy snapshots.

## 5. Constraints, correctness, and complexity

### OQ-CON-001 — Sound pruning with partial knowledge
**Question:** What proof obligations must a constraint plugin satisfy before it may prune a branch?  
**Probe:** Define three-valued or four-valued outcomes, construct counterexamples for `unknown` treated as `false`, and validate pruning certificates.

### OQ-CON-002 — Constraint interaction
**Question:** How can locally valid candidate relations produce globally inconsistent structural compositions, and how early can those conflicts be detected?  
**Probe:** Benchmark incremental propagation against full recomputation with mixed cardinality and temporal constraints.

### OQ-CON-003 — Conditional constraints
**Question:** How should constraints whose applicability depends on unobserved or evolving context be represented and re-evaluated?  
**Probe:** Build dependency graphs and measure correctness under context updates.

### OQ-CON-004 — Plugin trust and isolation
**Question:** How should the engine handle incorrect, nonterminating, nondeterministic, or adversarial constraint plugins?  
**Probe:** Use sandbox limits, differential validators, proof-carrying results, and fault-injection tests.

### OQ-CON-005 — Complexity boundaries
**Question:** Which restricted D-BTP problem families admit tractable exact algorithms, approximation bounds, or fixed-parameter methods?  
**Probe:** Formalize reductions and analyze parameterized cases such as bounded treewidth, bounded degree, or restricted relation arity. Do not assume a general polynomial solution.

## 6. Directional fields: generation and selection as one system

### OQ-DIR-001 — Coupling benefit
**Question:** Does coupling candidate generation with directional selection outperform generating first and scoring afterward?  
**Probe:** Ablate generation guidance and selection guidance separately while holding compute and candidate budget constant.

### OQ-DIR-002 — Field representation
**Question:** Should directional fields be scalar objectives, vector-valued policies, learned programs, constraint-conditioned distributions, or composable structural units?  
**Probe:** Compare expressiveness, calibration, transfer, and auditability on shared benchmarks.

### OQ-DIR-003 — Multiobjective conflict
**Question:** How should the system balance explanatory fit, novelty, uncertainty reduction, cost, risk, and diversity when objectives conflict?  
**Probe:** Compare weighted aggregation, lexicographic ordering, Pareto portfolios, and constrained optimization.

### OQ-DIR-004 — Policy-induced blind spots
**Question:** Can directional fields systematically suppress the very hypotheses that would disconfirm them?  
**Probe:** Inject counterexamples outside the current preference region; measure recovery with random exploration, adversarial critics, and diversity reserves.

### OQ-DIR-005 — Calibration and transfer
**Question:** When does a direction field learned on one task remain useful on a different structural domain?  
**Probe:** Report transfer performance, out-of-distribution failure, and negative-transfer rates rather than only average gains.

### OQ-DIR-006 — Resource allocation
**Question:** What is the optimal division of limited compute among candidate invention, constraint validation, evidence acquisition, and policy improvement?  
**Probe:** Measure anytime performance and regret under fixed wall-clock, memory, and token budgets.

## 7. Weak evidence, counterevidence, and epistemic safeguards

### OQ-EVD-001 — Search value without proof value
**Question:** Under what conditions can weak or noisy signals improve search efficiency without improving, or while even harming, inference accuracy?  
**Probe:** Separate ranking utility from evidential strength; report false attribution and calibration alongside search cost.

### OQ-EVD-002 — Dependent evidence
**Question:** How can the system avoid double counting correlated signals from the same underlying source?  
**Probe:** Construct provenance dependency graphs and compare naive aggregation with dependency-aware scoring.

### OQ-EVD-003 — Active counterevidence
**Question:** Which evidence-gathering actions most efficiently discriminate between competing structural hypotheses?  
**Probe:** Compare information gain, expected falsification, and random acquisition using held-out ground truth.

### OQ-EVD-004 — Directional similarity and REN
**Question:** When does a directional relational measure provide useful information beyond symmetric metric similarity?  
**Probe:** Define asymmetric tasks with known target directions and compare against strong symmetric and learned-metric baselines.

### OQ-EVD-005 — Evidence drift
**Question:** How should evidence credibility and relevance change over time, especially when sources are updated or invalidated?  
**Probe:** Replay evidence revisions and test whether dependent scores and conclusions are correctly recomputed.

### OQ-EVD-006 — Responsible attribution
**Question:** What confidence, privacy, and independent corroboration requirements should govern claims about latent blockchain actors?  
**Probe:** Evaluate on synthetic or consented datasets; separate behavior clusters from real-world identities and quantify false-positive harms.

## 8. Multi-agent competition, relay, and collective learning

### OQ-MAG-001 — When do multiple agents help?
**Question:** For which tasks does agent diversity exceed its coordination and communication costs?  
**Probe:** Compare single-agent, homogeneous multi-agent, heterogeneous multi-agent, and independent ensemble baselines under equal total budgets.

### OQ-MAG-002 — Productive disagreement
**Question:** How can competing hypotheses be preserved long enough to discover decisive counterevidence without wasting resources?  
**Probe:** Evaluate top-K diversity, Pareto portfolios, adversarial review, and early-consensus policies.

### OQ-MAG-003 — Relay semantics
**Question:** What evidence and validation metadata must travel with a Structural Hypothesis Unit (SHU) for another agent to reuse it safely?  
**Probe:** Test schema compatibility, provenance preservation, version negotiation, and receipt validation.

### OQ-MAG-004 — Avoiding collective error amplification
**Question:** How can relay networks prevent one flawed hypothesis or contaminated source from becoming apparent consensus?  
**Probe:** Inject a shared false premise and measure propagation with independent validators, lineage tracking, and source-diversity requirements.

### OQ-MAG-005 — Reuse versus genuine learning
**Question:** What distinguishes caching a useful hypothesis from improving the general candidate generator or search policy?  
**Probe:** Measure performance on novel held-out tasks after removing task-specific memory.

### OQ-MAG-006 — Collective credit assignment
**Question:** How should contributions from generators, critics, validators, and relay nodes be credited when a result emerges collectively?  
**Probe:** Compare marginal contribution estimates and controlled ablations while reporting computational overhead.

## 9. Recursive field evolution and open-ended growth

### OQ-EVO-001 — What counts as validated RSI?
**Question:** What measurable criteria distinguish self-modification, local adaptation, transferable improvement, and recursive self-improvement?  
**Probe:** Require independent evaluations across multiple generations, held-out tasks, rollback tests, and compute-normalized gains.

### OQ-EVO-002 — Search over search policies
**Question:** Can directional fields be generated and evaluated as first-class structural hypotheses without unbounded meta-search cost?  
**Probe:** Compare fixed policy, parameter tuning, policy composition, and operator invention with nested budget accounting.

### OQ-EVO-003 — Four growth frontiers
**Question:** How should hypothesis, representation, operator, and relay frontiers interact, and which frontier creates the largest marginal gain?  
**Probe:** Freeze three frontiers at a time; measure task coverage, transfer, and validation cost.

### OQ-EVO-004 — Residual-driven invention
**Question:** When do unexplained structural residuals justify inventing new relation types or operators rather than refining existing ones?  
**Probe:** Use synthetic worlds with known missing operators and measure recovery, overfitting, and false invention.

### OQ-EVO-005 — Open-endedness criteria
**Question:** What finite, falsifiable indicators support a claim of open-ended structural evolution?  
**Probe:** Track novel capability classes, validated transfer, representation expansion, and diminishing-return curves across increasing budgets.

### OQ-EVO-006 — Governance of self-revision
**Question:** Which policy changes may be deployed automatically, and which require sandbox review or human approval?  
**Probe:** Define promotion gates, capability scopes, rollback conditions, and independent conformance suites.

## 10. Application-specific questions

### OQ-APP-001 — Dynamic starmap similarity
**Question:** How do structural noise, missing edges, noninjective mappings, and changing topology affect dynamic matching accuracy?  
**Probe:** Generate controlled perturbations with known correspondence and report exactness, robustness, and runtime.

### OQ-APP-002 — Blockchain latent actor attribution
**Question:** Can dynamic many-to-one behavioral hypotheses improve structural explanation without inducing unjustified real-person identification?  
**Probe:** Use synthetic actor graphs, blinded evaluation, abstention thresholds, and alternative explanations.

### OQ-APP-003 — Strategic search and games
**Question:** Can D-BTP discover and evaluate strategic structural hypotheses in games beyond what ordinary tree search already captures?  
**Probe:** Compare with standard game-tree search, Monte Carlo tree search, and learned policy baselines under matched compute.

### OQ-APP-004 — Cross-domain portability
**Question:** Which candidate, constraint, and direction-field contracts are reusable across matching, attribution, planning, and diagnosis?  
**Probe:** Measure engineering changes, conformance pass rates, and transfer quality when moving between domains.

## 11. Priority research packages

The following packages are suggested starting points, not commitments or established milestones.

| Package | Main questions | Minimal deliverable | Key decision criterion |
|---|---|---|---|
| P1 — State and correctness | OQ-DYN-002, OQ-CON-001, OQ-FND-003 | Executable bucket contract and counterexample suite | No unsafe pruning or closure claims |
| P2 — Dynamic-generation value | OQ-FND-001, OQ-DYN-001, OQ-DYN-004 | Static-vs-dynamic benchmark | Better coverage or quality per equal budget |
| P3 — Coupled direction fields | OQ-DIR-001, OQ-DIR-004, OQ-DIR-006 | Ablation study with blind-spot probes | Benefit survives matched compute and robust baselines |
| P4 — Weak-evidence reliability | OQ-EVD-001, OQ-EVD-002, OQ-EVD-003 | Synthetic evidence benchmark | Search gains without unacceptable calibration loss |
| P5 — Multi-agent relay | OQ-MAG-001, OQ-MAG-003, OQ-MAG-004 | SHU exchange and fault-injection tests | Correct provenance and net value after overhead |
| P6 — Recursive evolution | OQ-EVO-001, OQ-EVO-002, OQ-EVO-004 | Sandboxed policy evolution experiment | Reproducible held-out improvements |

Recommended order: establish sound state and constraint semantics before performance optimization; establish reliable evidence and relay before attempting recursive policy promotion.

## 12. Common evaluation discipline

Across packages, record:

- **Correctness:** hard-constraint violations, unsafe prunes, closure errors, state-replay failures.
- **Search outcomes:** best feasible score, optimality gap where known, hypothesis diversity, coverage, time-to-first-valid solution.
- **Resources:** wall-clock time, memory, calls per plugin, tokens where applicable, evidence-acquisition cost.
- **Epistemic quality:** calibration, false-positive and false-negative rates, abstention quality, sensitivity to counterevidence.
- **Generalization:** held-out performance, cross-domain transfer, robustness to drift, negative transfer.
- **Reproducibility:** code and dataset versions, random seeds, policy snapshots, full provenance and declared assumptions.

At minimum, compare: static BTP; dynamic BTP without directional guidance; dynamic BTP with fixed guidance; and dynamic BTP with adaptive guidance. Add strong task-specific baselines. Match total compute and report variability over multiple runs. Where exact solutions are unavailable, do not imply that a higher heuristic score proves global optimality.

## 13. Counterexamples and negative results to seek actively

1. A static candidate generator that dominates a dynamic one because candidate discovery overhead is excessive.
2. A directional field that accelerates early progress but systematically misses a rare high-value branch.
3. A weak-evidence feature that improves search ranking yet worsens attribution calibration.
4. A pruning plugin that misclassifies `unknown` as infeasible and silently discards the optimum.
5. A relay network that amplifies correlated false evidence despite high apparent consensus.
6. A self-modifying field that improves its training tasks but regresses on held-out tasks.
7. A state deduplication rule that merges superficially similar buckets with different future possibilities.
8. An apparently open-ended generator whose novelty saturates under longer evaluation.

Publishing these failures would materially strengthen the framework by clarifying its domain of validity.

## 14. Interfaces to other D-BTP documents

| Document | Relevant questions |
|---|---|
| `docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md` | OQ-FND series |
| `docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md` | OQ-DYN series |
| `docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md` | OQ-CON series |
| `docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md` | OQ-DIR series |
| `docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md` | OQ-EVD series |
| `docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md` | OQ-DIR and OQ-EVO series |
| `docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md` | OQ-MAG series |
| `docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md` | OQ-EVO series |
| `docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md` | State consistency and closure |
| `docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md` | Generation and plugin soundness |
| `docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md` | Directional guidance and budget control |
| `docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md` | Evidence provenance, relay, learning gates |
| `docs/cases/CASE-001-Blockchain-Actor-Attribution.md` | OQ-APP-002 |
| `docs/cases/CASE-002-Dynamic-Starmap-Similarity.md` | OQ-APP-001 |
| `docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md` | OQ-MAG series |
| `docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md` | OQ-DIR and active sensing |
| `docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md` | OQ-EVO-001, 002, 006 |
| `docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md` | OQ-EVO-003, 004, 005 |

See also `FUTURE-DIRECTIONS.md` for strategic research directions, `TESTABLE-HYPOTHESES.md` for operational predictions, and `VALIDATION-ROADMAP.md` for staged verification plans. These files serve different purposes: questions, hypotheses, and experiments should not be conflated.

## 15. Contribution and issue template

A proposed question or answer should include:

```text
Question ID / proposed title:
Claim or uncertainty:
Task domain and assumptions:
Why existing methods may be insufficient:
Proposed experiment or proof:
Strongest relevant baseline:
Success criterion and failure criterion:
Counterexample or alternative explanation:
Reproducibility artifacts:
Evidence status (hypothesis / simulated / independently replicated):
Related D-BTP documents:
```

If an experiment addresses several questions, state which conclusions are supported by which measurements. Preserve explicit unresolved leftovers; an inconclusive result can become a new research unit rather than being silently dropped.

## 16. Closing perspective

The promise of D-BTP is not a claim that one algorithm solves general structural inference or intelligence. Its research value lies in an explicit, testable architecture for **dynamic hypothesis generation, constraint-safe composition, directional exploration, evidence-aware feedback, and transferable structural learning**. The most useful next step is to find both the cases where these mechanisms help and the cases where they do not.

**Research posture:** open hypotheses, explicit assumptions, falsifiable tests, reproducible artifacts, and collective learning friendly.
