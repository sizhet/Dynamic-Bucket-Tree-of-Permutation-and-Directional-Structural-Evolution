# EXT-001 — Biomimetic Directional Intelligence

**Project:** D-BTP — Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document type:** Research extension / hypothesis and design study  
**Status:** v1.0.0 research proposal; mechanisms and claims require empirical validation  
**Repository path:** `docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md`

## Abstract

Biological organisms often explore an uncertain environment without enumerating every possible action. Their behavior can exhibit selective attention, active sensing, memory-dependent exploration, adaptive allocation of effort, and revision of expectations after unexpected observations. This extension investigates whether those functional motifs can inform Dynamic Bucket Tree of Permutation (D-BTP), a framework for generating and evaluating evolving structural hypotheses. The proposed analogy is **functional, not anatomical**: D-BTP is not claimed to model the brain, and similarities in observable behavior do not establish shared internal algorithms.

We propose a biomimetic directional search architecture in which candidate hypotheses, directional fields, evidence acquisition, and feedback form a coupled loop. We distinguish biological inspiration from engineering implementation and specify measurable predictions, ablations, and failure conditions. Particular attention is paid to weak evidence, counterevidence, uncertainty, exploration diversity, and the separation of feasibility from priority. The objective is a testable program for adaptive structural search rather than an assertion of biological equivalence or general intelligence.

**Keywords:** dynamic BTP; biomimetic intelligence; directional fields; active sensing; structural hypotheses; weak evidence; exploration–exploitation; collective learning; adaptive search.

---

## 1. Motivation and Research Position

A conventional structural matcher can evaluate a predefined collection of candidate correspondences. D-BTP instead treats the candidate set as a function of the current structural state, observed evidence, and search policy. This distinction invites a comparison with organisms that discover relevant possibilities while acting: an animal need not possess a complete list of routes, food sources, or threat explanations before exploring.

The useful question is not whether D-BTP *is* a biological cognitive mechanism. It is whether certain biologically inspired design principles can improve computational search under incomplete information:

1. Generate new options from context rather than relying solely on a fixed option list.
2. Allocate attention and effort directionally.
3. Seek observations that distinguish competing hypotheses.
4. Retain uncertainty and counterevidence rather than collapsing early to a single explanation.
5. Update search policies from validated outcomes.

These are engineering hypotheses. They should be tested against simpler baselines, including unguided dynamic search and fixed-direction heuristics.

## 2. Scope and Epistemic Boundaries

This document addresses computational analogies to adaptive behavior, not neuroscience claims about neural circuits. Terms such as *attention*, *curiosity*, *expectation*, and *memory* refer to operational functions of an engineered system unless explicitly identified as biological observations.

Three levels of assertion must remain separate:

- **Biological observation:** organisms can exhibit adaptive, information-seeking behavior in specific tasks.
- **Functional analogy:** D-BTP can be designed to exhibit corresponding computational functions.
- **Mechanistic identity:** the organism actually implements a BTP-like algorithm.

Only the first two are within the intended scope. Mechanistic identity is neither assumed nor established here. Similarly, a system's ability to adapt its search policy does not by itself establish consciousness, autonomy in the human sense, or artificial general intelligence.

## 3. The D-BTP Search Unit

Let a dynamic Bucket at time or iteration \(t\) be

\[
\mathcal{B}_t = (H_t,S_t,E_t,P_t,M_t),
\]

where:

- \(H_t\) is the hypothesis ledger, including accepted, rejected, deferred, and unresolved propositions;
- \(S_t\) is the composed structural state and constraint context;
- \(E_t\) is the evidence set with provenance, dependencies, and uncertainty;
- \(P_t\) is the directional search and resource-allocation state;
- \(M_t\) is metadata including versions, budgets, audit history, and termination status.

Candidate hypotheses are dynamically generated:

\[
C_t = G(\mathcal{B}_t,\Phi_t,\mathcal{R}_t),
\]

where \(\Phi_t\) denotes directional fields and \(\mathcal{R}_t\) represents permitted tools, plugins, and resources. A transition accepts, rejects, defers, or probes a candidate while preserving hard constraints and provenance.

This architecture provides the substrate for biomimetic analogies without requiring a literal mapping to biological structures.

