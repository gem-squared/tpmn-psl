# TPMN-PSL — Open Mathematical Contract Language v0.5.2

## What TPMN-PSL Is

TPMN-PSL is an open mathematical contract language for the operation
and audit of autonomous AI systems. It is not a product, not a
framework, not a library — it is a specification, published under
CC-BY 4.0, that any LLM, any toolchain, and any AI system may implement.

The language has two complementary roles:

- **Operation** — a formal grammar for specifying what an AI system
  should do. Contracts of the form `F := ⟨A, B, P⟩` (read as
  `F: A → B | P` — input domain A, output domain B, constraint P),
  with procedural layers (P-phase pre-flight validation, Inline
  epistemic tagging, O-phase post-flight verification) that compile
  prose intent into executable structure.

- **Audit** — a verification framework for measuring whether what
  the AI system did matches what was specified. Five compilation
  principles — **SIMP** (boundary clarity), **CONS** (edge-transition
  totality), **FALS** (falsifiability), **INCV** (selection incentive),
  **CTRST** (negative contract) — composed into the **SOUND** test.
  Plus the **EEF** epistemic taxonomy (⊢ grounded · ⊨ inferred ·
  ⊬ extrapolated · ⊥ unknown · ? speculative) and the **SPT**
  violation registry (S→T state-to-trait, L→G local-to-global,
  Δe→∫de incremental-to-mass).

## Core Claim

> Under TPMN, an LLM becomes a compiler.

## Tagline

> Don't write prompts. Write specifications.

## Three Pillars

| Pillar    | What It Does                                                              |
|-----------|---------------------------------------------------------------------------|
| Grammar   | Formal syntax for AI instructions (TLA+ / Panini / Math / NL — four-layer notation) |
| Protocol  | Three-phase dual-gate validation (P-phase → Inline → O-phase)             |
| Result    | Evidence-based completion criteria (CONTRACT.B + non-empty ¬B + SOUND audit) |

## Architectural Commitments

TPMN-PSL is grounded in three commitments that distinguish it from
prompt-engineering approaches:

- **Kantian alignment.** Ontological vocabulary (point / line / face)
  names the noumenal — what beings *are*. Topological vocabulary
  (STATE / STATUS / SET) names the phenomenal — how beings *appear*
  in relation. TPMN-PSL apparatus operates on the phenomenal layer
  while remaining committed to the noumenal underneath.

- **GEM² as Riemann approximation.** The framework is a discrete
  projection of continuous reality — ΣΔ space, finite sums of
  discrete units rather than continuous integration. It claims
  provable accuracy *within its discretization*, not against reality.
  TPMN governs CONTRACT satisfaction; it does not govern truth-in-the-world.

- **Control-at-the-edge.** Sovereignty of F: the producer (human
  or AI) is autonomous inside the contract face; judgment happens
  only at the boundary. This is the architectural alternative to
  human-in-the-loop oversight.

## Deposit Contents

This deposit contains three coordinated specification documents:

- **GEM²_core-v052.md** (3.7 KB) — Mathematical foundation.
  5 axioms, 5 lemmas, 3 theorems. Defines the contract space
  `F := ⟨A, B, P⟩`, the bounded local complex face `ℂ_F`, and the
  **Composition Bridge** `G_ij ≜ ⟨B_i, A_j, P_ij⟩` with the
  `ValidHandoff` predicate for verified multi-agent
  contract-to-contract composition.

- **tpmn-psl-v052-p.md** (110.7 KB) — Language specification.
  Four-layer grammar (TLA+ / Panini / Math / NL), philosophical
  foundation (§0.0), geometric ontology (§0.3), the five
  compilation principles (§0.2), four-step compilation process
  (§1.5), CONTRACT archetype (§6), three-phase protocol (§5),
  EEF (§3), SPT (§4), SOUND composite test (§10), Domain
  Extension Protocol (§9).

- **how-to-tpmn-v052.md** (37.0 KB) — Practitioner field manual.
  Four-step compilation process, worked example line-by-line,
  three case studies (software development / prediction /
  communication), four anti-patterns (Domain Smuggling /
  NL Leakage / TLA+ Overreach / Vocabulary Conflation),
  reader paths by role.

