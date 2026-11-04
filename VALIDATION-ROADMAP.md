# D-BTP Validation Roadmap

**Project:** Dynamic Bucket Tree of Permutation — Directional Structural Generation and Hypothesis Evolution  
**Status:** Proposed research and validation plan; no experimental results are asserted  
**Version:** 1.0.0 (research roadmap)  
**Scope:** Algorithmic correctness, empirical utility, evidence governance, structural relay, and controlled evolution

## 1. Purpose and evidence standard

D-BTP proposes a stateful structural-hypothesis search architecture in which dynamic candidate generation, constraint checking, directional guidance, and feedback are coupled. This roadmap turns the research program into executable validation gates. A specification, reference implementation, demonstration, or plausible synthetic example is **not** itself evidence of superior performance. Every positive claim must be tied to a documented benchmark, baseline, measurement, and replication protocol.

The primary questions are: (i) are state transitions and pruning sound under declared assumptions; (ii) when does dynamic generation outperform static candidate enumeration; (iii) does directional coupling add value beyond post-generation ranking; (iv) can weak evidence improve exploration without being treated as proof; (v) when do multi-agent relay and field adaptation improve independently evaluated outcomes; and (vi) what evidence, if any, supports open-ended structural capability growth?

## 2. Traceability to the repository

| Source | Validation responsibility |
|---|---|
| D-BTP-001–003 | Search formulation, dynamic state, constraint semantics |
| D-BTP-004–006 | Directional fields, weak evidence, feedback coupling |
| D-BTP-007–008 | Multi-agent learning, structural growth and limits |
| SPEC-001 | Bucket state, ledger, transitions, lifecycle, reproducibility |
| SPEC-002 | Candidate generation, plugin contracts, hard constraints and sound pruning |
| SPEC-003 | Directional scoring, frontier control, budgets and field versions |
| SPEC-004 | Evidence provenance, relay receipts, learning lifecycle and RSI governance |
| CASE-001–003 | Application-oriented evaluation and synthetic demonstrations |
| EXT-001–003 | Biomimetic hypotheses, recursive field evolution, open-ended relay |
| OPEN-QUESTIONS.md | Questions motivating experimental packages |
| TESTABLE-HYPOTHESES.md | Hypothesis registry; individual identifiers should be mapped to tests before execution |

**Traceability rule:** before running an experiment, assign an immutable experiment ID, the exact hypothesis identifier from `TESTABLE-HYPOTHESES.md`, specification clauses, benchmark version, and intended decision threshold. Do not silently renumber hypothesis IDs.

## 3. Claims ladder

| Level | Permitted claim | Minimum evidence |
|---|---|---|
| L0: proposal | An algorithm or interface is specified | Reviewed document and explicit assumptions |
| L1: conformance | Implementation obeys declared contracts | Automated tests, invariant checks, negative tests |
| L2: feasibility | Method solves selected instances | Reproducible runs and independently checked outputs |
| L3: comparative benefit | Method improves a measured outcome | Fair baselines, repeated trials, uncertainty intervals |
| L4: generalization | Benefit transfers beyond development tasks | Held-out families, domain shifts and ablations |
| L5: validated adaptation | Learned policy improves future tasks | Frozen evaluation, rollback controls, replication |
| L6: open-ended growth | New reusable capabilities accumulate | Longitudinal independent tests and operator/representation audits |

No level implies the next. In particular, L5 does not establish general intelligence or unrestricted recursive self-improvement.

## 4. Common experimental protocol

### 4.1 Registration and data separation

Every experiment must specify its question, primary metric, direction of expected change, null comparison, constraints, resource budget, randomization, seeds, stopping rules, and planned analysis **before** inspecting final test outcomes. Separate development, validation, and locked test families. Record all modifications after registration.

### 4.2 Fair comparisons