## 4. Five Biomimetic Functional Motifs

### 4.1 Context-sensitive candidate discovery

An organism's feasible behavioral options depend on its location, observations, and recent history. Analogously, D-BTP may generate different structural hypotheses after a new relation is accepted or contradicted. The hypothesis space is *operationally revealed* over time, although the formal generator may still have a bounded representational capacity.

### 4.2 Selective attention and directional effort

A direction field may prioritize candidates by estimated relevance, information gain, novelty, risk, and expected computational cost. The field is a policy for allocating finite effort, not a truth oracle.

### 4.3 Active sensing and discriminative probing

Rather than passively scoring available evidence, a search agent may request the next measurement most likely to distinguish competing hypotheses. The resulting observation can modify both the hypothesis ledger and the directional policy.

### 4.4 Memory-dependent adaptation

Past search traces can reveal useful generators, recurring failure modes, or unproductive directions. Such traces should be retained with domain and distribution metadata, because a policy learned in one environment may fail in another.

### 4.5 Exploration diversity

Biological search is not always greedy. A D-BTP portfolio may similarly reserve budget for lower-ranked but structurally distinct hypotheses, reducing premature convergence and improving resilience to misleading signals.

## 5. Coupled Generation and Directional Selection

A central D-BTP proposition is that generation and selection are not merely two independent sequential stages. The direction field can affect which candidates are generated at all, while newly generated structures and observations reshape the field.

A conceptual loop is:

\[
\begin{aligned}
C_t &= G(\mathcal{B}_t,\Phi_t),\\
A_t &= \Pi(C_t,\mathcal{B}_t,\Phi_t,\text{budget}_t),\\
(\mathcal{B}_{t+1},Y_t) &= T(\mathcal{B}_t,A_t),\\
\Phi_{t+1} &= U(\Phi_t,\mathcal{B}_{t+1},Y_t).
\end{aligned}
\]

Here \(A_t\) is the selected search action, \(Y_t\) is observed feedback, \(T\) is a constraint-aware state transition, and \(U\) is an update rule. The feedback must be qualified by provenance and validation status before it influences long-lived policy parameters.

The equation is a design abstraction, not a guarantee that \(U\) improves performance.

## 6. Directional Fields as Operational Constructs

A useful field is multi-component:

\[
\Phi_t = (\phi_{\mathrm{goal}},\phi_{\mathrm{information}},
\phi_{\mathrm{novelty}},\phi_{\mathrm{risk}},\phi_{\mathrm{cost}},
\phi_{\mathrm{diversity}})_t.
\]

Each component may score candidate generation opportunities, proposed actions, or entire Buckets. Scores should carry scale, uncertainty, version, applicability, and evidence lineage. A weighted scalar score is one possible selection method:

\[
q_t(a)=\sum_i w_{i,t}\,\widehat{\phi}_{i,t}(a),
\]

but Pareto ranking, lexicographic policy, or constrained portfolio selection may be preferable when objectives conflict. The normalization \(\widehat{\phi}\) and weights \(w\) must be specified; otherwise comparisons across agents or experiments may be invalid.

**Non-negotiable separation:** a low directional score does not prove infeasibility. Only sound hard-constraint reasoning can justify a logically irreversible rejection.

## 7. Weak Evidence as a Search Signal

Weak evidence can have limited probative strength while still being useful for choosing the next experiment. For example, a repeated temporal pattern may suggest where to look for a relation, without establishing that the relation exists.

Evidence records should distinguish:

- the observation itself;
- its source and acquisition method;
- dependence on other observations;
- reliability and uncertainty estimates;
- the hypothesis to which it pertains;
- counterevidence and alternative explanations;
- permitted uses, such as ranking, probing, or hard validation.

Multiple correlated observations must not be treated as independent confirmations. A promising direction may be valuable because it enables a cheap discriminative test, even if the initial evidence is unreliable.

## 8. Active Perception and Information Gain

Suppose a portfolio contains hypotheses \(\mathcal{H}=\{h_1,\dots,h_k\}\). A proposed observation action \(a\) can be ranked by expected reduction in uncertainty:

