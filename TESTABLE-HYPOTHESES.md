# Testable Hypotheses — Dynamic Bucket Tree of Permutation (D-BTP)

**Project:** Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document type:** Research hypothesis registry and experimental protocol  
**Status:** Proposed, unvalidated research hypotheses; not empirical findings  
**Version:** 1.0.0 research draft  
**Companion documents:** [OPEN-QUESTIONS.md](OPEN-QUESTIONS.md), [FUTURE-DIRECTIONS.md](FUTURE-DIRECTIONS.md), [VALIDATION-ROADMAP.md](VALIDATION-ROADMAP.md)

> **Epistemic statement.** Every hypothesis below is a falsifiable research proposition. No measured performance advantage, completeness guarantee, attribution accuracy, autonomous intelligence, or RSI achievement is claimed by this document. Negative results and clearly bounded applicability are first-class outputs.

## 1. Objective and scientific discipline

D-BTP treats structural inference as a dynamic search in which a Bucket maintains an auditable hypothesis ledger, structural state, constraints, evidence, and directional control. Candidate generation, selection, constraint propagation, and feedback may influence one another. The purpose of this registry is to separate **design claims**, **correctness obligations**, **empirical performance claims**, and **long-horizon evolution claims**.

A testable hypothesis must specify: an intervention, an independent comparison, a measurable outcome, a failure criterion, and the circumstances under which it may generalize. Hard-constraint soundness is not an average-case performance metric: any confirmed unsound rejection is a correctness defect, even if aggregate search speed improves.

### 1.1 Formal experimental objects

Let a task instance be `x`, a search budget be `B`, a random seed be `s`, and a configuration be `a`. The result `R(a,x,B,s)` includes: the best feasible structural hypothesis (if any), a diverse portfolio, constraint and evidence audit trails, computational cost, and termination reason. Where a trusted reference exists, let `Q(R,x)` denote task quality, with larger values better. Define `C(R)` as total measured cost (compute, calls, communication and evidence acquisition as appropriate), and `T_q` as the cost required to reach a prespecified quality threshold `q`.

The primary treatment contrast is paired over the **same instances, seeds or matched seed blocks, budgets, hardware, and plugin contracts**. Report effect sizes and uncertainty intervals, not just a favorable best run. For randomized methods, predeclare the minimum practically important improvement, confidence or credible interval method, and multiplicity policy for primary endpoints.

### 1.2 Baseline ladder

| ID | Configuration | Distinguishing feature |
|---|---|---|
| B0 | Exhaustive or exact solver where tractable | Reference optimum or feasibility oracle |
| B1 | Static BTP / fixed candidate inventory | Original fixed-inventory search behavior |
| B2 | Dynamic BTP without directional guidance | State-dependent generation with neutral selection |
| B3 | Dynamic BTP with selection-only scoring | Generate independently, then rank |
| B4 | Dynamic BTP with fixed coupled directional field | Field influences generation and selection |
| B5 | Dynamic BTP with feedback-adaptive field | Field updates from eligible feedback |
| B6 | Multi-agent D-BTP with relay | Multiple agents and controlled exchange |
| B7 | Multi-agent D-BTP with validated policy promotion | Proposed policy revisions evaluated out of sample |

Not every baseline is appropriate for every task. A baseline that receives less information, a smaller budget, or a weaker constraint oracle is not a fair comparison. Where exact solvers are infeasible, explicitly label the reference as approximate or incomplete.

## 2. Registration format and decision rules

Each record specifies a *primary endpoint* and an anticipated direction. A hypothesis is **supported on the tested distribution** only if its preregistered endpoint passes the stated statistical and practical criteria, with no disqualifying correctness failure. It is **not supported** if the interval excludes the minimum meaningful gain, and **inconclusive** if data are insufficient. A null result is not proof of universal equivalence.

Use distinct training, tuning, validation, and held-out test instances. Keep feedback updates blind to held-out labels. For streaming experiments, use chronological splits and avoid look-ahead leakage. Report failure cases, especially when adaptive guidance suppresses rare but valid hypotheses.