Use equal or explicitly normalized limits for wall-clock time, CPU/GPU usage, memory, candidate evaluations, plugin calls, evidence queries, and agent communication. Report both solution quality and total cost. Distinguish *algorithmic benefit at equal compute* from *benefit gained by spending more compute*. For stochastic algorithms, run multiple predeclared seeds and use paired instances when possible.

### 4.3 Baseline ladder

| ID | Comparator | Purpose |
|---|---|---|
| B0 | Exhaustive search on tractable small instances | Exact correctness oracle |
| B1 | Static BTP, fixed candidate list | Original fixed-frontier reference |
| B2 | Dynamic BTP, no directional guidance | Isolate candidate regeneration |
| B3 | Dynamic BTP with fixed post-generation scoring | Isolate generation–selection coupling |
| B4 | Dynamic BTP with fixed guidance at generation and selection | Isolate feedback adaptation |
| B5 | Adaptive coupled D-BTP | Proposed integrated treatment |
| B6 | Multi-agent variant under matched total budget | Test relay/competition overhead and benefit |
| B7 | Learned-field variant evaluated on frozen holdouts | Test transfer and validated adaptation |

A baseline may be inapplicable to a particular benchmark. Record and justify exclusions; do not fabricate a universal baseline winner.

### 4.4 Core measurements

- **Correctness:** hard-constraint violations, invalid pruning decisions, oracle disagreement, transition-invariant failures.
- **Search utility:** feasible solutions found, objective gap to oracle or best-known bound, top-K coverage, time-to-first-valid hypothesis, search nodes expanded, candidate evaluations.
- **Efficiency:** CPU/GPU time, peak memory, evidence-query cost, plugin latency, total energy when measurable.
- **Exploration:** distinct hypothesis families, novelty, diversity, false-negative branch suppression, calibration of search priority.
- **Evidence:** provenance completeness, dependence-adjusted scoring, counterevidence discovery, spurious-correlation sensitivity.
- **Learning:** held-out gain, regression rate, policy rollback frequency, transfer success and total adaptation cost.

Use confidence intervals or other uncertainty estimates suited to the design. Report distributions and failures, not only means or best runs. Correctness violations are not averaged away by higher speed.

## 5. Benchmark families

### BK-01: Exact synthetic structural alignment

Generate small typed starmaps with known mappings, symmetries, controlled noise, and exhaustive or independently verified optima. Vary graph size, branching, relation density, missing edges, mapping cardinality and degree of ambiguity. Primary use: contract correctness and search completeness under stated conditions.

### BK-02: Dynamic discovery and delayed candidates

Construct instances where a candidate is only discoverable after a prior acceptance, exclusion, constraint propagation, or evidence update. Include cases where static candidate lists are complete, to measure dynamic overhead rather than presuming benefit.

### BK-03: Constraint stress and plugin faults

Mix hard, conditional, and soft constraints; introduce contradictory, incomplete, non-monotonic and version-mismatched plugins. Inject timeouts, stale state, invalid certificates, duplicate candidates and malformed responses. Test that uncertain results are not treated as hard rejection.

### BK-04: Directional-field landscapes

Create multiobjective landscapes with deceptive local optima, conflicting directions, sparse rewards, shifting objectives and variable evidence quality. Compare fixed and adaptive fields and Pareto-aware portfolios under matched budgets.

### BK-05: Weak evidence and counterevidence

Control evidence reliability, dependence, adversarial contamination and temporal drift. Include deliberately misleading directional signals and independent counterevidence. Measure utility without allowing weak signals to become proof of feasibility or identity.

### BK-06: Multi-agent competition and relay

Vary agent specialization, shared knowledge, disagreement, coordination cost, relay loss, stale versions and adversarial agents. Compare single-agent and multi-agent systems with identical aggregate budgets and independently scored hypothesis portfolios.

### BK-07: Cross-task and longitudinal learning

Train or adapt generators, fields or operators on one set of task families; evaluate on locked, shifted families. Track retained improvements, negative transfer, new operator reuse and regressions over multiple cycles.