\[
\operatorname{EIG}(a)=H(\mathcal{H}\mid E_t)-
\mathbb{E}_{y\sim p(y\mid a,E_t)}
\big[H(\mathcal{H}\mid E_t,y)\big].
\]

This expression is meaningful only when the probability model and its calibration are defensible. In settings without trustworthy probabilities, D-BTP can use qualitative disagreement reduction, bounded uncertainty intervals, or expected constraint elimination as substitutes. Information gain is an *exploration heuristic* and should not be confused with proof of a candidate hypothesis.

## 9. Surprise, Residuals, and Candidate Invention

A prediction residual can signal a gap in the current structural representation:

\[
r_t = d\big(y_t,\widehat{y}_t(\mathcal{B}_t)\big).
\]

Large residuals may motivate new candidate relations, alternative causal explanations, or revised generation operators. However, surprise can also arise from sensor noise, distribution shift, or model misspecification. A responsible system should test simpler explanations before introducing more complex structures.

One proposed policy allocates a limited **residual-driven invention budget** to novel generators while preserving a baseline exploration budget. This makes the open-ended-growth claim measurable: new operators must improve held-out tasks, not merely create more hypotheses.

## 10. Exploration–Exploitation with Structural Portfolios

Greedy search may concentrate resources on the first attractive explanation. A biomimetic D-BTP controller can allocate a budget across:

- exploitation of high-scoring feasible branches;
- exploration of diverse alternative structures;
- targeted counterevidence collection;
- verification of uncertain constraints;
- operator or directional-policy experiments.

A portfolio \(\mathcal{P}_t\) should preserve structurally non-equivalent hypotheses, with explicit limits on duplicate states and redundant evidence. Diversity measures must be defined over relevant structural differences, not superficial text variations.

No universal allocation ratio is proposed. Optimal allocation is likely task- and budget-dependent.

## 11. Multi-Agent Biomimetic Roles

A distributed implementation may assign distinct roles to agents:

| Agent role | Primary responsibility | Required safeguard |
| --- | --- | --- |
| Explorer | Propose novel structural candidates | Record generation rationale and cost |
| Constraint examiner | Check hard and conditional feasibility | Never promote soft scores into hard rejection |
| Directional navigator | Rank branches and allocate effort | Expose policy version and uncertainty |
| Evidence scout | Request discriminative observations | Track source, permissions, and dependencies |
| Counterexample seeker | Challenge leading hypotheses | Preserve dissent and independent tests |
| Relay curator | Package reusable structural units | Validate compatibility and provenance |
| Learning evaluator | Compare policy revisions | Use held-out tests and rollback controls |

These are logical roles, not a requirement for seven distinct models. A single agent can implement multiple roles; multiple agents may introduce substantial communication and coordination overhead.

## 12. Structural Relay and Collective Learning

A successful local search result is not automatically reusable knowledge. A relayable Structural Hypothesis Unit (SHU) should include the structural claim, constraint assumptions, evidence provenance, scope of applicability, unresolved alternatives, evaluation outcomes, and versioned policy context.

Receiving agents must independently validate the SHU against their own constraints and environment. Collective learning occurs when accumulated experience changes future candidate generation, search prioritization, or evidence acquisition in a demonstrably useful way. Mere exchange of messages is not sufficient evidence of learning.

This design connects to D-BTP-007 and SPEC-004, while remaining compatible with broader structural relay and competitive learning research.

## 13. Distinguishing Adaptation from RSI

Three nested processes should be evaluated separately:

1. **Search adaptation:** the current Bucket and direction field change as new evidence arrives.
2. **Cross-task learning:** experience from prior searches modifies reusable parameters or strategies.
3. **Validated recursive self-improvement:** the system proposes modifications to its own learning/search mechanisms, tests them independently, and retains improvements under controlled governance.

A self-modification attempt that worsens performance is still an experiment, not an achieved improvement. Claims of RSI require longitudinal, held-out evidence of improvements to the improvement process itself, including costs and regressions.

## 14. Illustrative Synthetic Scenario: Foraging-Like Search

Consider an abstract grid with several potential resource sites. An agent starts with uncertain location-to-resource relationships and a finite sensing budget. The example is a computational benchmark inspired by foraging, not a simulation validated against animal behavior.