## 3. Dynamic search and structural representation


### H-DYN-001 — State-dependent candidate discovery

**Hypothesis.** On instances with hidden but inferable structural relations, B2 discovers more reference-valid candidate relations than B1 at equal budget.

- **Intervention / comparator:** B2 vs B1; inject relations revealed only after an accepted or rejected hypothesis.
- **Primary endpoint:** Recall of valid relations discovered before budget expiration; feasible-solution recall.
- **Evidence against / failure condition:** No positive paired recall difference, or gains vanish after equalizing generator information.
- **Traceability:** OQ-DYN-001; D-BTP-002; CASE-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DYN-002 — Conditional advantage over static inventory

**Hypothesis.** Dynamic generation improves time-to-quality when a large static inventory contains many irrelevant pairs, but may lose on complete small inventories.

- **Intervention / comparator:** B1 vs B2 across controlled inventory completeness and branching-factor strata.
- **Primary endpoint:** Median T_q and area under quality-versus-cost curve by stratum.
- **Evidence against / failure condition:** No interaction with inventory completeness; B2 consistently slower with equal quality.
- **Traceability:** OQ-FND-001; CASE-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DYN-003 — Safe deduplication and equivalence

**Hypothesis.** A state-equivalence relation preserving future candidate availability and constraint outcomes reduces duplicate expansions without changing feasible results.

- **Intervention / comparator:** B2 with certified equivalence-based merging vs B2 without merging.
- **Primary endpoint:** Expanded states and exact feasible-solution set on small oracle tasks.
- **Evidence against / failure condition:** Any missing feasible solution or any counterexample to equivalence assumptions.
- **Traceability:** OQ-FND-003; SPEC-001.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DYN-004 — Quiescence is not closure

**Hypothesis.** Generator quiescence alone is insufficient to establish global closure when new evidence or policy revisions can expose candidates.

- **Intervention / comparator:** Inject delayed evidence after a quiescent state; compare naive closure vs version-aware reopening.
- **Primary endpoint:** Rate of incorrectly closed states; recovered valid candidates.
- **Evidence against / failure condition:** No observed counterexample in the specified generator class; narrow claim accordingly.
- **Traceability:** OQ-DYN-002; SPEC-001.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DYN-005 — Cardinality-aware representation

**Hypothesis.** Explicit one-to-many or many-to-many mapping contracts reduce invalid pruning compared with an unexamined one-to-one assumption.

- **Intervention / comparator:** Compare cardinality-correct plugin vs one-to-one default on synthetic latent-actor tasks.
- **Primary endpoint:** False infeasibility rate and recall of reference-consistent hypotheses.
- **Evidence against / failure condition:** No difference in cases with genuine non-injective mappings.
- **Traceability:** OQ-FND-002; CASE-001.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 4. Constraints and correctness

### H-CON-001 — Sound incremental propagation

**Hypothesis.** Sound incremental constraint propagation reduces explored infeasible states without removing valid solutions.

- **Intervention / comparator:** B2 with and without propagation; use exact oracle for small tasks.
- **Primary endpoint:** Infeasible states expanded; feasible-set equality; wall-clock cost.
- **Evidence against / failure condition:** Any lost feasible solution or no net cost benefit on target workloads.
- **Traceability:** OQ-CON-001; SPEC-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-CON-002 — Plugin composition and conflict

**Hypothesis.** Independent constraint plugins with explicit scope and version contracts produce fewer silent contradictions than untyped plugin integration.

- **Intervention / comparator:** Contracted plugin composition vs permissive composition under injected conflicts.
- **Primary endpoint:** Undetected conflicts, incorrect pruning, diagnostic latency.
- **Evidence against / failure condition:** No reduction in undetected conflicts or unacceptable overhead.
- **Traceability:** OQ-CON-002; SPEC-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-CON-003 — Unknown is not Fail

**Hypothesis.** Representing Unknown and Error distinctly from Fail prevents unsound pruning under missing or delayed evidence.