### BK-08: Application-inspired synthetic cases

Use synthetic blockchain behavior attribution, dynamic starmap matching and strategic hypothesis search. For blockchain, measure **latent behavioral grouping** against synthetic ground truth; do not equate behavioral clusters with real-world people. Avoid private network identifiers or unjustified identity claims.

### BK-09: Open-ended operator and representation growth

Supply tasks that cannot be solved efficiently with a deliberately restricted initial operator library. Test whether proposed extensions are valid, reusable and independently useful. Compare against equal-budget hand-designed or randomly generated operator extensions.

## 6. Milestone M0 — Formalization and reproducibility

**Objective:** establish a frozen, testable contract surface before benchmarking.

**Deliverables:** versioned state schema; event/transition log; candidate and plugin interface definitions; directional field schema; evidence and relay envelopes; deterministic seed handling; reference examples; machine-readable experiment manifest; benchmark generator specification.

**Gate M0:** independent reviewers can reconstruct an instance, state transition, constraint decision, and experiment configuration from logged artifacts. Undefined lifecycle states and ambiguous hard/soft semantics block advancement.

**Exit evidence:** reviewed contracts, schema validation output, example traces and a published list of known underspecifications.

## 7. Milestone M1 — Conformance before runtime claims

**Objective:** demonstrate that a reference implementation respects SPEC-001 through SPEC-004.

**Required tests:**

1. Accepted/rejected ledger decisions remain consistent under branch and replay.
2. Hard constraints are evaluated with explicit plugin versions and provenance.
3. `Unknown`, timeout and error never silently become hard `Fail`.
4. Candidate regeneration reflects current state and preserves origin records.
5. Sound pruning only occurs with a valid declared justification.
6. Duplicate suppression does not collapse non-equivalent states.
7. Closed, quiescent and budget-terminated states remain distinct.
8. Directional scores affect prioritization but not hard feasibility.
9. Evidence dependency and counterevidence metadata survive relay.
10. Relay receipts, schema checks, version conflicts and rollback are auditable.
11. State snapshots can be replayed from immutable events where determinism is claimed.
12. Malformed plugin results fail safely and do not corrupt the ledger.

**Gate M1:** zero unexplained invariant violations in the registered conformance suite; all known exceptions documented with scope and severity. Test counts in earlier specifications should be mapped into a unified coverage matrix rather than merely summed.

## 8. Milestone M2 — Baseline dynamic-search validation

**Objective:** test whether dynamic candidate discovery is correct and useful.

**Design:** BK-01 and BK-02; compare B0, B1 and B2. Use exact oracles on small instances and independent bounds on larger ones. Separate fixed-frontier-complete instances from delayed-discovery instances.

**Primary outcomes:** oracle agreement, feasible-hypothesis recall, time to first feasible solution, total compute and memory. Analyze the regimes in which dynamic regeneration incurs overhead or introduces candidate redundancy.

**Gate M2:** no unaccounted hard-constraint errors; reproducible discovery of delayed candidates; a transparent comparative result, including negative findings. Performance superiority is not a prerequisite for reporting feasibility, but is required before claiming improvement.

## 9. Milestone M3 — Directional coupling and weak evidence

**Objective:** isolate the contribution of directional generation–selection coupling and evidence-aware exploration.

**Design:** BK-04 and BK-05; compare B2, B3, B4 and B5. Factorially vary guidance quality, evidence reliability, field update frequency and objective conflict. Include ablations disabling generation guidance, selection guidance, feedback, counterevidence and diversity preservation separately.

**Primary outcomes:** quality under equal budget, time to useful hypotheses, diversity, calibration, counterevidence yield and performance degradation under misleading evidence.

**Gate M3:** registered estimates with uncertainty and failure analysis; explicit confirmation that weak evidence never caused unjustified hard rejection. If coupling helps only under narrow conditions, publish those conditions.

## 10. Milestone M4 — Multi-agent relay and collective learning

