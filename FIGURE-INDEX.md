# Figure Index — Dynamic Bucket Tree of Permutation (D-BTP)

**Project:** Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Document:** `FIGURE-INDEX.md`  
**Status:** Research figure plan and manuscript placement guide  
**Version:** 1.0.0 preparation

## 1. Purpose and publication status

This index defines the intended roles, canonical filenames, manuscript placement, captions, and accessibility descriptions for the eight D-BTP research figures. It is a publication and consistency guide, not an assertion that eight independent image files have already been produced.

**Asset status as of this draft:** An eight-panel **composite infographic** has been generated. The eight separately named PNG files listed below have **not yet been verified as independent assets**. The repository's `README.md` and `START-HERE.md` link to the canonical individual paths; those links should be tested after exporting and inspecting each image. A cropped panel may require redrawing at higher resolution if labels become unreadable. Do not mark any figure as publication-ready without checking its actual content and resolution.

The figure sequence follows the research argument: general architecture → dynamic search → state model → constraint composition → directional coupling → weak evidence → concrete application → recursive collective evolution.

## 2. Canonical figure inventory

| Figure | Canonical file under `figures/` | Primary message | Primary manuscript |
|---|---|---|---|
| Fig-001 | `Fig-001-D-BTP-Grand-Architecture.png` | The unified D-BTP computational architecture | D-BTP-001 |
| Fig-002 | `Fig-002-From-Static-to-Dynamic-BTP.png` | A dynamic frontier differs from a fixed candidate list | D-BTP-002 |
| Fig-003 | `Fig-003-Dynamic-Bucket-State-and-Candidate-Generation.png` | State-dependent candidate generation and traceable transitions | D-BTP-002 / SPEC-001 |
| Fig-004 | `Fig-004-Constraint-Guided-Structural-Hypothesis-Search.png` | Hard constraints, propagation, and sound pruning | D-BTP-003 / SPEC-002 |
| Fig-005 | `Fig-005-Directional-Generation-and-Selection-Coupling.png` | Directional fields couple generation, selection, and feedback | D-BTP-004 / D-BTP-006 |
| Fig-006 | `Fig-006-Weak-Evidence-and-Multi-Directional-Scoring.png` | Weak evidence guides exploration without becoming proof | D-BTP-005 / SPEC-003 |
| Fig-007 | `Fig-007-Blockchain-Actor-Attribution-BTP.png` | Latent actor hypotheses mapped to observable behaviors | CASE-001 |
| Fig-008 | `Fig-008-Recursive-Structural-Evolution-and-Collective-Learning.png` | Structural relay, learning, and validated recursive improvement | D-BTP-007 / D-BTP-008 |

## 3. Detailed captions, placement, and interpretation

### Fig-001 — D-BTP Grand Architecture

**Canonical path:** `figures/Fig-001-D-BTP-Grand-Architecture.png`  
**Primary insertion:** `docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md`, immediately after the first complete overview of the proposed D-BTP mechanism, before detailed formalization.  
**Secondary references:** `README.md`; D-BTP-006; D-BTP-008.

**Proposed caption:** *Fig-001. D-BTP grand architecture. A dynamic bucket maintains structural hypotheses and evidence; state-dependent candidate generation, constraint validation, directional search control, and feedback jointly govern exploration. Structural relay and learning may operate across search episodes.*

**Alt text:** Architecture diagram linking dynamic bucket states, candidate generation, constraint checks, directional scoring, evidence feedback, and relay or learning modules.

**Reader takeaway:** D-BTP is a coupled search framework, not a pipeline in which all candidates are enumerated once and scored afterward.

**Accuracy check:** Show hard feasibility checks as logically distinct from heuristic directional scoring. Do not imply every feedback update is validated RSI.

### Fig-002 — From Static to Dynamic BTP

**Canonical path:** `figures/Fig-002-From-Static-to-Dynamic-BTP.png`  
**Primary insertion:** `docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md`, after the motivation contrasting fixed candidate lists with state-dependent candidate discovery.  
**Secondary references:** D-BTP-001; `docs/cases/CASE-002-Dynamic-Starmap-Similarity.md`.