- **Intervention / comparator:** Four-valued plugin outcome vs binary pass/fail coercion under missingness.
- **Primary endpoint:** False rejection rate, audit completeness, runtime.
- **Evidence against / failure condition:** No false rejection reduction under deliberately ambiguous inputs.
- **Traceability:** OQ-CON-003; SPEC-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-CON-004 — Constraint-guided generation

**Hypothesis.** Using validated constraint propagation to generate only admissible candidate families reduces wasted expansions versus generate-all-then-filter.

- **Intervention / comparator:** Constraint-aware generator vs post-hoc filtering with identical hard constraints.
- **Primary endpoint:** Rejected candidates per feasible solution; T_q.
- **Evidence against / failure condition:** No cost improvement after counting propagation overhead.
- **Traceability:** OQ-CON-005; D-BTP-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 5. Directional fields and coupled control

### H-DIR-001 — Coupled directional advantage

**Hypothesis.** A field influencing both candidate generation and selection outperforms selection-only scoring on structured, sparse-evidence tasks.

- **Intervention / comparator:** B4 vs B3; same field information and total compute.
- **Primary endpoint:** Primary: quality-versus-cost AUC; secondary: T_q and discovery recall.
- **Evidence against / failure condition:** No positive gain, or loss of rare-solution recall beyond tolerance.
- **Traceability:** OQ-DIR-001; D-BTP-004; D-BTP-006.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DIR-002 — Adaptive guidance beyond fixed field

**Hypothesis.** Feedback-updated fields improve held-out search efficiency compared with fixed fields when task families share transferable regularities.

- **Intervention / comparator:** B5 vs B4, feedback trained only on earlier tasks.
- **Primary endpoint:** Held-out T_q and quality AUC; calibration and drift metrics.
- **Evidence against / failure condition:** No held-out improvement or only training-set gains.
- **Traceability:** OQ-DIR-005; EXT-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DIR-003 — Multiobjective portfolios

**Hypothesis.** Pareto/diversity-aware selection retains more distinct feasible hypothesis families than single weighted-sum selection at matched quality and budget.

- **Intervention / comparator:** Pareto portfolio vs fixed scalar score, with matched portfolio size.
- **Primary endpoint:** Coverage of reference modes; diversity; best feasible quality.
- **Evidence against / failure condition:** No mode-coverage gain or material loss of best quality.
- **Traceability:** OQ-DIR-003; SPEC-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DIR-004 — Exploration safeguards

**Hypothesis.** Reserved exploration budgets mitigate policy-induced blind spots relative to greedy field-driven search.

- **Intervention / comparator:** B4 with epsilon exploration or stratified quota vs greedy B4.
- **Primary endpoint:** Rare-mode recall and worst-group discovery rate.
- **Evidence against / failure condition:** No gain or excessive quality/cost penalty beyond preregistered bounds.
- **Traceability:** OQ-DIR-004; SPEC-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-DIR-005 — Resource allocation benefit

**Hypothesis.** Uncertainty-aware resource allocation achieves higher discovery value per unit cost than uniform allocation when evidence costs vary.

- **Intervention / comparator:** Information-value scheduler vs equal-budget allocation.
- **Primary endpoint:** Validated discoveries per cost and net information gain.
- **Evidence against / failure condition:** No net improvement after evidence-acquisition overhead.
- **Traceability:** OQ-DIR-006; D-BTP-005.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 6. Weak evidence and counterevidence

### H-EVD-001 — Search utility without proof

**Hypothesis.** Weak signals can improve search prioritization even when their standalone predictive accuracy is insufficient for proof or hard rejection.

- **Intervention / comparator:** B4 with weak-evidence guidance vs B2, retaining identical hard constraints.
- **Primary endpoint:** T_q, valid-hypothesis recall, calibration, false rejection count.
- **Evidence against / failure condition:** No search gain or any weak-signal-induced hard rejection.
- **Traceability:** OQ-EVD-001; D-BTP-005.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVD-002 — Dependency-aware evidence