## What's New in v0.5.2

- **GEM² Composition Bridge formalized** as its own contract
  `G_ij ≜ ⟨B_i, A_j, P_ij⟩` with the `ValidHandoff` predicate.
  Multi-agent orchestration in GEM² is no longer "shared-context
  collaboration" — it is verified contract-to-contract composition
  through `G_ij`. No agent may enter `F_j` from `F_i` without a
  valid `G_ij`.

- **ℂ disambiguated** as schema for *local* complex spaces `ℂ_F`
  (one per CONTRACT/MANDATE), not a single global plane. Each face
  is its own bounded local complex space.

- **Lemma 2 tightened**: `Geom(F) ⊆ ℂ_F`.

- **Core Consequence collapse term updated**: `a + b𝓲 ∈ ℂ_F`.

## Relationship to Previous Versions

This v0.5.2 release continues the lineage of:

- v1.6.3 (DOI 10.5281/zenodo.18336200, January 26, 2026)
- v1.6.1 (January 22, 2026)

The version numbering has been re-architected: the v1.x line was
the "GEM² Platform Specification" series; v0.5.x is the consolidated
mathematical-axiomatic spec line, where the version number tracks
structural revisions to the axiom set rather than platform releases.

The resource type has also been corrected from "Software" to
"Standard": TPMN-PSL is an open language specification, not an
executable software artifact. Implementations of TPMN-PSL exist
as separate software deposits.

## License

Creative Commons Attribution 4.0 International (CC-BY 4.0).

This is a license change from the v1.x line (CC-BY-NC-SA 4.0).
The change is intentional: an open standard requires permissionless
commercial implementation to achieve adoption. The change does not
affect spec text. Attribution requirements (BY clause) remain
fully enforceable; misattribution and false endorsement claims
are explicitly prohibited under CC-BY 4.0 §3.

## Repository

https://github.com/gem-squared/tpmn-psl

## Appendix — GEM² Defined

**GEM²** = **G**rounded **E**xistence **M**atrix for **G**lobal
**E**ntropy **M**inimum.

GEM² is the mathematical universe in which TPMN-PSL operates.
Each letter is load-bearing:

- **Grounded** — every element has a verifiable basis;
  nothing enters the system ungrounded.
- **Existence** — what can be reasoned about within the system,
  governed by the contract space `F := ⟨A, B, P⟩`.
- **Matrix** — the structured space of contracts and the
  bridges between them.
- **Global** — across all MANDATEs and compositions, not local
  to a single inference.
- **Entropy** — disorder, undefined inference paths
  (Graph(f) ⊄ F).
- **Minimum** — bounded by P, audited by SOUND;
  computability requires Graph(f) ⊆ F.

### Primitive Ontology

```
x      : invariant      (observable algebraic entity)
{x}    : transformation (trajectory / relation over x)
ℂ      : schema for local complex spaces ℂ_F
         (one per CONTRACT/MANDATE F, not a single global plane)
```

### The GEM² Universe

```
𝒰_GEM² = ( {F_i}, {G_ij} )
```

A GEM² universe consists of contract spaces `{F_i}` linked by
verified composition bridges `{G_ij}`. There is no shared global
context — only contracts and the explicit bridges between them.

### The Collapse Identity

The elegance of GEM² is that ontology, relation, and geometry
share a single unified structure:

```
{x, {x}, ℂ}  ⇔  ⟨A, B, P⟩  ⇔  (a, b)  ⇔  a + b𝓲 ∈ ℂ_F
```

The same object viewed four ways — primitive ontology, contract,
admissible pair, point in bounded local complex space.

### One-Line Core

> GEM² approximates reality via invariant-preserving
> transformations within bounded contract-defined complex spaces.

## Citation

GEM Squared, Inc. (2026). *TPMN-PSL — Open Mathematical Contract Language for Autonomous AI Operation and Audit* (v0.5.2) [Standard]. Zenodo. https://doi.org/10.5281/zenodo.20079202
