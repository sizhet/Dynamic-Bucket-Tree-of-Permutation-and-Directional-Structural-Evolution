# Future Directions — Dynamic Bucket Tree of Permutation (D-BTP)

**Project:** Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document type:** Research roadmap and open-ended development agenda  
**Status:** Prospective research directions; not claims of demonstrated performance  
**Version:** 1.0.0 (research roadmap)

## 1. Purpose and research stance

D-BTP generalizes the Bucket Tree of Permutation (BTP) from constrained structural matching toward dynamic, constraint-guided hypothesis composition. Its central proposal is a **coupled system**: the current structural state generates candidate extensions; constraints determine which extensions are admissible; directional fields guide what to generate, inspect, and prioritize; evidence and feedback update both hypotheses and guidance. The resulting search may be conducted by one solver or by a collective of cooperating and competing agents.

This document identifies research directions beyond the initial foundations, specifications, and illustrative cases. Each direction separates (a) the hypothesis, (b) a plausible technical path, (c) measurable evidence, and (d) failure conditions. The agenda is intentionally falsifiable. No universal efficiency gain, automatic discovery of truth, general intelligence, or recursive self-improvement is assumed.

### A working distinction

- **State growth:** additional accepted/rejected structural hypotheses within a fixed representation.
- **Policy adaptation:** changes to candidate ordering, scoring, budgets, or other search controls.
- **Representational growth:** creation of new relation types, abstractions, or hypothesis languages.
- **Operator growth:** creation or revision of candidate generators, propagators, or other reusable procedures.
- **Validated recursive improvement:** improvements to the improvement process itself, established by independent evaluation rather than inferred from self-modification.

The first two can be useful without establishing the latter three.

## 2. Research axis A — Dynamic structural search semantics

### A1. Candidate-generation completeness and closure

**Question.** When can a dynamically generated frontier be considered complete relative to a specified hypothesis language and generator family?

A finite candidate queue is not proof that no more candidates exist. A bucket may be **quiescent** because no enabled generator currently emits a candidate, **closed** only under a justified closure condition, or **budget-terminated** while work remains possible. Future work should define closure certificates for particular generator classes, explicit fairness assumptions, and monotonic versus non-monotonic candidate availability.

**Approach.** Formalize the generator as $G(B_t,\Theta_t,R_t)$, with state $B_t$, policy $\Theta_t$, and resources $R_t$. Specify a hypothesis language $\mathcal H$, a reachability relation, and a closure predicate $C(B_t,G,\mathcal H)$. Study conditions under which the search enumerates every reachable feasible hypothesis before termination.

**Evidence.** Small instances with exhaustive ground truth; machine-checked transition invariants; adversarial cases where late evidence activates previously unavailable candidates.

**Failure condition.** A claimed closure certificate excludes a feasible candidate reachable under the stated assumptions.

### A2. Safe state equivalence and merging

Naive deduplication by accepted hypothesis IDs may merge buckets with different rejected hypotheses, evidence provenance, generator versions, or future candidate sets. Develop **behavioral equivalence** criteria under which two bucket states can safely share search work. Distinguish exact canonicalization from approximate similarity caching, which must not support correctness claims without an error bound.

### A3. Cardinality-aware structural composition

Original starmap matching often assumes one-to-one or injective correspondences. Applications may instead require one-to-many, many-to-one, optional, or hierarchical mappings. Extend plugin contracts to express cardinality and identity constraints explicitly, with clear handling of latent actors and shared infrastructure.

## 3. Research axis B — Constraint intelligence and sound pruning

### B1. Composable constraint plugins

Develop an interoperable constraint language with explicit types, preconditions, dependencies, scope, and evidence requirements. A plugin response should distinguish `PASS`, `FAIL`, `UNKNOWN`, and `ERROR`; a hard `FAIL` should be accompanied by a checkable explanation or certificate when feasible.

**Research test.** Compare independently composed plugins with monolithic validators for correctness, coverage, and runtime overhead. Inject contradictory plugins, stale versions, and missing dependencies.

### B2. Incremental propagation and conflict learning