**Hypothesis.** Provenance/dependency-aware aggregation reduces overconfidence from correlated evidence compared with naive evidence summation.

- **Intervention / comparator:** Dependency-aware vs naive aggregator on controlled correlated-signal suites.
- **Primary endpoint:** Calibration error, Brier score, overconfidence on false hypotheses.
- **Evidence against / failure condition:** No calibration benefit under strong correlation.
- **Traceability:** OQ-EVD-002; SPEC-004.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVD-003 — Active counterevidence

**Hypothesis.** Selecting evidence queries that discriminate between competing hypotheses reduces premature convergence relative to confirmatory querying.

- **Intervention / comparator:** Counterevidence-oriented acquisition vs highest-support acquisition.
- **Primary endpoint:** Time to eliminate incorrect leading hypothesis; false confidence rate.
- **Evidence against / failure condition:** No reduction or larger cost without accuracy gain.
- **Traceability:** OQ-EVD-003; CASE-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVD-004 — Directional similarity transfer

**Hypothesis.** REN-style directional relations help retrieve useful candidate hypotheses across heterogeneous starmaps better than undirected similarity in selected tasks.

- **Intervention / comparator:** Directional vs symmetric similarity retrieval, matched embedding and index budget.
- **Primary endpoint:** Top-k valid-candidate recall and downstream T_q.
- **Evidence against / failure condition:** No benefit or benefit limited to leakage-prone benchmarks.
- **Traceability:** OQ-EVD-004; D-BTP-005.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVD-005 — Evidence drift detection

**Hypothesis.** Explicit drift monitoring and evidence-version invalidation reduce persistent misranking after source distributions change.

- **Intervention / comparator:** Drift-aware B5 vs frozen B5 under controlled temporal shifts.
- **Primary endpoint:** Post-shift regret, recovery cost, stale-evidence reuse.
- **Evidence against / failure condition:** No recovery improvement or excessive false alarms.
- **Traceability:** OQ-EVD-005; SPEC-004.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 7. Multi-agent relay and collective learning

### H-MAG-001 — Diversity of competing agents

**Hypothesis.** Heterogeneous agents discover more nonredundant valid hypothesis families than homogeneous agents at equal total budget.

- **Intervention / comparator:** B6 heterogeneous vs B6 homogeneous vs single-agent B5.
- **Primary endpoint:** Unique validated modes per cost; quality AUC.
- **Evidence against / failure condition:** No diversity gain after accounting for coordination overhead.
- **Traceability:** OQ-MAG-001; CASE-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-MAG-002 — Productive disagreement

**Hypothesis.** Disagreement-triggered verification improves error detection compared with consensus-only selection.

- **Intervention / comparator:** Adversarial reviewer/verification agent vs majority-vote-only policy.
- **Primary endpoint:** Incorrect accepted hypotheses detected; validation cost.
- **Evidence against / failure condition:** No detection improvement or unacceptable false alarms.
- **Traceability:** OQ-MAG-002; D-BTP-007.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-MAG-003 — Relay interoperability

**Hypothesis.** Contract-checked SHU relay yields fewer semantic and provenance errors than unstructured agent message passing.

- **Intervention / comparator:** Typed SHU relay vs free-form transfer under schema/version perturbations.
- **Primary endpoint:** Misinterpreted constraints, lost provenance, replay success.
- **Evidence against / failure condition:** No error reduction or prohibitive transfer overhead.
- **Traceability:** OQ-MAG-003; SPEC-004.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-MAG-004 — Collective learning vs reuse

**Hypothesis.** A learned generator or policy can improve on unseen task families beyond the benefit of simply retrieving prior successful hypotheses.

- **Intervention / comparator:** B7 learned policy vs B6 retrieval-only, held-out structural families.
- **Primary endpoint:** Out-of-distribution T_q and feasible discovery; adaptation cost.
- **Evidence against / failure condition:** No transfer advantage on held-out families.
- **Traceability:** OQ-MAG-005; EXT-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-MAG-005 — Collective error amplification

