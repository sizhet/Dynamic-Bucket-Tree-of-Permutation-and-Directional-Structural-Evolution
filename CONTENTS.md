# CONTENTS — Dynamic Bucket Tree of Permutation (D-BTP)

**Project:** Dynamic Bucket Tree of Permutation: Directional Structural Generation and Hypothesis Evolution  
**Repository:** `Dynamic-Bucket-Tree-of-Permutation-and-Directional-Structural-Evolution`  
**Document role:** Canonical navigation, reading order, and cross-reference index  
**Research status:** Proposed framework, formal contracts, and illustrative cases; empirical claims require validation  
**Release track:** v1.0.0 (pre-release preparation)

> **Central proposition:** D-BTP treats structural matching and attribution as dynamic, constraint-guided hypothesis search. Candidate generation, directional selection, and feedback are coupled, while evidence quality and hard feasibility remain logically distinct.

## 1. Start here

| Resource | Purpose |
|---|---|
| [README.md](README.md) | Project overview, contributions, scope, and repository map |
| [START-HERE.md](START-HERE.md) | Entry points tailored to different research interests |
| **CONTENTS.md** | Complete document index, dependency map, and reading routes |
| [GLOSSARY.md](GLOSSARY.md) | Terminology and abbreviations (planned publication asset) |
| [FIGURE-INDEX.md](FIGURE-INDEX.md) | Figure captions and placement guide (planned publication asset) |
| [FUTURE-DIRECTIONS.md](FUTURE-DIRECTIONS.md) | Research extensions and priorities (planned publication asset) |
| [OPEN-QUESTIONS.md](OPEN-QUESTIONS.md) | Unresolved theoretical and engineering questions (planned publication asset) |
| [TESTABLE-HYPOTHESES.md](TESTABLE-HYPOTHESES.md) | Falsifiable hypotheses and proposed baselines (planned publication asset) |
| [VALIDATION-ROADMAP.md](VALIDATION-ROADMAP.md) | Staged experimental and conformance plan (planned publication asset) |

*Links marked “planned publication asset” describe the agreed repository structure; the corresponding files should be added before public release.*

## 2. Foundations — eight research papers

These papers build the conceptual and mathematical framework in dependency order.

| ID | Document | Main contribution |
|---|---|---|
| D-BTP-001 | [From Metric Similarity to Structural Hypothesis Search](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md) | Generalizes the original BTP structural similarity problem into constrained hypothesis composition |
| D-BTP-002 | [Dynamic Bucket States and Candidate Generation](docs/foundations/D-BTP-002-Dynamic-Bucket-States-and-Candidate-Generation.md) | Defines evolving bucket states, state-driven candidates, transitions, and search termination |
| D-BTP-003 | [Constraint-Guided Structural Composition](docs/foundations/D-BTP-003-Constraint-Guided-Structural-Composition.md) | Separates hard constraints, conditional feasibility, soft guidance, and sound pruning |
| D-BTP-004 | [Directional Fields for Generation and Selection](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md) | Couples what to generate with what to prioritize under multi-objective directional control |
| D-BTP-005 | [Weak Evidence and Directional Exploration](docs/foundations/D-BTP-005-Weak-Evidence-and-Directional-Exploration.md) | Studies how uncertain evidence can guide exploration without becoming proof |
| D-BTP-006 | [Coupled Generation, Selection and Feedback](docs/foundations/D-BTP-006-Coupled-Generation-Selection-and-Feedback.md) | Integrates state evolution, directional policy, evidence feedback, and governance |
| D-BTP-007 | [Multi-Agent RSI and Collective Structural Learning](docs/foundations/D-BTP-007-Multi-Agent-RSI-and-Collective-Structural-Learning.md) | Introduces competing agents, hypothesis relay, shared learning, and validated improvement |
| D-BTP-008 | [Open-Ended Structural Evolution and Intelligence](docs/foundations/D-BTP-008-Open-Ended-Structural-Evolution-and-Intelligence.md) | Distinguishes adaptive search from changes to representations, operators, and open-ended growth |

**Core reading sequence:** D-BTP-001 → 002 → 003 → 004 → 005 → 006 → 007 → 008.

## 3. Specifications — four implementation contracts

Specifications translate the research framework into interoperable and testable semantics. They are design contracts, **not claims of a completed reference implementation**.

| ID | Document | Contract focus |
|---|---|---|
| SPEC-001 | [Dynamic Bucket State Contract](docs/specifications/SPEC-001-Dynamic-Bucket-State-Contract.md) | Canonical state, hypothesis ledger, invariants, transitions, provenance, versioning |
| SPEC-002 | [Candidate Generation and Constraint Plugins](docs/specifications/SPEC-002-Candidate-Generation-and-Constraint-Plugins.md) | Generator interfaces, plugin results, constraint propagation, safe rejection |
| SPEC-003 | [Directional Scoring and Search Control](docs/specifications/SPEC-003-Directional-Scoring-and-Search-Control.md) | Directional field units, multi-objective scores, search budgets, diversity, policy updates |
| SPEC-004 | [Evidence Relay and Learning Lifecycle](docs/specifications/SPEC-004-Evidence-Relay-and-Learning-Lifecycle.md) | Evidence provenance, relay envelopes, learning lifecycle, conformance and rollback |

