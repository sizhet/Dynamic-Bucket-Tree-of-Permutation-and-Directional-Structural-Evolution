# SPEC-002 — Candidate Generation and Constraint Plugins

**Project:** D-BTP — Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Status:** Proposed research specification, v1.0.0  
**Scope:** Candidate discovery, plugin contracts, constraint evaluation, propagation, and conformance  
**Companion:** SPEC-001 — Dynamic Bucket State Contract

## Abstract

Dynamic Bucket Tree of Permutation (D-BTP) treats a search bucket as an evolving structural hypothesis state rather than a fixed list of unresolved pairs. Candidate generation and constraint evaluation are therefore state-dependent operations. This specification defines interoperable contracts for generators, validators, propagators, and plugin orchestration. It separates *feasibility* from *evidence* and *search priority*, states conditions for sound rejection and pruning, and makes plugin behavior auditable across multi-agent and relay workflows. The contracts are proposals for implementation and testing, not claims of a completed or formally verified runtime.

## 1. Normative language and design goals

The words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** express requirements for implementations claiming conformance to this proposed specification. They do not imply that a deployed implementation currently exists.

A conforming subsystem aims to:

1. Discover candidate structural relations from the current bucket state and relevant context.
2. Evaluate candidate feasibility under explicit, versioned constraints.
3. Preserve hard-constraint soundness even when directional guidance is uncertain.
4. Support reproducible branching, propagation, provenance, and evidence-aware prioritization.
5. Permit domain-specific plugins without embedding domain assumptions in the D-BTP core.
6. Distinguish search completeness, generator coverage, and budget-bounded exploration.

## 2. Definitions

- **Bucket:** An evolving state carrying hypothesis decisions, structural composition, evidence, policy, provenance, and lifecycle metadata.
- **Candidate:** A proposed atomic or composite structural change, not necessarily a simple one-to-one node pair.
- **Generator:** A component proposing candidates using the bucket and admissible contextual information.
- **Constraint plugin:** A component assessing a proposed transition against a declared rule set.
- **Propagator:** A component deriving logically justified restrictions or implications from accepted facts and hard rules.
- **Evidence plugin:** A component producing observations, likelihood-oriented features, or directional guidance; it cannot independently establish hard infeasibility.
- **Sound rejection:** A rejection justified by a valid hard constraint, supported premises, and a traceable decision record.
- **Unknown:** Insufficient information to determine feasibility; distinct from rejection.
- **Coverage claim:** A declared condition under which a generator can be considered exhaustive for a specified candidate domain.

## 3. System boundary

The D-BTP core owns bucket transitions, event ordering, state fingerprints, scheduling, decision provenance, and lifecycle classification. Plugins own narrowly declared functions. The core MUST NOT silently promote a plugin's heuristic score to a hard constraint. Plugins MUST NOT directly mutate the canonical bucket; they return proposals or evaluations for the core to validate and commit.

```text
Bucket Snapshot + Domain Context + Directional Policy
                       |
                       v
              Candidate Generators
                       |
               Candidate Envelope
                       |
                       v
             Normalization / Dedup
                       |
                       v
          Hard Constraint Evaluators
                 /      |      \
              PASS    FAIL    UNKNOWN
                |       |        |
                v       v        v
           Propagation Reject   Defer / Probe
                |
                v
        Directional / Evidence Scoring
                |
                v
          Branch / Schedule / Commit
                |
                v
          New Bucket Snapshot + Audit
```

The order shown is a logical dependency graph, not a requirement to execute all plugins sequentially. Implementations MAY parallelize read-only operations against the same immutable snapshot.

## 4. Canonical inputs and versioning

Each invocation MUST identify the snapshot against which it was computed. At minimum:

```yaml
invocation_id: string
bucket_id: string
bucket_version: integer
state_fingerprint: string
context_ref: string
context_version: string
plugin_id: string
plugin_version: string
policy_version: string
budget:
  max_candidates: integer
  max_work_units: number
  deadline_ms: integer | null
seed: string | null
```

`deadline_ms` is a relative execution limit, not a wall-clock assertion. Implementations MAY use additional resource limits. Context references MUST obey the application's access and privacy policy. The core MUST reject or recompute results tied to stale bucket versions unless a documented equivalence rule proves reuse safe.