Explore incremental constraint propagation, learned conflict clauses, no-good records, and domain reduction. Preserve the distinction between a **logical contradiction** and a **low-priority branch**. A low directional score is never sufficient for sound pruning.

### B3. Conditional and defeasible constraints

Some conditions depend on assumptions that may later be revised. Introduce assumption-scoped constraints and dependency tracking, so invalidated assumptions trigger targeted re-evaluation rather than silent inconsistency.

## 4. Research axis C — Directional fields as coupled search controls

### C1. From ranking to generative guidance

A key D-BTP hypothesis is that directional fields should influence not merely the ordering of already generated candidates but **which candidates are proposed**. A controlled comparison should isolate four systems:

| Variant | Dynamic generation | Directional generation | Directional selection | Feedback adaptation |
|---|---|---|---|---|
| V0 | No | No | Optional static ranking | No |
| V1 | Yes | No | No | No |
| V2 | Yes | No | Yes | No |
| V3 | Yes | Yes | Yes | No |
| V4 | Yes | Yes | Yes | Yes |

Compare solution quality at fixed computation budgets, coverage of diverse feasible explanations, and time to first independently validated result. Directional generation should be considered beneficial only when its incremental value exceeds model and orchestration costs.

### C2. Multi-perspective fields and Pareto portfolios

Replace a single scalar priority with a directional vector, for example

$$
\mathbf d(h) = [d_{\mathrm{fit}},d_{\mathrm{novelty}},d_{\mathrm{information}},d_{\mathrm{cost}},d_{\mathrm{risk}}].
$$

Weights may depend on task and governance policy. Preserve non-dominated hypotheses and controlled exploration quotas to avoid prematurely eliminating unusual but potentially correct explanations. Study how uncertainty intervals and missing evidence affect Pareto comparisons.

### C3. Field drift, calibration, and feedback loops

Directional models may become overconfident when they train on evidence produced by their own search policy. Develop held-out evaluation, randomized exploration, delayed feedback, drift alarms, and rollback triggers. Separate observational correlation from demonstrated causal search benefit.

### C4. Recursive directional field evolution

Treat a directional field unit (DFU) as a versioned, testable hypothesis about how search should be conducted. Candidate DFUs can be generated, compared, and retired. A change qualifies as **validated improvement** only after out-of-sample tests with controlled budgets and credible uncertainty estimates. Recursive modification alone is not RSI.

## 5. Research axis D — Weak evidence and counterevidence

### D1. Measuring search utility separately from truth

Weak evidence may improve prioritization even if it does not establish that a hypothesis is correct. Define separate quantities for evidential support and search utility:

$$
U_{\mathrm{search}}(e) = \mathbb E[Q(\pi_e;B)] - \mathbb E[Q(\pi_0;B)] - \lambda\,\Delta C(e),
$$

where $Q$ is a predeclared quality measure at budget $B$, $\pi_e$ is an evidence-guided policy, $\pi_0$ a baseline, and $\Delta C$ the added cost. This is an experimental estimand, not an established law.

### D2. Provenance and correlated evidence

Multiple signals can originate from one underlying event or source. Without dependency accounting, an algorithm may count one observation many times. Future work should use evidence-dependency graphs, provenance labels, confidence calibration, and sensitivity analyses for correlated features.

### D3. Active evidence acquisition

Allow a search agent to choose what to observe next. Compare expected information gain, hypothesis-discrimination gain, and acquisition cost. Explicitly test whether counterevidence-seeking agents reduce confirmation bias relative to purely supportive evidence collection.

### D4. Relational Evidence Navigation (REN)

Explore whether relation- and direction-aware weak evidence can guide the search of structurally analogous hypotheses without reducing all guidance to Euclidean similarity. This is a candidate research connection to BM-ODWEI and REN, not a proven universal scoring method.

## 6. Research axis E — Multi-agent competition and collective structural learning

### E1. Diverse hypothesis portfolios

Assign agents complementary roles: generators, constraint auditors, evidence critics, counterexample finders, and resource allocators. Measure **marginal diversity**, not raw agent count. Multiple agents producing near-identical hypotheses may increase cost without adding information.

### E2. Relay contracts and trust boundaries