**Recommended implementation order:** SPEC-001 → SPEC-002 → SPEC-003 → SPEC-004. Establish state and plugin conformance before enabling adaptive policies or cross-agent relay.

## 4. Cases — three illustrative applications

| ID | Document | Research question |
|---|---|---|
| CASE-001 | [Blockchain Actor Attribution](docs/cases/CASE-001-Blockchain-Actor-Attribution.md) | Can latent behavioral actors be inferred from observed transaction structures without confusing behavior attribution with real-world identity? |
| CASE-002 | [Dynamic Starmap Similarity](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md) | When does state-driven candidate discovery improve on a fixed-candidate BTP baseline? |
| CASE-003 | [Multi-Agent Hypothesis Competition](docs/cases/CASE-003-Multi-Agent-Hypothesis-Competition.md) | Can competing hypothesis portfolios and counterevidence agents improve calibrated search outcomes after accounting for coordination costs? |

The cases are **research designs and synthetic illustrations**, not field-validated forensic conclusions or performance benchmarks.

## 5. Extensions — three forward-looking papers

| ID | Document | Extension focus |
|---|---|---|
| EXT-001 | [Biomimetic Directional Intelligence](docs/extensions/EXT-001-Biomimetic-Directional-Intelligence.md) | Functional analogies with active sensing, purposeful exploration, and biological adaptive search |
| EXT-002 | [Recursive Directional Field Evolution](docs/extensions/EXT-002-Recursive-Directional-Field-Evolution.md) | Makes directional policies themselves objects of search, validation, versioning, and rollback |
| EXT-003 | [Open-Ended BTP and Structural Relay](docs/extensions/EXT-003-Open-Ended-BTP-and-Structural-Relay.md) | Explores growth in representations, operators, and transferable structural capabilities |

**Epistemic boundary:** Biomimetic analogy does not establish that brains execute BTP. Self-modification is not automatically validated recursive self-improvement (RSI). Open-ended evolution remains a research hypothesis.

## 6. Figures — planned eight-file index

| Figure | Planned file | Recommended reading context |
|---|---|---|
| Fig-001 | `figures/Fig-001-D-BTP-Grand-Architecture.png` | README, D-BTP-001, D-BTP-008 |
| Fig-002 | `figures/Fig-002-From-Static-to-Dynamic-BTP.png` | D-BTP-001, D-BTP-002, CASE-002 |
| Fig-003 | `figures/Fig-003-Dynamic-Bucket-State-and-Candidate-Generation.png` | D-BTP-002, SPEC-001, SPEC-002 |
| Fig-004 | `figures/Fig-004-Constraint-Guided-Structural-Hypothesis-Search.png` | D-BTP-003, SPEC-002 |
| Fig-005 | `figures/Fig-005-Directional-Generation-and-Selection-Coupling.png` | D-BTP-004, D-BTP-006, SPEC-003 |
| Fig-006 | `figures/Fig-006-Weak-Evidence-and-Multi-Directional-Scoring.png` | D-BTP-005, SPEC-003, SPEC-004 |
| Fig-007 | `figures/Fig-007-Blockchain-Actor-Attribution-BTP.png` | CASE-001 |
| Fig-008 | `figures/Fig-008-Recursive-Structural-Evolution-and-Collective-Learning.png` | D-BTP-007, D-BTP-008, EXT-002, EXT-003 |

**Publication check:** The current artwork was initially generated as one eight-panel composite. The eight independent image paths above are *planned outputs*, not verified separate assets. Export, inspect, and save each panel under its exact filename before publishing these image links. The illustration is explanatory, not experimental evidence.

## 7. Publication and metadata assets

| Asset | Intended use | Status in preparation |
|---|---|---|
| [CHANGELOG.md](CHANGELOG.md) | Versioned research changes | Planned |
| [CITATION.cff](CITATION.cff) | GitHub citation metadata | Planned |
| [.zenodo.json](.zenodo.json) | Zenodo deposit metadata | Planned |
| [LICENSE](LICENSE) | Apache-2.0 license text | Planned |
| [GitHub-Release-Notes-v1.0.0.md](publication/GitHub-Release-Notes-v1.0.0.md) | GitHub release description | Planned |
| [ResearchGate-Description.txt](publication/ResearchGate-Description.txt) | Plain-text project description | Planned |
| [D-BTP-v1.0.0-ResearchGate-Overview.pdf](publication/D-BTP-v1.0.0-ResearchGate-Overview.pdf) | One-page research overview | Planned |

No DOI is asserted here. Add a verified DOI and finalized release tag only after deposit and publication.

## 8. Cross-reference map by research mechanism