**Hypothesis.** Independent relay validation and provenance-based de-duplication reduce correlated errors propagated among agents.

- **Intervention / comparator:** Validated relay vs unchecked relay under injected misleading shared source.
- **Primary endpoint:** Propagation depth of false claims; correlated error rate.
- **Evidence against / failure condition:** No reduction or unacceptable rejection of valid novel claims.
- **Traceability:** OQ-MAG-004; SPEC-004.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 8. Recursive evolution and open-ended growth

### H-EVO-001 — Field search as a second frontier

**Hypothesis.** Searching a versioned portfolio of directional fields improves held-out search efficiency over local weight tuning alone.

- **Intervention / comparator:** Field-structure proposals vs parameter-only tuning; matched tuning budget.
- **Primary endpoint:** Held-out quality AUC and field diversity.
- **Evidence against / failure condition:** No gain or unstable performance across seeds.
- **Traceability:** OQ-EVO-002; EXT-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVO-002 — Residual-driven operator proposals

**Hypothesis.** Persistent residual patterns can prioritize useful new generator operators better than random operator proposals.

- **Intervention / comparator:** Residual-guided operator discovery vs random proposals with same validation budget.
- **Primary endpoint:** Rate of validated operator improvements per proposal and cost.
- **Evidence against / failure condition:** No enrichment in successful proposals.
- **Traceability:** OQ-EVO-004; EXT-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVO-003 — Validated RSI threshold

**Hypothesis.** Promoted policy revisions can yield reproducible improvements across multiple held-out cycles without increasing unsoundness.

- **Intervention / comparator:** Versioned promotion gate vs uncontrolled self-revision, longitudinal holdouts.
- **Primary endpoint:** Successive independent generalization gains, rollback rate, correctness violations.
- **Evidence against / failure condition:** Gains disappear on independent tests or correctness degrades.
- **Traceability:** OQ-EVO-001; SPEC-004.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-EVO-004 — Relay frontier growth

**Hypothesis.** Cross-task relay of validated representations/operators improves new-task discovery beyond transferring final hypotheses alone.

- **Intervention / comparator:** Operator/representation relay vs hypothesis-only relay.
- **Primary endpoint:** New-domain feasible discovery and reuse-adjusted cost.
- **Evidence against / failure condition:** No improvement on domain-shifted tasks.
- **Traceability:** OQ-EVO-003; EXT-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 9. Application and transfer

### H-APP-001 — Starmap matching applicability

**Hypothesis.** Dynamic BTP is especially useful when relation candidates emerge after partial matching, not necessarily when all pairs are known.

- **Intervention / comparator:** B1–B5 across staged-reveal and fully-known graph alignment.
- **Primary endpoint:** Correct match recall and quality AUC by regime.
- **Evidence against / failure condition:** No staged-reveal benefit or pervasive static dominance.
- **Traceability:** OQ-APP-001; CASE-002.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-APP-002 — Latent behavioral actor attribution

**Hypothesis.** Cardinality-aware, constraint-guided D-BTP recovers simulated latent behavioral clusters better than simple address clustering in defined synthetic settings.

- **Intervention / comparator:** D-BTP vs clustering and graph baselines on labeled synthetic chains.
- **Primary endpoint:** Pairwise clustering F1, split/merge error, abstention calibration.
- **Evidence against / failure condition:** No gain or false real-world identity conclusions.
- **Traceability:** OQ-APP-002; CASE-001.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-APP-003 — Strategic search transfer

**Hypothesis.** Competitive structural hypotheses with directional fields improve strategy coverage in deterministic game-like tasks over a fixed search heuristic.

- **Intervention / comparator:** B6 vs single-policy search under equal simulator calls.
- **Primary endpoint:** Valid strategy diversity, regret against reference, cost.
- **Evidence against / failure condition:** No performance improvement or instability under adversarial tasks.
- **Traceability:** OQ-APP-003; CASE-003.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