## 5. Candidate envelope contract

A candidate is represented as a typed proposal with an explicit action, operands, assumptions, and provenance.

```yaml
candidate_id: string
candidate_type: relation | grouping | assignment | exclusion | operator_extension | other
operation: add | remove | revise | test
operands:
  - entity_ref: string
    role: string
proposed_delta: object
preconditions: [predicate_ref]
assumptions: [assumption_ref]
origin:
  generator_id: string
  generator_version: string
  invocation_id: string
  source_refs: [string]
  derivation_refs: [string]
coverage_scope: string | null
priority_hints: object
```

A `candidate_id` MUST be stable under canonical serialization of the same logical proposal within its declared identity scope. Two candidates with equivalent surface labels but different preconditions or semantics MUST NOT be merged merely by string equality. A generator MUST label speculative assumptions separately from established facts.

### 5.1 Atomic and composite candidates

An atomic candidate changes one declared structural relation. A composite candidate proposes a coordinated set of changes, such as assigning multiple observed behaviors to one latent actor. Composite proposals MUST declare whether their deltas are **all-or-nothing** or **separably admissible**. The core MUST NOT partially commit an all-or-nothing candidate.

### 5.2 Non-bijective mappings

Candidate schemas MUST support one-to-many, many-to-one, and many-to-many relations when the domain permits them. A generator MUST NOT assume injectivity or surjectivity unless those properties are declared as hard domain constraints. This matters for actor-to-behavior hypotheses, where one latent actor may explain multiple observations and one observation may initially have several competing explanations.

## 6. Generator interface

```text
GenerateCandidates(
    snapshot: BucketSnapshot,
    context: ContextView,
    policy: DirectionalPolicy,
    limits: GenerationBudget,
    cursor?: OpaqueCursor
) -> GenerationBatch
```

A `GenerationBatch` MUST contain:

```yaml
candidates: [CandidateEnvelope]
continuation_cursor: string | null
termination_reason: exhausted | budget | suspended | error
coverage:
  scope: string
  exhaustive: boolean
  assumptions: [string]
  certificate_ref: string | null
metrics:
  generated_count: integer
  examined_count: integer
  work_units: number
warnings: [string]
```

The `exhaustive` flag is meaningful only relative to the declared scope and assumptions. A generator returning zero candidates with `termination_reason: budget` MUST NOT be interpreted as proving no further candidates exist. Generator results MUST be idempotently ingestible: retrying a batch cannot create duplicate decisions.

### 6.1 Generation sources

A generator MAY derive proposals from unresolved structural gaps, prior accepted relations, constraint propagation, analogical transfer, residual patterns, weak-evidence cues, historical successful motifs, or competing agents. Each source MUST be represented in provenance; weak-evidence-derived proposals MUST be labeled as such.

### 6.2 Directional influence

Directional fields MAY affect candidate order, candidate family, expansion depth, resource budgets, and exploratory diversity. Directional fields MUST NOT redefine a domain's hard feasibility rules. The system SHOULD reserve some exploration capacity for candidates not favored by the current field to reduce premature convergence.

## 7. Constraint plugin interface

```text
EvaluateConstraint(
    snapshot: BucketSnapshot,
    candidate: CandidateEnvelope,
    rule_set: RuleSetRef,
    context: ContextView
) -> ConstraintResult
```

The result MUST contain:

```yaml
verdict: pass | fail | unknown | error
constraint_id: string
constraint_version: string
hardness: hard | soft | conditional
premise_refs: [string]
reason_code: string
explanation: string
proof_or_witness_ref: string | null
confidence_metadata: object | null
suggested_actions: [string]
```

**Hard failure** MAY justify rejection only if the constraint is applicable, its premises are supported, and the implementation's validation policy accepts the rule as authoritative. **Soft failure** MUST NOT independently justify irreversible pruning. **Conditional failure** MUST state the condition under which it becomes hard. **Unknown** MUST NOT be treated as failure. **Error** MUST be surfaced as an execution problem, not a candidate verdict.

### 7.1 Three-valued feasibility

Let \(F(B,c)\in\{\mathsf{valid},\mathsf{invalid},\mathsf{unknown}\}\) denote feasibility of adding candidate \(c\) to bucket \(B\). For hard constraints \(h_i\), define:

\[
F(B,c)=
\begin{cases}
\mathsf{invalid}, & \exists i:\ h_i(B\oplus c)=\mathsf{false}\text{ with valid premises},\\
\mathsf{valid}, & \forall i:\ h_i(B\oplus c)=\mathsf{true}\text{ and checks complete},\\
\mathsf{unknown}, & \text{otherwise}.
\end{cases}
\]

This definition does not claim that every relevant domain constraint is known. `valid` means valid under the declared, completed checks, not globally true in an unrestricted world model.

## 8. Constraint classes

| Class | Examples | Permitted effect |
|---|---|---|
| Structural hard | Type compatibility, cardinality bounds, exclusive ownership | Reject with valid witness |
| Temporal hard | Proven ordering incompatibility under declared clock assumptions | Reject if premises verified |
| Resource hard | Capacity or conservation invariant | Reject if invariant applies |
| Logical hard | Contradiction with accepted facts | Reject or trigger conflict resolution |
| Conditional | Constraint activated by a stated hypothesis or context | Defer or apply when condition holds |
| Soft | Plausibility, similarity, reputational evidence | Score, rank, probe; not hard prune |
| Policy | Access, privacy, legal or safety boundaries | Restrict allowed operations; separately auditable |

Policy prohibitions may block an action even when the structural hypothesis is feasible; the system SHOULD record this as **operation disallowed**, not **hypothesis disproven**.

## 9. Constraint composition semantics

Constraint plugins MUST declare whether they are independent, ordered, or jointly evaluated. Hard feasibility is the conjunction of applicable hard predicates, subject to premise validity:

\[
\operatorname{Feasible}(B\oplus c) = \bigwedge_{i\in H_{\mathrm{applicable}}} h_i(B\oplus c).
\]

A false predicate establishes infeasibility only when its scope and premise requirements hold. Missing checks yield `unknown`, not `pass`. Soft signals SHOULD be combined by a separate scoring contract with declared normalization, dependence handling, and uncertainty.

### 9.1 Conflict among plugins

If two plugins disagree about the same purported hard rule, the core MUST NOT silently choose the higher-scoring result. It MUST flag a rule conflict, preserve both provenance records, and apply an explicit governance resolution or suspend the affected transition. Plugin priority is not a substitute for logical consistency.

## 10. Propagation contract

```text
Propagate(
    snapshot: BucketSnapshot,
    accepted_delta: StructuralDelta,
    rule_set: RuleSetRef
) -> PropagationResult
```

A propagation result MAY include entailed assignments, forbidden candidate patterns, narrowed domains, and conflict witnesses. Each derived restriction MUST reference the rule and premises that entail it. The core MUST distinguish **entailed restrictions** from **heuristic suggestions**.

A propagator SHOULD support incremental evaluation, but caching MUST include all state and rule dependencies. If an upstream assumption is retracted, derived restrictions depending on it MUST be invalidated or re-evaluated.

### 10.1 Monotonicity and retraction

Within a fixed, monotonic hard-rule context, accepted facts may only narrow the feasible candidate domain. Across changing evidence, rules, or assumptions, that monotonicity cannot be presumed. Implementations MUST track dependencies to permit safe reopening of branches after retraction or rule revision.

## 11. Branching and transition integration

The core SHOULD distinguish at least four actions:

1. **Accept:** Commit a candidate delta after required feasibility checks.
2. **Reject:** Record a justified infeasibility finding or explicit branch exclusion.
3. **Defer:** Retain a candidate pending evidence, resources, or applicable rules.
4. **Probe:** Schedule a bounded information-gathering action without asserting acceptance.

Rejecting a candidate in one bucket does not imply global invalidity. The rejection scope MUST be recorded. If an accepted candidate later conflicts with a new hard fact, the system MUST initiate explicit revision or conflict resolution rather than silently rewriting history.

## 12. Deduplication and semantic identity

Candidate deduplication SHOULD use a canonical structural representation including operation, operands, role labels, preconditions, and relevant context. Bucket deduplication is stricter: two buckets may merge only if their future admissible transitions and objective-relevant semantics are equivalent under a documented criterion.