A Structural Hypothesis Unit (SHU) should include its claim, assumptions, supporting and opposing evidence, constraints, provenance, versions, and unresolved questions. Relay receipts should distinguish successful transport from successful validation. Receiving agents must independently check compatibility with their task and policy.

### E3. Cross-task transfer

Test whether learned generators, field policies, and constraint patterns transfer between synthetic starmap matching, scheduling, strategy search, and other domains. Use held-out task families and negative-transfer tests; improvements on the training family do not demonstrate general transfer.

### E4. Collective learning versus RSI

An archive of successful strategies is collective memory. Reusing it can improve future performance, but is not necessarily recursive self-improvement. A stronger claim requires evidence that the system improves its ability to produce and validate *new improvements*, across repeated rounds and independent tasks.

## 7. Research axis F — Open-ended structural evolution

### F1. Four frontiers

Study the interaction of four explicit frontiers:

1. **Hypothesis frontier:** candidate explanations in the current representation.
2. **Representation frontier:** new concepts, relation types, and abstractions.
3. **Operator frontier:** new generators, validators, and transformation rules.
4. **Relay frontier:** new reusable units and cross-agent interfaces.

A system may expand one frontier while remaining bounded in the others. Record each expansion as a versioned proposal with a conformance and evaluation plan.

### F2. Residual-driven invention

Use persistent mismatches between model and observations as triggers for structural invention. Distinguish residuals caused by inadequate representation from those caused by noise, incomplete evidence, or incorrect assumptions. Require proposed new operators to outperform simpler repairs on held-out examples.

### F3. Growth governance

Open-ended proposals can consume unbounded compute or introduce unsafe behavior. Set resource ceilings, sandbox execution, review gates, rollback, and explicit leftover records for deferred work. A failed or repeated execution may still create useful evidence for future relay, but does not automatically count as an improvement.

## 8. Research axis G — Benchmark suite and evaluation methodology

### G1. Benchmark families

| Family | Main capability tested | Ground truth strategy |
|---|---|---|
| Synthetic graph/starmap alignment | Matching and cardinality constraints | Constructed exact mappings |
| Dynamic candidate activation | Late-emerging relations and closure | Generator-defined reachable set |
| Constraint-heavy composition | Sound pruning and propagation | Exhaustive small-case solver |
| Weak-evidence search | Guidance under noisy/correlated signals | Seeded signal/noise process |
| Multi-agent competition | Diversity, contradiction discovery, cost | Multiple planted explanations |
| Cross-domain transfer | Reuse of generators and fields | Held-out task families |
| Recursive field improvement | Sustained out-of-sample gains | Frozen evaluation protocol |

### G2. Required baselines

At minimum: exhaustive search on small problems; static BTP where applicable; dynamic BTP without guidance; dynamic BTP with fixed directional selection; dynamic BTP with coupled directional generation and selection; and the same with feedback adaptation. Add domain-standard solvers where relevant rather than benchmarking only against weak in-house baselines.

### G3. Metrics

Report feasible-solution recall, top-k explanation quality, false-pruning rate, counterexample discovery rate, search coverage, calibration, diversity, wall-clock time, CPU/GPU cost, memory, communication overhead, reproducibility, and negative-transfer frequency. Distinguish **anytime quality** from final quality, and report performance against matched resource budgets.

### G4. Experimental discipline

Predeclare tasks and success criteria, separate development and test splits, use multiple seeds, report uncertainty, preserve failed runs, and release synthetic datasets and conformance traces when possible. Avoid presenting illustrative examples as empirical validation.

## 9. Research axis H — Application frontiers

### H1. Dynamic starmap similarity

Revisit the original BTP setting to identify when dynamic candidate discovery helps and when a static candidate matrix is simpler or faster. Explore typed, hierarchical, and partially observed structures.

### H2. Blockchain behavioral attribution

Treat observed transactions and latent behavioral actors as competing structural hypotheses. Address clustering ambiguity, shared services, adversarial behavior, and incomplete observations. Distinguish **behavioral association** from **real-world identity**. Do not treat weak structural similarity, public-key reuse assumptions, or network metadata as proof of a person's identity. Evaluate with synthetic or appropriately authorized datasets and privacy-preserving reporting.