### H-APP-004 — Cross-domain generality

**Hypothesis.** Shared Bucket/SHU contracts allow at least two dissimilar domains to reuse the same search core with only domain-specific plugins.

- **Intervention / comparator:** Implement graph matching and scheduling/strategy toy domains.
- **Primary endpoint:** Fraction of unchanged core interfaces; conformance pass rate; adaptation cost.
- **Evidence against / failure condition:** Core requires unacknowledged domain-specific semantics or cannot pass conformance.
- **Traceability:** OQ-APP-004; SPEC-001–004.

**Test design.** Construct or sample task instances across at least three predeclared difficulty strata. Hold instance families constant across arms; use matched compute and the same feasibility oracle. Record generation traces, accepted/rejected/unknown constraint results, directional-field versions, provenance and termination state. Estimate paired effects with uncertainty intervals and inspect counterexamples, including cases where the treatment is worse. If the hypothesis involves learning, use disjoint held-out instances and disclose all tuning trials.

## 10. Cross-cutting measurement and reproducibility protocol

### 10.1 Quality and correctness

- **Feasibility precision:** share of returned hypotheses satisfying the declared hard constraints, checked independently.
- **Feasible recall:** share of oracle-valid solutions found on enumerable small instances; report coverage limits on larger instances.
- **Structural quality:** task-specific alignment accuracy, objective score, or distance to a reference optimum; do not substitute a search heuristic for ground truth.
- **Abstention:** share of uncertain outputs explicitly withheld rather than asserted; report error conditional on abstention.
- **Pruning soundness:** count of feasible branches eliminated by purported hard pruning; target **zero** in oracle-tractable tests.
- **Termination integrity:** distinguish proven closed, currently quiescent, and budget-terminated partial results.

### 10.2 Efficiency and exploration

Record wall-clock time, CPU/GPU time, memory peak, plugin invocations, generator calls, unique Bucket expansions, duplicate states, evidence-query costs, agent communication, and serialization. Use quality-versus-cost curves and anytime performance, not only the final best score. A directional method that wins at a large budget but loses at the user's likely budget should be reported as such.

### 10.3 Directional evidence and uncertainty

Track field calibration, distribution drift, source dependence, effective evidence diversity, contradictory signals, and rate of high-confidence false hypotheses. Distinguish *search priority* from *posterior belief* and from *proof*. When a weak signal is used to reorder work, audit whether it ever indirectly triggered an unsound hard rejection.

### 10.4 Multi-agent and learning measurements

Measure distinct valid hypotheses per unit **total** compute, not per-agent compute; relay acceptance/rejection, provenance preservation, duplicated work, convergence diversity, policy revision frequency, and held-out improvement after policy promotion. Report whether improvements persist when a new evaluator, task seed, or domain family is used.

## 11. Benchmark suite and data splits

| Suite | Construction | Oracle / label | Key stressors |
|---|---|---|---|
| S1: Exact toy graphs | Small typed starmaps with known alignments | Enumerated feasible matches | Soundness, state equivalence, closure |
| S2: Staged-reveal graphs | Relations become discoverable after decisions | Hidden planted correspondences | Dynamic generation, discovery recall |
| S3: Constraint conflict suite | Contradictory and conditional plugins | Independently checked SAT/constraint oracle | Unknown vs Fail, sound pruning |
| S4: Directional distractors | Helpful, neutral and misleading signals | Planted valid solutions | Blind spots, evidence calibration |
| S5: Correlated evidence | Shared latent causes across evidence items | Known data-generating process | Double counting, counterevidence |
| S6: Synthetic ledger networks | Many-to-one and one-to-many latent actor behaviors | Synthetic actor assignments | Cardinality, clustering error, abstention |
| S7: Multi-agent structural games | Deterministic strategy search instances | Simulator outcomes | Diversity, coordination cost |
| S8: Domain transfer | Graphs, scheduling and other distinct domains | Domain-specific feasibility checks | Contract portability, transfer |
| S9: Longitudinal policy evolution | Repeated task families with distribution shift | Sealed future-task evaluations | RSI claims, drift, rollback |