A shared candidate fingerprint across buckets does not imply the candidate has the same feasibility in both. Constraint results MUST be cached against the relevant bucket and rule dependencies.

## 13. Search closure and completeness

A bucket is **generator-quiescent** when all invoked generators report no immediately available candidates; this does not establish global closure. A bucket is **closed relative to a declared scope** only when coverage claims, rule checks, and pending transitions satisfy an explicit closure criterion. A bucket terminated by budget MUST be labeled partial.

Conditional completeness can be discussed only if:

- the candidate domain is finitely enumerable or has a fair exhaustive enumeration;
- generators meet their stated coverage assumptions;
- no sound branch is permanently suppressed by heuristics;
- hard pruning is sound;
- resource limits permit the required exploration.

D-BTP does not thereby become a polynomial-time general solver. Worst-case combinatorial growth remains possible.

## 14. Directional and evidence plugin separation

The following interfaces are deliberately distinct:

```text
ScoreCandidate(snapshot, candidate, evidence_view, field) -> ScoreVector
RecommendProbe(snapshot, candidate, uncertainty) -> ProbeProposal
EvaluateConstraint(snapshot, candidate, hard_rules) -> ConstraintResult
```

A `ScoreVector` MAY include plausibility, novelty, information gain, expected cost, risk, and directional alignment. Scores MUST carry their scale, provenance, and uncertainty representation. Evidence from correlated sources SHOULD not be counted as independent confirmations. A scoring plugin MUST NOT return a hard rejection through an undocumented side channel.

## 15. Plugin registry and capability manifest

Each plugin MUST publish a manifest:

```yaml
plugin_id: string
version: semver
kind: generator | constraint | propagator | evidence | scoring | probe
schema_version: string
supported_candidate_types: [string]
required_context: [string]
read_capabilities: [string]
side_effects: none | declared
rule_dependencies: [string]
determinism: deterministic | seeded | nondeterministic
resource_limits: object
security_classification: string
conformance_profile: string
```

Plugins SHOULD use least-privilege context views. Untrusted plugin outputs MUST be validated as data. The core SHOULD sandbox plugin execution, impose quotas, and record failures. Remote or nondeterministic plugins MUST declare reproducibility limits.

## 16. Orchestration reference algorithm

```python
def expand_bucket(bucket, registry, policy, budget):
    snapshot = freeze(bucket)
    batches = registry.generators.generate(snapshot, policy, budget)
    candidates = normalize_and_deduplicate(batches)

    for candidate in candidates:
        if budget.exhausted():
            record_partial_termination(snapshot)
            break

        checks = registry.constraints.evaluate(snapshot, candidate)
        if checks.has_execution_error():
            record_plugin_error(candidate, checks)
            continue
        if checks.has_supported_hard_failure():
            record_rejection(candidate, checks.witnesses())
            continue
        if checks.has_unknown_required_check():
            schedule_defer_or_probe(candidate, checks)
            continue

        proposal = registry.propagators.derive(snapshot, candidate)
        if not validate_propagation(proposal):
            quarantine_plugin_result(proposal)
            continue

        score = registry.scorers.score(snapshot, candidate, policy)
        schedule_branch(candidate, proposal, score)

    commit_audited_transitions_with_version_checks()
    classify_lifecycle_from_coverage_and_pending_work()
```

This pseudocode omits concurrency, transactional persistence, and application-specific policies. In particular, `has_supported_hard_failure()` requires verification of applicability and premises, not merely the presence of a `fail` string.

## 17. Multi-agent and relay interoperability

Agents MAY independently propose candidates or evaluate constraints. Every shared artifact MUST carry a stable schema version, source references, rule versions, and a receiving-context compatibility check. A receiving agent MUST NOT import another agent's `pass` verdict as authoritative without checking the rule scope and premises. Competitive proposals SHOULD preserve alternative explanations and counterevidence rather than collapsing immediately to a single winner.

The relay unit SHOULD contain the candidate envelope, evaluation records, dependency graph, directional metadata, and explicit unresolved questions. Shared weak evidence remains weak evidence after relay.

## 18. Domain case: blockchain actor attribution

