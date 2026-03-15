# CHANGELOG — TPMN-PSL

All versions follow semantic versioning. Breaking changes increment the minor version.
Patch versions are additive or corrective only.

---

## v0.1.5-p — 2026-03-16

**Public reference implementation specification. Three-mode workflow, response contracts, conformance levels.**

### Added
- **REF-1:** Three-mode workflow formalized: `strict` (diagnose only), `refine` (compose + re-verify), `interpolate` (diagnose + search suggestions)
- **REF-2:** Response contracts typed as JSON-serializable records: `TruthReport`, `PReport`, `OReport`, `ComposedOutput`, `SearchSuggestion`, `Consensus`
- **REF-3:** Consensus algorithm formalized — majority-vote over `≥2` providers
- **REF-4:** Calibration interface defined — `μ=1` default (public), SAS hook declared
- **REF-5:** Three conformance levels: L1 (minimal), L2 (full), L3 (calibrated, SAS-only)
- **REF-6:** Public / SAS boundary explicitly fenced (§R6)
- **REF-7:** Composer semantics formalized — overclaim stripping rules CR1–CR6
- `CheckerInput` standard input record for all checker endpoints
- `CheckResult`, `TPMNExtraction`, `EEFFlag`, `SPTIssue` typed records
- Conformance verification procedure (§R9) with L1/L2/L3 test requirements
- Implementation guidance (§R8) — non-normative advisory for defensive parsing, error handling, multi-provider patterns
- Weight interface contract (sum=1, positive, documented)
- Verdict derivation reference thresholds (PASS ≥ 0.8, WARN ≥ 0.5, FAIL < 0.5)

### Backward compatibility
- Fully compatible with v0.1.4 — no base definitions changed
- This is a reference implementation appendix (`-p` suffix), not a protocol change
- Implementations of v0.1.4 are valid L0 (spec-only, no checker)

---

## v0.1.4 — 2026-03-15

**14 fixes: truth_score split, P_Record/O_Record formally defined, SPT_Check rewritten, tagline scoped.**

### Changed
- **FIX-6:** `drift_model.tpmn_response` retagged `⊢` → `⊨` (design hypothesis, not established fact)
- **FIX-7:** `set_contract` reframed as normative design requirement (not universal guarantee)
- **FIX-8:** `SPT_Check` rewritten — circularity removed; now uses `SPT_Signals` → `SPT_Classify` → `SPT_Check` pipeline
- **FIX-9:** P-phase gains explicit failure semantics `{PASS | FAIL | CONDITIONAL}` with `failure_policy`
- **FIX-10:** `A_Priori_Grid` immutability clarified with restart/recompile rule (immutable per execution instance)
- **FIX-11:** `EEF_Record.spt_violations` typed `Seq(𝕊)` · `NoViolations ≜ <<>>` (never `⊥` or `null`)
- **FIX-12:** `truth_score` split into `epistemic_score` (Real ∈ [0,1]) + `contract_score` (Real ∈ [0,1])
- **FIX-13:** `Metric` type defined, distinguished from `Constraint`
- **FIX-14:** MANDATE wording "provable" → "verifiable"
- **FIX-15:** Tagline scope narrowed to "complex, high-stakes AI workflows"
- **FIX-16:** §7 Kantian mapping labeled heuristic framing, not structural proof
- **FIX-17:** `truth_score` defined as composite heuristic % ∈ [0,100] · formula: `round(min(100, e·c·μ·100))` · `modification_factor μ = 1` in PSL base (identity) · `μ` calibrated by SAS similarity query at runtime
- **FIX-18:** `O_Record` and `P_Record` formally defined with typed fields
- **FIX-19:** `SPT_Check` release note L→G violation corrected

### Added
- `EpistemicScore` and `ContractScore` type definitions (§3)
- `TruthScorePercent` type and `TruthScorePolicy` (§3)
- `P_Record` type definition (§5.1)
- `O_Record` type definition with `epistemic_score`, `contract_score`, `truth_score` fields (§5.3)
- `O_Record_Rules` R1–R8 (§5.3)
- `Metric` type definition (§6)
- `modification_factor` glossary entry (§10)
- Format rules V5–V7 and prohibition N6 for integer truth_score output (§8)