### H3. Scheduling and combinatorial optimization

Use school transportation or other constrained scheduling as controlled environments with explicit objectives and ground truth checks. Compare D-BTP with integer programming, constraint programming, local search, and established heuristics. Optimize multiple objectives such as fleet size, travel burden, and fairness, not a single unconstrained score.

### H4. Strategic multi-agent laboratories

Investigate connections to SSICR and Chess-SSIL: competitive structural hypotheses, strategic counterexamples, and relayable search policies. Distinguish generating a strategy from proving that it is robust against adaptive opponents.

### H5. Autonomous question generation

Connect D-BTP to AQSI: a question can be treated as a structured proposal to reduce uncertainty or expose residuals. Test whether question-selection policies improve downstream hypothesis discovery rather than merely generating more questions.

## 10. Reference architecture for a research MVP

A minimal implementation should separate correctness-critical operations from heuristic controls:

```text
Task + Hypothesis Language + Governance Policy
                    |
                    v
        Dynamic Bucket State Registry
                    |
          +---------+----------+
          |                    |
          v                    v
  Candidate Generators   Directional Field Units
          |                    |
          +---------+----------+
                    v
         Constraint Plugin Layer
                    |
           PASS / FAIL / UNKNOWN
                    |
                    v
       Hypothesis Frontier + Portfolio
                    |
                    v
          Evidence / Counterevidence
                    |
                    v
        Feedback and Evaluation Gate
                    |
             +------+------+
             |             |
             v             v
       Bucket Update   Policy Proposal
                           |
                           v
                  Sandbox + Validation
                           |
                           v
                    Versioned Relay
```

The diagram describes a proposed architecture. It is not a claim that the system has been implemented or benchmarked.

### Minimum interoperable artifacts

- Versioned Dynamic Bucket State and event log.
- Candidate generator declaration with explicit preconditions and scope.
- Constraint plugin declaration with typed results and failure evidence.
- Directional field unit with calibration and update history.
- SHU/relay envelope with provenance and receiving-side validation.
- Reproducible experiment manifest with budgets, seeds, baselines, and outcomes.

## 11. Milestone roadmap

| Stage | Deliverable | Exit criterion |
|---|---|---|
| M0 — Contract stabilization | Harmonized SPEC-001–004 and examples | No unresolved schema contradictions in conformance fixtures |
| M1 — Correctness kernel | Dynamic buckets, generator interface, hard-constraint plugins | Exhaustive small-case agreement; no observed unsound pruning |
| M2 — Directional search | Fixed and adaptive guidance under equal budgets | Reproducible ablation results, including negative cases |
| M3 — Evidence intelligence | Provenance, dependence, counterevidence acquisition | Improved calibration or discrimination on held-out tasks |
| M4 — Multi-agent relay | SHU exchange, portfolio management, conflict handling | Independent receiving-side verification and measured overhead |
| M5 — Transfer and policy evolution | Versioned DFUs, sandboxed upgrades, cross-task tests | Statistically credible gains on frozen external evaluations |
| M6 — Open-ended research | Representation/operator proposal pipeline | Demonstrated useful new capability beyond parameter tuning |

Stages are research gates, not promised dates. Failure at any gate should trigger model revision or narrowing of claims.

## 12. Prioritized open questions

**Priority 1 — correctness and meaning**

1. What precisely distinguishes quiescence from provable closure for a dynamic generator?
2. Under which state-equivalence conditions can bucket deduplication preserve all feasible futures?
3. How should conditional constraints be revised when their supporting assumptions fail?
4. What constitutes a checkable certificate for a hard rejection?

**Priority 2 — search utility**

5. When does directional candidate generation outperform directional ranking alone?
6. How can one estimate the marginal value of weak evidence without leaking test labels?
7. Which diversity mechanisms best prevent premature convergence at fixed budgets?
8. How much does counterevidence acquisition improve error detection relative to its cost?

**Priority 3 — collective learning and evolution**

9. What is the smallest portable SHU/DFU/SERU contract that remains semantically useful?
10. Which task features predict positive versus negative cross-domain transfer?
11. What evidence would distinguish one-off self-modification from sustained validated RSI?
12. How can representation and operator growth remain interpretable, auditable, and bounded?