**Objective:** establish whether competition, specialization and structural relay improve outcomes beyond equivalent single-agent compute.

**Design:** BK-06; compare B5 and B6, and include a no-relay multi-agent ablation. Vary communication overhead and agent diversity. Require receipt verification and provenance-preserving SHU exchanges.

**Primary outcomes:** best and top-K hypothesis quality, diversity, independent counterevidence discoveries, duplicate effort, latency, relay error rates and total resource use.

**Gate M4:** measurable benefit, neutral result or regression documented with total-cost accounting; no claim that agreement among agents is independent validation. Correlated evidence must not be counted multiple times.

## 11. Milestone M5 — Field and operator adaptation

**Objective:** distinguish ordinary search updates from generalizable learning.

**Design:** BK-07 and BK-09; freeze held-out tests before policy revisions. Compare B5 and B7 with a no-learning control, random-update control and manually tuned control. Test across multiple task distributions and time horizons.

**Primary outcomes:** held-out performance change, negative-transfer frequency, stability, rollback frequency, cumulative adaptation cost and independent operator reuse.

**Gate M5:** any claimed improvement is replicated on locked holdouts and survives relevant cost normalization. Changes that improve training instances alone are labeled adaptation, not validated RSI.

## 12. Milestone M6 — Open-ended structural evolution prospecting

**Objective:** investigate whether the system can expand representations or operator libraries in ways that support sustained, transferable capability growth.

**Design:** use BK-09 and cross-family longitudinal tasks; compare discovered extensions with random and human-designed alternatives. Evaluate operator validity, composability, reuse, novelty and capability retention. Introduce adversarial tests for benchmark gaming and complexity inflation.

**Primary outcomes:** verified novel operators, transfer to previously unseen tasks, persistent improvements across cycles, regression rate, total cost and reproducible extension provenance.

**Gate M6:** publish only the level of evidence achieved. More nodes, more operators, longer trajectories or self-modification do not by themselves demonstrate open-ended intelligence or AGI.

## 13. Work packages and dependency graph

```text
M0 Contract freeze and manifests
  |
  v
M1 Conformance and fault injection
  |
  v
M2 Dynamic search and exact-oracle baselines
  |
  v
M3 Directional coupling / weak evidence
  |
  +------------------+
  v                  v
M4 Multi-agent relay  M5 Field/operator adaptation
  |                  |
  +---------+--------+
            v
M6 Open-ended structural evolution prospecting
```

M4 and M5 may proceed in parallel once M3 evidence and governance controls are available. A failed gate triggers remediation or a narrower claim, not automatic cancellation of all exploratory work.

## 14. Experiment registry template

```yaml
experiment_id: DBTP-EXP-0001
hypothesis_ids: []              # exact identifiers from TESTABLE-HYPOTHESES.md
specification_refs: []
benchmark_id: BK-02
benchmark_version: 0.1.0
train_validation_test_split: frozen-before-test
primary_metric: feasible_recall_at_equal_budget
baselines: [B1, B2]
resource_budget:
  wall_time_seconds: null
  candidate_evaluations: null
  evidence_queries: null
seeds: []
pre_registered_analysis: null
stopping_rule: null
software_commit: null
plugin_versions: {}
field_version: null
artifact_manifest_hash: null
outcome: not-run
limitations: []
```

This is a suggested manifest, not an implemented schema. Set numeric budgets and seeds before execution. Retain both successful and failed run artifacts.

## 15. Minimum evidence package per experiment

An experiment release should contain: task and generator definitions; dataset licenses and provenance; frozen split manifests; exact software commit; plugin/field/operator versions; execution environment; seeds and budgets; raw result tables; invariant failures; analysis scripts; uncertainty estimates; counterexamples; limitations; and a concise reproducibility guide. For stochastic or non-deterministic components, document what can and cannot be replayed.

## 16. Acceptance criteria and decision rules