### Backward compatibility
- **Breaking:** `truth_score` format changed from Real [0,1] to integer [0,100]. Implementations reading old `truth_score` Real values must update to read integer percent.
- **Breaking:** `spt_violations` changed from nullable (`⊥`/`null`) to `Seq(𝕊)` with empty = `<<>>`. Consumers checking for `null`/`⊥` must update to check for `<<>>`.
- `epistemic_score` and `contract_score` are new component fields in `O_Record`.
- `P_Record` is a new structured output type for P-phase.

---

## v0.1.2 — 2026-03-13

**Panini layer elevated. A_Priori_Grid extended. Glossary completed.**

### Changed
- **§1.2 Panini Adaptation** — Primary function redefined from "compact notation" to **ontological discretization layer**. Panini now formally defines the SET structure of the target domain before reasoning begins, using `set_contract` (mutual_exclusion, exhaustion, decidability). Secondary notation functions preserved and demoted.
- **§5.1 A_Priori_Grid** — Added optional `? categories: Seq(PaniniCategory)` field. Backward compatible with v0.1.0 and v0.1.1 implementations.
- **§5.3 O-Phase** — Added conditional `O8: Category integrity` check. Fires only when `A_Priori_Grid.categories` is populated. Verifies no claim crossed a Panini category boundary without `⊬` escalation.
- **§7 KantianMapping.A_Priori** — Added `mechanism` field: `Panini_Categories ⊂ A_Priori` — names Panini as the operative discretization mechanism.
- **§9 Extension Protocol** — Added `E7`: extensions using Panini discretization must define P6 and populate `A_Priori_Grid.categories`. Added `recommended_p6` definition.
- **§10 Glossary** — Added four new entries: `Panini_Categories`, `ontological_discretization`, `set_contract`, `MANDATE`. Updated `A_Priori_Grid` entry to reference optional `categories` field.
- **§11 Summary** — `grammar` field now describes the four-layer hierarchy as hierarchical not parallel. Added `mandate` field: the core transformation TPMN performs.
- **§3 EEF** — Added `evolution` field documenting origin (boolean Explicit Extrapolation Flag) and evolution to five-tag taxonomy.

### Added
- `PaniniCategory` type definition in §5.1
- `MANDATE` formally defined in §10 Glossary

### Backward compatibility
All v0.1.0 and v0.1.1 implementations remain valid. The `categories` field in `A_Priori_Grid` is optional. O8 is conditional. P6 is a recommended extension check, not a base spec requirement.

---

## v0.1.1 — 2026-03-13

**Initial public draft with §1.2 Panini revision integrated.**

### Changed
- **§1.2 Panini Adaptation** — Introduced ontological discretization as primary function (intermediate version, superseded by v0.1.2)
- **§0 Overview** — Version bumped to v0.1.1

---

## v0.1.0 — 2026-03-12

**Initial public release.**

### Added
- §1 Grammar: TLA+ Conventions, Panini Adaptation (compact grammar), Math Notation, NL Rules
- §2 Symbol Governance: Tier1 fixed glyphs (⊢ ⊨ ⊬ ⊥ ?), Tier2 extensible
- §3 EEF: Epistemic Evidence Framework, TagRules R1–R4, EEF_Record, ConfidenceCalibration
- §4 SPT: Structural Prohibition Taxonomy (S→T, L→G, Δe→∫de)
- §5 Three-Phase Protocol: P-Phase (P0–P5), Inline Phase, O-Phase (O1–O7), A_Priori_Grid
- §6 CONTRACT archetype: In → Out | Constraints
- §7 Philosophical Foundation: KantianMapping, ResponsibilityBoundary
- §8 Format Rules: V1–V5, N1–N5
- §9 Extension Protocol: E1–E6
- §10 Glossary
- §11 Summary

---

## Versioning Policy

- `0.x.y` — pre-stable. Minor (x) = structural changes. Patch (y) = additive or corrective.
- `1.0.0` — stable release. Requires: public community review, reference implementation verification, at least one published domain extension.
- Breaking changes in `0.x` series are permitted with explicit backward-compat notes.