**Proposed caption:** *Fig-002. From fixed-candidate BTP to dynamic BTP. A static search explores a previously defined candidate universe; dynamic BTP generates additional candidates from the evolving bucket state and observed structural consequences. Both retain explicit branch decisions and feasibility checks.*

**Alt text:** Side-by-side static search tree with a fixed candidate pool and dynamic search tree whose evolving states expose new candidate relationships.

**Reader takeaway:** Dynamic generation changes the discoverable search frontier; it does not by itself establish better accuracy or complexity.

**Accuracy check:** Do not portray baseline BTP as necessarily incapable of dynamic operation in its original conceptual form; the fixed-list formulation is a restricted presentation or baseline variant.

### Fig-003 — Dynamic Bucket State and Candidate Generation

**Canonical path:** `figures/Fig-003-Dynamic-Bucket-State-and-Candidate-Generation.png`  
**Primary insertion:** `docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md`, after the canonical bucket-state definition and before state-transition semantics.  
**Secondary references:** `docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md` and SPEC-002.

**Proposed caption:** *Fig-003. A dynamic bucket carries a hypothesis ledger, structural state, evidence with provenance, directional policy state, and versioned metadata. Candidate generation reads the current state; accept, exclude, and defer decisions produce traceable successor states.*

**Alt text:** Versioned bucket state with five logical compartments feeding a candidate generator and branching into successor buckets, with a feedback arrow.

**Reader takeaway:** A bucket is an auditable hypothesis state, not merely a set of selected pairs.

**Accuracy check:** Distinguish candidate discovery from candidate acceptance; depict provenance and versioning; distinguish quiescence from proven closure.

### Fig-004 — Constraint-Guided Structural Hypothesis Search

**Canonical path:** `figures/Fig-004-Constraint-Guided-Structural-Hypothesis-Search.png`  
**Primary insertion:** `docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md`, after the distinction between hard, soft, and conditional constraints.  
**Secondary references:** `docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md`; CASE-002.

**Proposed caption:** *Fig-004. Constraint-guided structural composition. Candidate hypotheses pass through explicit hard-constraint checks, conditional evaluations, and propagation. Soundly inconsistent branches can be pruned; uncertain or weakly supported branches remain eligible for further investigation.*

**Alt text:** Branching hypothesis tree with constraint plugins, accepted feasible branches, deferred uncertain branches, and provably invalid branches pruned.

**Reader takeaway:** Constraint validation protects feasibility semantics while heuristic scoring guides exploration.

**Accuracy check:** Never label a branch infeasible solely because it received a low directional or weak-evidence score. If a constraint result is unknown, show it as unknown rather than failed.

### Fig-005 — Directional Generation and Selection Coupling

**Canonical path:** `figures/Fig-005-Directional-Generation-and-Selection-Coupling.png`  
**Primary insertion:** `docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md`, immediately after the discussion of the two inseparable dimensions of generation and selection.  
**Secondary references:** D-BTP-006; `docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md`; EXT-002.

**Proposed caption:** *Fig-005. Directional fields couple what is proposed with what is explored next. Directional policies influence candidate generation, branch prioritization, and resource allocation; evaluated outcomes and independently checked evidence feed back into subsequent policy updates.*

**Alt text:** Feedback loop connecting a directional field to candidate generation, hypothesis selection, evidence evaluation, and updated guidance.

**Reader takeaway:** Direction is a structural control influence on both generation and selection, not only a terminal score.

**Accuracy check:** Feedback updates are conditional on evidence quality; the figure should not suggest automatic monotonic improvement.

### Fig-006 — Weak Evidence and Multi-Directional Scoring

**Canonical path:** `figures/Fig-006-Weak-Evidence-and-Multi-Directional-Scoring.png`  
**Primary insertion:** `docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md`, after introducing evidence value for exploration versus evidence strength for proof.  
**Secondary references:** SPEC-003; D-BTP-004; D-BTP-006.

**Proposed caption:** *Fig-006. Weak evidence can contribute to several directional objectives—plausibility, novelty, information gain, cost, and counterevidence potential—without becoming a hard feasibility verdict. Provenance, correlation checks, and competing perspectives constrain how scores are interpreted.*

**Alt text:** Multiple weak-evidence inputs with provenance and uncertainty annotations feeding a multidimensional scoring panel and a diverse search portfolio.