## 13. Falsification and stop conditions

The research program should explicitly accept outcomes that limit D-BTP's scope:

- Static methods dominate dynamic generation when candidate sets are already complete and cheap to enumerate.
- Directional fields overfit or amplify spurious evidence, producing worse solutions than unguided exploration.
- Multi-agent communication and coordination cost exceeds any diversity benefit.
- Learned operators improve familiar benchmarks but degrade held-out tasks.
- Closure or deduplication heuristics silently eliminate feasible solutions.
- Claimed RSI gains disappear under independent evaluation or matched compute budgets.

These are not peripheral caveats: they are central experiments that define where D-BTP is useful.

## 14. Governance, privacy, and research integrity

Maintain a strict boundary between hypothesis exploration and factual attribution. Log evidence origin, model versions, permissions, and unresolved uncertainty. Avoid unauthorized collection or exposure of personal data. In high-stakes domains, route consequential decisions through independent review and domain-appropriate validation. Preserve alternative explanations and make uncertainty visible to downstream users.

Use conservative publication language: *proposed*, *illustrated*, *hypothesized*, and *to be validated* when appropriate. Only use *demonstrated* or *outperformed* with reproducible experimental support.

## 15. Connections to the D-BTP document set

### Foundations

- [D-BTP-001 — From Metric Similarity to Structural Hypothesis Search](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md)
- [D-BTP-002 — Dynamic Bucket States and Candidate Generation](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md)
- [D-BTP-003 — Constraint-Guided Structural Composition](docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md)
- [D-BTP-004 — Directional Fields for Generation and Selection](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md)
- [D-BTP-005 — Weak Evidence and Directional Exploration](docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md)
- [D-BTP-006 — Coupled Generation, Selection and Feedback](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md)
- [D-BTP-007 — Multi-Agent RSI and Collective Structural Learning](docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md)
- [D-BTP-008 — Open-Ended Structural Evolution and Intelligence](docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md)

### Specifications

- [SPEC-001 — Dynamic Bucket State Contract](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md)
- [SPEC-002 — Candidate Generation and Constraint Plugins](docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md)
- [SPEC-003 — Directional Scoring and Search Control](docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md)
- [SPEC-004 — Evidence Relay and Learning Lifecycle](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md)

### Cases and extensions

- [CASE-001 — Blockchain Actor Attribution](docs/cases/CASE-001-Blockchain-Actor-Attribution.md)
- [CASE-002 — Dynamic Starmap Similarity](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md)
- [CASE-003 — Multi-Agent Hypothesis Competition](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md)
- [EXT-001 — Biomimetic Directional Intelligence](docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md)
- [EXT-002 — Recursive Directional Field Evolution](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md)
- [EXT-003 — Open-Ended BTP and Structural Relay](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md)

### Companion navigation and validation documents

- [README](README.md) · [START-HERE](START-HERE.md) · [CONTENTS](CONTENTS.md) · [GLOSSARY](GLOSSARY.md) · [FIGURE-INDEX](FIGURE-INDEX.md)
- [OPEN-QUESTIONS](OPEN-QUESTIONS.md) · [TESTABLE-HYPOTHESES](TESTABLE-HYPOTHESES.md) · [VALIDATION-ROADMAP](VALIDATION-ROADMAP.md)

## 16. Closing perspective

D-BTP's most consequential research opportunity may lie in the **reciprocal coupling** of structural generation and purposeful search. Structural hypotheses shape what can be explored; directional fields shape what is generated and examined; constraints protect feasibility; evidence can challenge both hypotheses and guidance; and relay may allow validated discoveries to accumulate across agents and tasks.

Whether this becomes a broadly useful algorithmic family, a collection of domain-specific heuristics, or a narrower theory of dynamic structural matching is an empirical question. The next phase should prioritize conformance, strong baselines, negative results, and portable experimental artifacts before broader intelligence claims.

---

*Research note: This document is a prospective roadmap. Mathematical expressions, architectural sketches, and proposed benchmarks describe research hypotheses and design choices; they are not reports of completed experiments.*