The following are **proposed governance rules**, not empirically established thresholds:

- **Correctness gate:** any unexplained invalid hard pruning or contradictory ledger transition blocks a correctness claim.
- **Comparative claim gate:** require predeclared primary metric, fair cost accounting and uncertainty reporting; improvement must be robust enough for the claim's scope.
- **Evidence gate:** weak or correlated evidence cannot override a sound hard constraint or justify real-world identity conclusions.
- **Learning gate:** independent held-out evaluation and regression checks precede promotion of a learned field/operator.
- **Relay gate:** imported hypotheses are untrusted until local schema, provenance and applicability checks pass.
- **Open-ended gate:** new representations/operators require independent utility and reuse evidence, not merely novelty labels.

The research team should pre-register numerical thresholds for specific benchmarks; this document deliberately does not invent universal pass rates.

## 17. Threats to validity and safeguards

**Selection bias:** publish all registered benchmark families and negative results.  
**Data leakage:** freeze held-outs and isolate agent memory from evaluation labels.  
**Unfair budgets:** report normalized and absolute compute and communication.  
**Evidence dependence:** model provenance graphs and correlated sources.  
**Metric gaming:** use multiple independently evaluated metrics and adversarial tests.  
**Unsound pruning:** preserve certificates and oracle-check small cases.  
**Distribution shift:** test shifted graph families, objective landscapes and evidence reliability.  
**Overfitting to synthetic worlds:** separate synthetic mechanism checks from external-validity claims.  
**Agent consensus illusion:** require independent evidence, not vote count.  
**Non-reproducible self-modification:** version, sandbox and rollback all promoted updates.

## 18. Responsible-use boundary for actor attribution

For CASE-001, the validated target should be **synthetic latent behavioral structure** or another appropriately authorized, ground-truthed setting. Blockchain transaction structure can support competing behavioral hypotheses; it does not alone establish the identity of a natural person. Do not present uncertain clustering as a finding about a named individual. Respect privacy, lawful access, data minimization and evidence provenance. Security and misuse review should accompany any extension to sensitive real-world attribution.

## 19. Proposed release stages

| Stage | Contents | Appropriate public wording |
|---|---|---|
| R0: theory release | Foundations, specifications, cases, open questions, figures | Proposed framework and testable hypotheses |
| R1: contract reference | Schemas, conformance tests, synthetic traces | Reference implementation conforms to tested contracts |
| R2: baseline study | Frozen benchmarks, baselines and raw outcomes | Measured benefits/limits in specified regimes |
| R3: learning study | Relay and held-out adaptation experiments | Evaluated transfer or adaptation within stated scope |
| R4: evolution study | Independently validated operator/representation growth | Evidence of specific structural capability growth |

A DOI for R0 preserves the research proposal; it is not certification that R1–R4 have been achieved.

## 20. Immediate next actions

1. Reconcile the 32 hypothesis entries in `TESTABLE-HYPOTHESES.md` with immutable experiment IDs and the 43 open questions in `OPEN-QUESTIONS.md`.
2. Build a machine-readable coverage matrix for SPEC-001–004, including negative and fault-injection tests.
3. Define BK-01/BK-02 generators and exact small-instance oracles before implementing adaptive guidance.
4. Freeze B1–B5 baseline configurations and cost-accounting rules.
5. Run M1 and M2, publish failures and revise contracts under explicit version control.
6. Only then expand to weak-evidence, multi-agent and learning claims.

## 21. Conclusion

D-BTP is best advanced through a **claims-ladder and contract-first** validation strategy: formalize the dynamic state, verify constraints and transitions, benchmark dynamic discovery, isolate directional coupling, evaluate weak evidence and relay, then test learning and structural growth on independent tasks. The roadmap is intentionally falsifiable. Negative results and boundary conditions are part of the intended scientific output.

---

*Research note: All experiments, thresholds and milestone gates in this document are proposals. No performance measurements, implementations or validated RSI results are claimed.*