**Reader takeaway:** Weak signals may help allocate attention even when they cannot establish a hypothesis.

**Accuracy check:** Show uncertainty and counterevidence; avoid adding correlated observations as though they were independent confirmations.

### Fig-007 — Blockchain Actor Attribution BTP

**Canonical path:** `figures/Fig-007-Blockchain-Actor-Attribution-BTP.png`  
**Primary insertion:** `docs/cases/CASE-001-Blockchain-Actor-Attribution.md`, after defining the observed-behavior and latent-actor starmaps and before the synthetic example.  
**Secondary references:** D-BTP-003; D-BTP-005; D-BTP-002.

**Proposed caption:** *Fig-007. Illustrative blockchain behavior attribution using D-BTP. Observed transactions and behavioral patterns support competing latent-actor grouping hypotheses, subject to constraints and directional evidence. The inferred units are behavioral actors, not verified real-world identities.*

**Alt text:** Observable blockchain behavior nodes linked by candidate relations to several hypothetical latent actor groups, with constraints and evidence annotations.

**Reader takeaway:** Structural attribution is hypothesis inference under uncertainty, not personal identification.

**Accuracy check:** Label the example synthetic; do not show identifiable people, real wallet addresses, or an unqualified identity-resolution claim. Allow many-to-one behavior-to-actor relations where the model permits them.

### Fig-008 — Recursive Structural Evolution and Collective Learning

**Canonical path:** `figures/Fig-008-Recursive-Structural-Evolution-and-Collective-Learning.png`  
**Primary insertion:** `docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md`, after the introduction of Structural Relay and the controlled learning loop.  
**Secondary references:** D-BTP-008; EXT-002; EXT-003; SPEC-004.

**Proposed caption:** *Fig-008. Multi-agent structural relay and recursive evolution. Competing search agents exchange versioned hypotheses, evidence, and candidate improvements. Independent validation and governance distinguish ordinary adaptation from accepted reusable improvements and from stronger claims of recursive self-improvement.*

**Alt text:** Several hypothesis-search agents exchanging structural units through a relay, with evaluation and versioned policy upgrades feeding subsequent search rounds.

**Reader takeaway:** Collective reuse and improvement are separate claims; validated capability gain must be measured rather than presumed.

**Accuracy check:** Mark the validation gate explicitly; distinguish hypothesis evolution, policy evolution, and operator or representation evolution.

## 4. Recommended placement matrix

Use **one primary insertion per figure** to avoid unnecessary repetition. Secondary manuscripts should normally link to the existing asset with a short contextual sentence rather than duplicating the entire diagram.

| Document | Recommended figure use | Placement rationale |
|---|---|---|
| D-BTP-001 | Fig-001 primary; Fig-002 optional link | Introduce the overall architecture and historical transition |
| D-BTP-002 | Fig-002 and Fig-003 primary | Explain dynamic frontier and bucket semantics |
| D-BTP-003 | Fig-004 primary | Visualize constraints, propagation, and safe pruning |
| D-BTP-004 | Fig-005 primary | Explain coupled directional generation and selection |
| D-BTP-005 | Fig-006 primary | Explain weak-evidence guidance and multiple objectives |
| D-BTP-006 | Fig-005 reference; Fig-001 reference | Integrate the feedback loop without adding duplicate graphics |
| D-BTP-007 | Fig-008 primary | Introduce multi-agent relay and controlled learning |
| D-BTP-008 | Fig-008 reference | Connect open-ended growth with governance and validation |
| SPEC-001 | Fig-003 reference | State model and lifecycle contract |
| SPEC-002 | Fig-004 reference | Generator and constraint-plugin interfaces |
| SPEC-003 | Fig-005 and Fig-006 references | Directional scoring, weak evidence, and search control |
| SPEC-004 | Fig-008 reference | Evidence relay and learning lifecycle |
| CASE-001 | Fig-007 primary | Concrete actor-attribution application |
| CASE-002 | Fig-002 / Fig-003 / Fig-004 references | Baseline comparison and dynamic matching |
| CASE-003 | Fig-008 reference | Competitive hypothesis portfolio |
| EXT-001 | Fig-005 / Fig-006 references | Biomimetic directional exploration |
| EXT-002 | Fig-005 / Fig-008 references | Evolution of directional policies |
| EXT-003 | Fig-008 reference | Open-ended structural relay |