Consider an illustrative starmap of observed on-chain behaviors and a hypothesis space of latent behavioral actors. A generator proposes that one actor explains several behaviors; another proposes a split into distinct actors. A cardinality plugin allows one-to-many actor-to-behavior mappings. Temporal and transaction-consistency plugins test explicit constraints. Behavioral similarities or network metadata may guide which hypotheses to inspect but do not by themselves establish a real-world person's identity.

A synthetic example:

```text
Candidate A: actor X -> {behavior b1, behavior b2}
Candidate B: actor X -> {behavior b1}; actor Y -> {behavior b2}
Evidence: timing similarity favors A weakly
Hard constraint: a validated domain rule conflicts with A
Result: reject A under that rule; retain B for further checks
```

The example illustrates constraint precedence, not a general rule that timing similarity is reliable. Real-world applications MUST account for privacy, data minimization, uncertain attribution, and applicable legal safeguards.

## 19. Conformance profiles

**Core profile:** immutable snapshot invocation, typed candidates, explicit three-valued feasibility, hard/soft separation, versioned audit records, safe branching.

**Propagation profile:** premise-tracked implications, incremental invalidation, sound restriction certificates or equivalent checks.

**Directional profile:** scoring/generation coupling with non-authoritative heuristic signals, exploration diversity, budget reporting.

**Relay profile:** interoperable provenance, receiving-context validation, versioned artifacts, reproducibility metadata.

An implementation MUST name the profile(s) it claims and disclose unsupported optional capabilities.

## 20. Conformance test catalog

| ID | Test | Expected behavior |
|---|---|---|
| CG-01 | Same logical candidate generated twice | Idempotent ingestion |
| CG-02 | Same operands with different preconditions | Distinct semantic candidates |
| CG-03 | One-to-many relation | Accepted if domain rules allow |
| CG-04 | Missing required hard check | `unknown`, not `pass` |
| CG-05 | Verified hard contradiction | Reject with rule and premise witness |
| CG-06 | Soft score strongly negative | No automatic hard prune |
| CG-07 | Conditional rule not activated | No unconditional rejection |
| CG-08 | Constraint plugin execution error | Error record, not infeasibility |
| CG-09 | Stale bucket version | Recompute or verified safe reuse |
| CG-10 | Budget ends generation | Partial status, not closed |
| CG-11 | Generator reports empty batch without coverage | Quiescence only |
| CG-12 | Two hard plugins disagree | Conflict surfaced and audited |
| CG-13 | Propagation premise retracted | Dependent restrictions invalidated |
| CG-14 | Plugin returns unsupported mutation | Rejected by core |
| CG-15 | Evidence source duplicated | Dependence flagged or corrected |
| CG-16 | Directional field changes priority | Feasibility rules unchanged |
| CG-17 | Composite all-or-nothing delta partly invalid | No partial commit |
| CG-18 | Relay artifact with incompatible rule version | Re-evaluation required |
| CG-19 | Rejected candidate in another bucket | No unwarranted global rejection |
| CG-20 | Privacy policy denies a probe | Operation blocked, hypothesis not disproven |
| CG-21 | Same candidate under distinct hard-rule contexts | Context-sensitive cache behavior |
| CG-22 | Nondeterministic generator | Reproducibility limits recorded |
| CG-23 | Untrusted plugin emits malformed schema | Quarantined and logged |
| CG-24 | Claimed exhaustive generator with unmet assumptions | Closure claim denied |

Passing these tests is a proposed conformance criterion; no execution results are asserted here.

## 21. Validation roadmap

**Phase 1 — Contract fixtures.** Build schema validators, deterministic synthetic buckets, rule fixtures, and negative tests for unknown/error handling.

**Phase 2 — Constraint correctness.** Compare plugin outcomes with a small exhaustive reference solver on bounded synthetic problems. Measure false hard rejections separately from false acceptance.

**Phase 3 — Dynamic generation.** Compare fixed-list generation, dynamic unguided generation, and dynamic directional generation under equal budgets. Track candidate coverage and discovered feasible hypotheses.

**Phase 4 — Propagation and scaling.** Evaluate pruning benefit, invalidation correctness, cache hit rates, time-to-feasible-solution, and diversity under increasing structural complexity.

**Phase 5 — Multi-agent relay.** Test version compatibility, provenance retention, contradiction handling, and reproducible transfer across independent agents.