- **Initial state:** sparse observations, three plausible resource clusters, and uncertain movement costs.
- **Generation:** nearby observations and structural continuity produce candidate routes and cluster hypotheses.
- **Directional selection:** estimated reward, information gain, travel cost, and uncertainty rank actions.
- **Active probe:** the agent samples a site selected to discriminate between two competing cluster hypotheses.
- **Feedback:** the observation updates structural relations and may shift attention toward an alternative cluster.
- **Counterevidence:** a second agent deliberately probes the strongest hypothesis's predicted failure region.
- **Relay:** validated route motifs and their environmental assumptions become reusable SHUs.

A successful run would show improved resource discovery per unit cost relative to suitable baselines. It would **not** demonstrate that biological foragers use D-BTP.

## 15. Illustrative Synthetic Scenario: Dynamic Starmap Matching

Two starmaps contain partially observed nodes and relations. A static matcher starts with a fixed pair list. A dynamic matcher creates candidate correspondences after each accepted relation. A directional controller prioritizes pairs expected to resolve ambiguous substructures; a counterexample agent probes inconsistent neighborhoods.

The benchmark can vary missing-edge rates, false clues, graph size, relation ambiguity, and candidate-generation quality. Outcomes include feasible-match recall, search cost, constraint violations, structural diversity, and sensitivity to misleading weak evidence. This scenario directly connects the biomimetic analogy to the original BTP use case without requiring biological data.

## 16. Reference Algorithm Sketch

```text
procedure BiomimeticDirectionalDBTP(initial_bucket, generators,
                                    constraint_plugins, field_policy,
                                    budgets):
    frontier := {initial_bucket}
    portfolio := empty
    evidence_log := empty

    while frontier not empty and budgets permit:
        bucket := select_bucket(frontier, field_policy, diversity_policy)
        candidates := generate_from_state(bucket, generators, field_policy)
        candidates := deduplicate_with_provenance(candidates)

        for candidate in candidates:
            verdict := evaluate_constraints(bucket, candidate, constraint_plugins)
            if verdict == PROVEN_INFEASIBLE:
                record_sound_rejection(bucket, candidate, verdict)
                continue
            if verdict in {UNKNOWN, ERROR}:
                schedule_verification_or_defer(bucket, candidate)
                continue

            actions := {accept_branch, reject_branch, targeted_probe}
            action := prioritize(actions, candidate, bucket, field_policy)
            successors, observations := execute_bounded_action(action)
            evidence_log.add(observations)
            for successor in successors:
                verify_invariants(successor)
                frontier.add_if_novel(successor)
                portfolio.consider(successor)

        validated_feedback := independently_validate(evidence_log)
        field_policy := guarded_update(field_policy, validated_feedback)
        preserve_diverse_alternatives(frontier, portfolio)

    return portfolio, audit_trail, termination_reason
```

The sketch omits implementation-specific synchronization, transactional rollback, resource metering, and generator completeness guarantees. In particular, `PROVEN_INFEASIBLE` requires a sound plugin certificate under stated assumptions.

## 17. Required Invariants

**BI-01 — Feasibility separation.** Directional scores never independently justify hard rejection.

**BI-02 — Traceable generation.** Every candidate records its generating operator, input Bucket version, and rationale.

**BI-03 — Evidence lineage.** Observations retain source, timestamp or sequence, dependency information, and permitted usage.

**BI-04 — Counterevidence preservation.** Relevant contradictory observations cannot be silently discarded by a scoring update.

**BI-05 — Budget accountability.** Probing, branching, agent communication, and policy learning consume recorded resources.

**BI-06 — Version coherence.** A transition uses an identifiable compatible set of generator, constraint, and field-policy versions.

**BI-07 — Distinct termination states.** Proven closure, temporary quiescence, and budget exhaustion are reported separately.

**BI-08 — Controlled policy updates.** Persistent strategy changes require independent evaluation and rollback support.

**BI-09 — Portfolio diversity.** Distinct alternatives are retained according to an explicit diversity policy, not hidden consensus.

**BI-10 — Scoped transfer.** A relayed hypothesis or policy carries its applicability assumptions and validation status.