## 5. Markdown embedding examples

For a primary insertion in `docs/foundations/`:

```markdown
![Fig-005. Coupled directional generation, selection, and feedback.](../../figures/Fig-005-Directional-Generation-and-Selection-Coupling.png)

*Fig-005. Directional fields jointly guide candidate generation, branch selection, and resource allocation; evaluated feedback informs later guidance.*
```

For a primary insertion in `docs/cases/`:

```markdown
![Fig-007. Latent actor hypotheses over observable blockchain behavior.](../../figures/Fig-007-Blockchain-Actor-Attribution-BTP.png)

*Fig-007. Synthetic illustration of competing behavioral actor hypotheses; no real-world identity is established.*
```

For an index link from the repository root:

```markdown
[Fig-005 — Directional Generation and Selection Coupling](figures/Fig-005-Directional-Generation-and-Selection-Coupling.png)
```

The relative paths differ between root-level documents and files in `docs/`.

## 6. Figure production

[`1. Fig-001-D-BTP-Grand-Architecture.png`](figures/Fig-001-D-BTP-Grand-Architecture.png)

[`2. Fig-002-From-Static-to-Dynamic-BTP.png`](figures/Fig-002-From-Static-to-Dynamic-BTP.png)

[`3. Fig-003-Dynamic-Bucket-State-and-Candidate-Generation.png`](figures/Fig-003-Dynamic-Bucket-State-and-Candidate-Generation.png)

[`4. Fig-004-Constraint-Guided-Structural-Hypothesis-Search.png`](figures/Fig-004-Constraint-Guided-Structural-Hypothesis-Search.png)

[`5. Fig-005-Directional-Generation-and-Selection-Coupling.png`](figures/Fig-005-Directional-Generation-and-Selection-Coupling.png)

[`5. figures/Fig-006-Weak-Evidence-and-Multi-Directional-Scoring.png`](figures/Fig-006-Weak-Evidence-and-Multi-Directional-Scoring.png)

[`7. figures/Fig-007-Blockchain-Actor-Attribution-BTP.png`](figures/Fig-007-Blockchain-Actor-Attribution-BTP.png)

[`8. Fig-008-Recursive-Structural-Evolution-and-Collective-Learning.png`](figures/Fig-008-Recursive-Structural-Evolution-and-Collective-Learning.png)

## 7. Pre-release figure conformance checklist

- [ ] Eight independent files exist under `figures/` with exact canonical names.
- [ ] All eight images open correctly and have readable labels at normal display size.
- [ ] Fig-001 separates directional guidance from hard constraint validation.
- [ ] Fig-002 distinguishes the static baseline from the broader dynamic BTP conception.
- [ ] Fig-003 includes hypothesis ledger, structural state, evidence, policy, and version metadata.
- [ ] Fig-004 distinguishes provably invalid branches from merely low-priority branches.
- [ ] Fig-005 illustrates the bidirectional coupling of generation, selection, and feedback.
- [ ] Fig-006 includes uncertainty, provenance, and competing evidence.
- [ ] Fig-007 is explicitly synthetic and distinguishes behavioral attribution from personal identity.
- [ ] Fig-008 distinguishes collective learning, self-modification, and validated RSI.
- [ ] All primary manuscript image links and README/START-HERE/CONTENTS links resolve.
- [ ] Every primary figure has a numbered caption and useful alt text.
- [ ] `FIGURE-INDEX.md` accurately reflects the actual published assets.

## 8. Related navigation

- [README](README.md)
- [START-HERE](START-HERE.md)
- [CONTENTS](CONTENTS.md)
- [GLOSSARY](GLOSSARY.md)
- [D-BTP-001 — From Metric Similarity to Structural Hypothesis Search](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md)
- [SPEC-001 — Dynamic Bucket State Contract](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md)
- [CASE-001 — Blockchain Actor Attribution](docs/cases/CASE-001-Blockchain-Actor-Attribution.md)

---

*Research status: conceptual architecture, algorithm specifications, and validation plans. Figures communicate proposed mechanisms and should not be interpreted as proof of experimental performance.*