| Mechanism | Foundation | Specification | Case / extension |
|---|---|---|---|
| Dynamic bucket and state transitions | D-BTP-002 | SPEC-001 | CASE-002 |
| Constraint-guided composition | D-BTP-003 | SPEC-002 | CASE-001, CASE-002 |
| Directional generation and selection | D-BTP-004, D-BTP-006 | SPEC-003 | CASE-002, EXT-002 |
| Weak evidence and counterevidence | D-BTP-005 | SPEC-003, SPEC-004 | CASE-001, CASE-003 |
| Multi-agent competition and relay | D-BTP-007 | SPEC-004 | CASE-003, EXT-003 |
| Open-ended structural evolution | D-BTP-008 | SPEC-003, SPEC-004 | EXT-001, EXT-002, EXT-003 |

## 9. Suggested reading routes

### Route A — A 20-minute conceptual introduction

1. [README](README.md): problem statement and architecture.
2. [D-BTP-001](docs/foundations/D-BTP-001-From-Metric-Similarity-to-Structural-Hypothesis-Search.md): why the original BTP formulation generalizes.
3. [D-BTP-004](docs/foundations/D-BTP-004-Directional-Fields-for-Generation-and-Selection.md): why generation and selection are coupled.
4. [CASE-002](docs/cases/CASE-002-Dynamic-Starmap-Similarity.md): a familiar structural matching example.

### Route B — Algorithm design and conformance

D-BTP-002 → D-BTP-003 → D-BTP-006 → SPEC-001 → SPEC-002 → SPEC-003 → SPEC-004. Prioritize transition invariants, sound pruning, reproducible search traces, and the distinction between quiescence and budget exhaustion.

### Route C — Directional weak evidence

D-BTP-004 → D-BTP-005 → SPEC-003 → SPEC-004 → CASE-001. Examine evidence provenance, correlation, counterevidence, confidence calibration, and the difference between search priority and factual validity.

### Route D — Collective learning and RSI

D-BTP-007 → D-BTP-008 → CASE-003 → EXT-002 → EXT-003. Separate hypothesis search, adaptive policy tuning, validated policy improvement, and the stronger claim of open-ended growth.

### Route E — Application evaluation

CASE-002 → CASE-001 → CASE-003 → TESTABLE-HYPOTHESES → VALIDATION-ROADMAP (the last two are planned assets). Compare against static BTP, unguided dynamic search, fixed directional policies, and adaptive directional policies with equal compute budgets.

## 10. Repository structure

```text
Dynamic-Bucket-Tree-of-Permutation-and-Directional-Structural-Evolution/
├── README.md
├── START-HERE.md
├── CONTENTS.md
├── GLOSSARY.md
├── FIGURE-INDEX.md
├── FUTURE-DIRECTIONS.md
├── OPEN-QUESTIONS.md
├── TESTABLE-HYPOTHESES.md
├── VALIDATION-ROADMAP.md
├── CHANGELOG.md
├── CITATION.cff
├── .zenodo.json
├── LICENSE
├── docs/
│   ├── foundations/       # D-BTP-001 ... D-BTP-008
│   ├── specifications/    # SPEC-001 ... SPEC-004
│   ├── cases/             # CASE-001 ... CASE-003
│   └── extensions/        # EXT-001 ... EXT-003
├── figures/               # Fig-001 ... Fig-008 (independent PNGs)
└── publication/
    ├── GitHub-Release-Notes-v1.0.0.md
    ├── ResearchGate-Description.txt
    └── D-BTP-v1.0.0-ResearchGate-Overview.pdf
```

The source Markdown files should be placed in the directories indicated above. Relative links in this index assume that repository layout.

## 11. Validation and responsible-use notes

- **Soundness before speed:** A heuristic directional score cannot by itself establish a hard contradiction or justify a completeness claim.
- **Dynamic search is not necessarily better:** Fixed-candidate baselines may win when candidate sets are complete and inexpensive to enumerate.
- **No free completeness:** Conditional completeness depends on candidate coverage, valid pruning, search scheduling, and available budgets.
- **Weak evidence is not proof:** Correlated signals, provenance defects, and selection bias require explicit controls.
- **Attribution is not identification:** A behavioral cluster or latent actor hypothesis does not establish a real-world person's identity.
- **Collective learning is not validated RSI:** Improvements must be independently measured against fixed baselines and checked for regression.
- **Open-ended growth is an experimental question:** New representations and operators must demonstrate useful, transferable, validated capabilities.

## 12. Contribution and maintenance conventions

1. Preserve stable document IDs and filenames; update the index when adding or renaming a paper.
2. Keep specification contracts aligned with foundations and cases. Record any breaking contract change in the changelog.
3. Distinguish formal guarantees, design assumptions, illustrative examples, and empirical findings.
4. Keep unresolved counterexamples and negative results visible rather than silently removing them.
5. Verify that all relative links resolve after assembling the repository, especially figures and publication assets.
6. Prefer reproducible synthetic benchmarks and privacy-respecting evidence handling for attribution experiments.
7. Follow the guiding workflow: **Specifications / Contracts First; Conformance Before Runtime**.

---

**Research orientation:** Open, testable, and collective-learning-friendly. This index is a navigation document, not an assertion that all proposed mechanisms have been implemented or validated.