## 18. Testable Hypotheses

| ID | Hypothesis | Falsifiable comparison |
| --- | --- | --- |
| BH-01 | Context-sensitive generation improves feasible-hypothesis recall under incomplete initial candidate sets. | Dynamic vs fixed candidate list at matched compute budgets |
| BH-02 | Coupled generation and selection outperforms post-hoc ranking on some sparse-information tasks. | Coupled field vs generate-then-rank |
| BH-03 | Active probing reduces evidence acquisition cost to distinguish competing hypotheses. | Disagreement/information-directed vs random probing |
| BH-04 | Diversity preservation reduces catastrophic early convergence under misleading signals. | Portfolio search vs greedy top-1 |
| BH-05 | Counterevidence-seeking agents improve error detection. | With vs without independent challenger |
| BH-06 | Provenance-aware evidence fusion reduces confidence inflation from correlated clues. | Dependency-aware vs naive aggregation |
| BH-07 | Cross-task policy learning yields positive transfer within a defined task family. | Trained policy vs fresh policy on held-out tasks |
| BH-08 | Guarded operator evolution can improve search efficiency without violating hard constraints. | Frozen operators vs validated operator updates |
| BH-09 | Multi-agent gains can exceed coordination overhead only in identifiable regimes. | Agent counts and role partitions under total-cost accounting |
| BH-10 | Residual-triggered structural invention improves recovery from representation gaps. | Residual-triggered vs fixed-generator controls |

All hypotheses may fail; a negative result should refine the scope of the biomimetic analogy.

## 19. Experimental Design

### 19.1 Benchmark families

Use at least three controlled families: (a) partially observed starmap alignment, (b) foraging-like spatial hypothesis search, and (c) dynamic constraint composition with hidden relational structure. For each family, vary problem size, missing information, misleading weak evidence, constraint density, and observation cost.

### 19.2 Ablation matrix

Compare: static BTP; dynamic unguided BTP; dynamic BTP with fixed directional scoring; coupled adaptive direction; coupled direction plus active probing; plus counterevidence; plus multi-agent relay; plus guarded cross-task learning. Use identical data partitions and comparable wall-clock, token, or compute budgets as applicable.

### 19.3 Metrics

Report feasible-hypothesis recall and precision, best validated objective value, evidence cost, constraint violation rate, calibration where probabilistic outputs exist, structural diversity, time-to-discovery, total compute/communication cost, and robustness to distribution shift. Separate training, tuning, and held-out evaluation. Use repeated seeds and uncertainty intervals rather than single-run anecdotes.

### 19.4 Negative controls

Include randomized direction fields, intentionally misleading signals, duplicate evidence, adversarially correlated clues, and tasks where static enumeration is already complete. Such controls test whether the additional machinery provides genuine benefit or merely adds overhead.

## 20. Failure Modes and Safeguards

| Failure mode | Why it matters | Mitigation |
| --- | --- | --- |
| Anthropomorphic overinterpretation | Functional analogy is mistaken for a brain model | Explicit scope statements and independent biological evidence requirements |
| Confirmation loops | A field generates evidence favorable to itself | Challenger agents, disconfirming probes, holdouts |
| Weak-to-hard promotion | Heuristics incorrectly eliminate feasible branches | Certified hard-constraint interface |
| Evidence double counting | Correlated clues inflate confidence | Provenance dependency graph |
| Novelty chasing | New structures grow without explanatory benefit | Complexity penalties and held-out validation |
| Premature convergence | Search misses alternatives | Diversity budget and portfolio retention |
| Excessive probing | Information gathering outweighs utility | Value-of-information and resource caps |
| Nonstationary transfer | Previously useful policies become harmful | Applicability metadata and drift detection |
| Multi-agent echo chambers | Agents recycle shared errors | Independent evidence and adversarial roles |
| Unsafe self-modification | Policy changes break invariants | Sandboxed evaluation, conformance gates, rollback |

## 21. Conformance-Oriented Checks

A prototype claiming compatibility with this extension should demonstrate the following minimal behaviors:

1. A change in Bucket state can alter the generated candidate set.
2. Directional policy can affect both generation and selection through documented interfaces.
3. Constraint plugins can veto only under declared soundness conditions.
4. Low-scored feasible candidates remain recoverable under an explicitly bounded exploration policy.
5. Active probes are represented as actions with cost and observable outcomes.
6. Evidence updates preserve contradictory records and provenance.
7. Portfolio selection uses a defined structural diversity measure.
8. Policy revisions can be reproduced, compared with a baseline, and rolled back.
9. Cross-task transfer is scoped by assumptions and tested on held-out tasks.
10. Outputs report whether termination reflects closure, quiescence, or exhausted budget.

These are proposed checks, not claims of an existing certified implementation.

## 22. Research Roadmap

**Phase I — Formal baseline.** Implement deterministic dynamic candidate generation and sound constraint plugins on synthetic starmaps. Establish correctness and cost baselines.

**Phase II — Directional coupling.** Introduce multi-objective fields, explicit budgets, and controlled exploration. Test generation–selection coupling against post-hoc ranking.

**Phase III — Active evidence.** Add discriminative probes, counterevidence, and provenance-aware evidence handling. Test under missing and misleading observations.

**Phase IV — Collective learning.** Relay scoped structural units across agents and tasks. Quantify communication cost and transfer performance.

**Phase V — Guarded evolution.** Permit sandboxed changes to generators and directional policies, gated by conformance and independent holdout performance.

Progression between phases should depend on empirical criteria rather than a presupposed trajectory toward general intelligence.

## 23. Relationship to the D-BTP Corpus

- **D-BTP-001:** establishes the move from metric matching to structural hypothesis search.
- **D-BTP-002:** defines dynamic Bucket states and state-dependent candidate generation.
- **D-BTP-003:** formalizes constraint-guided composition and sound pruning.
- **D-BTP-004:** develops directional fields for generation and selection.
- **D-BTP-005:** studies weak evidence as a directional exploration signal.
- **D-BTP-006:** defines the coupled generation–selection–feedback loop.
- **D-BTP-007:** explores multi-agent RSI and collective structural learning.
- **D-BTP-008:** distinguishes dynamic search from open-ended structural evolution.
- **SPEC-001–004:** provide state, generator, directional control, and evidence-relay contracts.
- **CASE-002:** supplies a natural dynamic starmap matching benchmark.
- **EXT-002:** can investigate recursive evolution of directional fields.
- **EXT-003:** can investigate open-ended structural relay and expansion.

Related conceptual connections include directional weak-evidence intelligence, relational evidence navigation, strategic competition, and autonomous question generation. These connections motivate comparative research; they do not substitute for empirical evidence.

## 24. Open Questions

1. What is the smallest directional state sufficient for robust performance gains?
2. Under which task distributions does state-dependent generation outperform a well-engineered static candidate list?
3. Can information-seeking probes be selected reliably without calibrated probabilities?
4. How should structural diversity be measured when hypotheses differ in granularity?
5. How can a system detect that its own candidate language is inadequate?
6. When does residual-driven operator invention outperform simpler model repair?
7. What safeguards best prevent feedback loops from amplifying misleading evidence?
8. How much agent independence is needed for effective counterevidence search?
9. Which cross-task structural units transfer without introducing negative transfer?
10. What evidence would justify a stronger biological analogy beyond functional resemblance?

## 25. Conclusion

Biomimetic directional intelligence offers D-BTP a productive set of **design questions**, not a ready-made biological explanation. Context-dependent candidate discovery, directional effort, active sensing, diversity preservation, and feedback-driven adaptation can be expressed as explicit search mechanisms with testable interfaces. The distinctive D-BTP proposition is the coupling: directional fields shape what is generated, generated structures reshape what is considered valuable, and validated observations can modify both.

Whether this coupling produces a meaningful advantage remains an empirical question. A credible research program must preserve sound constraints, track weak evidence and counterevidence, account for computation and coordination costs, and test transfer beyond the examples used to design the system. Within those boundaries, the biomimetic perspective may help identify practical mechanisms for more adaptive structural search and collective learning.

---

**Research note:** This document proposes hypotheses, architecture patterns, and validation protocols. It does not report completed experiments, establish neuroscientific equivalence, or demonstrate AGI/ASI.