Use synthetic or permissioned datasets by default for attribution tasks. A blockchain behavioral cluster is **not** an identified person; public network artifacts, IP addresses, keys or device metadata must not be treated as proof of personal identity. Evaluate privacy leakage and false accusation risk separately from algorithmic clustering performance.

### 11.1 Splitting and leakage controls

Separate generators of test instances, not merely individual samples: two graphs generated from the same latent template can leak structure across splits. For multi-agent trials, freeze all prompt templates, plugins and shared memories before opening the test set. For evolving systems, maintain an immutable evaluation suite and a rotating secret suite to limit overfitting.

## 12. Preregistration template

```yaml
hypothesis_id: H-DIR-001
version: 1
status: proposed
population: staged-reveal typed-starmap tasks
primary_endpoint: quality_cost_auc
minimum_practical_gain: TO_BE_SET_BEFORE_RUN
comparison: coupled_field_vs_selection_only
budget_unit: total_compute_cost
budget_levels: TO_BE_REGISTERED
seeds: TO_BE_REGISTERED
sample_size_and_power: TO_BE_JUSTIFIED
statistical_method: paired_bootstrap_or_predeclared_alternative
multiplicity_family: directional_field_primary_endpoints
correctness_gate: zero_confirmed_unsound_hard_pruning
holdout_policy: sealed_instance_families
artifact_requirements: [configuration, versions, seeds, traces, metrics]
stop_rule: fixed_budget_or_predeclared_sequential_rule
```

The placeholders are intentional: no numerical threshold or sample size is justified without a pilot variance estimate and target use case. Choose them **before** inspecting confirmatory outcomes. If an experiment is exploratory, label it exploratory and avoid retroactively presenting its threshold as preregistered.

## 13. Statistical analysis and interpretation

1. **Pair by task.** Compute per-instance differences before aggregating, stratify by instance family and complexity, and show the full distribution.
2. **Report uncertainty.** Use confidence/credible intervals for the primary endpoint and disclose statistical assumptions; do not interpret `p > 0.05` as proof of no effect.
3. **Control selection.** Count all tested variants, hyperparameter sweeps and failed policy revisions. Keep the confirmatory test set sealed.
4. **Use practical thresholds.** A statistically detectable but tiny gain that costs substantial implementation complexity may not support adoption.
5. **Audit correctness first.** Any reproducible unsound hard pruning, evidence leakage, or invalid state merge is a blocker independent of mean speedup.
6. **Separate transfer from memorization.** Test novel structural families, not only new random seeds from a familiar template.
7. **Report negative results.** Publish conditions in which static BTP, greedy selection or single-agent search is superior.

## 14. Ablation and factorial designs

The principal D-BTP mechanism has at least four potentially interacting factors: **D** dynamic generation, **G** generation-time directional guidance, **S** selection-time directional guidance, and **F** feedback adaptation. A controlled factorial or carefully chosen partial factorial study should estimate main effects and interactions, particularly `G × S` and `D × G`. A comparison of fully enabled D-BTP with static BTP alone cannot identify which mechanism caused a gain.

For multi-agent experiments add **A** agent diversity and **R** typed relay, but keep total compute fixed. For constraint experiments vary propagation **P** and plugin validation **V**, preserving the same declared hard constraints. For recursive improvement, distinguish learning a policy parameter from learning a new policy structure and from promoting a validated improvement.

## 15. Conformance gates before performance claims

| Gate | Requirement | Linked specification |
|---|---|---|
| C1 | Bucket ledger transitions preserve decision consistency and provenance | SPEC-001 |
| C2 | Candidate generators declare scope, version and determinism assumptions | SPEC-002 |
| C3 | Hard-constraint Fail is distinguishable from Unknown and Error | SPEC-002 |
| C4 | Sound pruning has an independently checkable justification | SPEC-002 |
| C5 | Directional score cannot silently override hard feasibility | SPEC-003 |
| C6 | Budget, priority and termination semantics are explicit | SPEC-003 |
| C7 | Evidence dependencies and revisions are traceable | SPEC-004 |
| C8 | Relay receivers revalidate applicable constraints and provenance | SPEC-004 |
| C9 | Learned policy versions have rollback and independent evaluation | SPEC-004 |