Pre-register benchmark rules and scoring metrics where practical. Report timeouts and unknown outcomes explicitly.

## 22. Testable hypotheses

- **H1:** State-dependent candidate generation discovers valid compositions missed by a fixed initial candidate list under matched budgets.
- **H2:** Sound propagation reduces explored branches without reducing the feasible solution set on bounded reference tasks.
- **H3:** Separating hard constraints from weak evidence reduces erroneous pruning relative to a mixed-threshold baseline.
- **H4:** Versioned provenance improves reproducibility and diagnosis of conflicting plugin verdicts.
- **H5:** Directional guidance improves median time to a high-quality feasible hypothesis on some task families, but not uniformly across all distributions.
- **H6:** Explicit diversity allocation reduces premature convergence in ambiguous multi-hypothesis tasks.
- **H7:** Relay with dependency-aware validation transfers useful candidate structures while limiting propagation of stale verdicts.

Each hypothesis is empirical and may be falsified. Improvements must be evaluated against computation cost and benchmark selection effects.

## 23. Failure modes and mitigations

**Unsound pruning:** A heuristic or invalid premise is treated as hard. Mitigate with typed verdicts, premise validation, and reference tests.

**Candidate starvation:** Directional policy never explores disfavored branches. Mitigate with fairness or exploration quotas and budget transparency.

**False closure:** A quiet generator is treated as exhaustive. Mitigate with coverage certificates and explicit partial lifecycle states.

**Rule drift:** Plugins change meaning across versions. Mitigate with immutable rule references, compatibility checks, and replay.

**Evidence laundering:** Repeated relay makes a weak claim appear independently confirmed. Mitigate with source lineage and dependence-aware scoring.

**Unsafe caching:** State-sensitive verdicts are reused across incompatible buckets. Mitigate with dependency-complete cache keys.

**Plugin capture:** A malicious or buggy plugin manipulates state or consumes excessive resources. Mitigate with sandboxing, least privilege, schema checks, and quotas.

**Identity overreach:** Structural behavioral clustering is presented as personal identification. Mitigate with explicit epistemic boundaries and independent corroboration requirements.

## 24. Open questions

1. Which useful generator families admit checkable completeness certificates?
2. How can incremental constraint propagation remain efficient under frequent hypothesis retraction?
3. When should a candidate be composite rather than a sequence of atomic proposals?
4. What equivalence relation permits safe merging of bucket states across distinct provenance histories?
5. How should uncertainty about the rule set itself affect search closure?
6. Can learned generators provide calibrated coverage estimates without claiming exhaustive enumeration?
7. How should competing agents reconcile hard-rule conflicts without centralizing every decision?
8. What minimal provenance is sufficient for trustworthy relay across heterogeneous runtimes?

## 25. Relationship to the D-BTP research series

- **D-BTP-001:** Transition from metric similarity to structural hypothesis search.
- **D-BTP-002:** Dynamic bucket states and state-dependent candidate generation.
- **D-BTP-003:** Constraint-guided structural composition and sound pruning.
- **D-BTP-004:** Directional fields for generation and selection.
- **D-BTP-005:** Weak evidence as a search resource rather than proof.
- **D-BTP-006:** Coupled generation, selection, and feedback.
- **D-BTP-007:** Multi-agent RSI and collective structural learning.
- **D-BTP-008:** Open-ended structural evolution and its boundaries.
- **SPEC-001:** Canonical bucket state, transitions, provenance, and lifecycle.
- **SPEC-003 (planned):** Directional scoring and search control.
- **SPEC-004 (planned):** Evidence relay and learning lifecycle.

## 26. Conclusion

The proposed D-BTP plugin boundary makes dynamic structural search extensible without sacrificing the distinction between feasibility, uncertainty, and directional preference. Generators create hypotheses; hard constraints test admissibility; propagators derive justified consequences; evidence and directional plugins determine what deserves further attention; the core records and governs transitions. The decisive engineering requirement is not merely modularity, but **traceable, versioned, and sound interaction among modules**. This contract provides a basis for conformance testing before runtime optimization or autonomous improvement claims.

---

*Research note:* This specification describes a proposed architecture and validation program. Its contracts, performance hypotheses, and completeness conditions require implementation-specific testing and should not be interpreted as established empirical results.