Performance results from configurations failing a relevant gate should be marked **non-conformant**, not used as evidence of a sound algorithmic improvement.

## 16. Priority experiment packages

**P0 — Correctness before speed.** Execute S1 and S3, focusing on H-DYN-003/004 and H-CON-001/002/003. Deliver a reproducible conformance report and explicit counterexamples.

**P1 — The core coupled-generation hypothesis.** Execute S2 and S4, testing H-DYN-001/002, H-DIR-001/003/004 with B1–B4 under equal compute. This is the highest-priority empirical test of D-BTP's distinctive claim.

**P2 — Weak evidence as search guidance.** Execute S4 and S5 for H-EVD-001/002/003. Measure benefit without granting weak evidence the status of a hard constraint.

**P3 — Collective structural learning.** Execute S7 and S8 for H-MAG-001/003/004/005; include communication overhead and source correlation.

**P4 — Recursive directional evolution.** Execute S9 for H-DIR-002, H-EVO-001/002/003/004 with sealed evaluation and reversible policy promotion. This phase is not evidence of RSI unless repeated held-out improvements survive independent review.

**P5 — Application stress tests.** Execute S6 and selected S7/S8 for H-APP-001–004. Treat behavioral actor attribution as uncertain structural inference, not personal identification.

## 17. Results registry and evidence grades

For each completed run, store: `experiment_id`, hypothesis ID, task suite and split hash, exact code/contract versions, plugin manifests, seed list, resource limits, all baseline outputs, quality/cost curves, constraint audit, statistical analysis, negative cases and a machine-readable summary. Use the following non-exclusive result labels:

- **Proposed:** not yet tested.
- **Exploratory observation:** tested without a sealed confirmatory protocol.
- **Supported in scope:** preregistered criteria met on specified task distributions.
- **Not supported in scope:** prespecified meaningful gain not established.
- **Inconclusive:** uncertainty or data quality prevents a decision.
- **Correctness failure:** violated a required invariant; supersedes performance claims.
- **Replication pending / replicated:** independent confirmation status.

A hypothesis may be supported on staged-reveal starmaps and not supported on complete small inventories; record both rather than collapsing into a universal success/failure claim.

## 18. Relationship to the D-BTP research corpus

- **Foundations:** [D-BTP-001](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md) through [D-BTP-008](docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md) motivate the conceptual mechanisms.
- **Specifications:** [SPEC-001](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md), [SPEC-002](docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md), [SPEC-003](docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md), [SPEC-004](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md) define normative contracts and conformance expectations.
- **Cases:** [CASE-001](docs/cases/CASE-001-Blockchain-Actor-Attribution.md), [CASE-002](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md), [CASE-003](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md) suggest application-grounded stress tests.
- **Extensions:** [EXT-001](docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md), [EXT-002](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md), [EXT-003](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md) contain longer-horizon proposals requiring stronger evidence.
- **Registry companions:** [OPEN-QUESTIONS.md](OPEN-QUESTIONS.md) captures unresolved research questions; [FUTURE-DIRECTIONS.md](FUTURE-DIRECTIONS.md) prioritizes directions; [VALIDATION-ROADMAP.md](VALIDATION-ROADMAP.md) should track implementation phases, acceptance gates and completed results.

## 19. Closing research position

The strongest potential contribution of D-BTP is a **testable coupling**: structural hypotheses are generated dynamically, directional fields influence both what is generated and what receives attention, constraints preserve feasible interpretation, and feedback can revise future guidance. The correct scientific outcome may be a conditional advantage, a narrower mechanism, or a negative result. The registry is designed to make all three outcomes useful to a collective research program.
