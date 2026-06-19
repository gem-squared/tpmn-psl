# GEM² — Core Document (Axiom → Lemma → Theorem)

**Version:** v0.5.2
**Author:** Inseok Seo / GEM Squared Inc.

---

## Version Log

- **v0.5.2** — Added GEM² Composition Bridge (formalizes G_ij as its own contract ⟨B_i, A_j, P_ij⟩; adds ValidHandoff and the orchestration rule for multi-agent TPMN-PSL support).
- **v0.5.1** — Disambiguated ℂ as schema for local complex spaces (ℂ_F), not a single global plane. Tightened Lemma 2 (Geom(F) ⊆ ℂ_F). Updated Core Consequence collapse term to a + b𝓲 ∈ ℂ_F.
- **v0.5.0** — Initial axiomatic formulation.

---

## 0. Primitive Ontology

x      : invariant (observable algebraic entity)
{x}    : transformation (trajectory / relation over x)
ℂ : schema for local complex spaces (ℂ_F), not a single global plane

---

## Axiom 1 — Discrete Projection

Real-world phenomena are projected into a discrete mathematical system:

Reality → {x, {x}, ℂ}

---

## Axiom 2 — Contextual Meaning

An observable is defined as:

ι(p, F)

and is only meaningful within a space (F).

---

## Axiom 3 — Bounded Complex Face

Each F is represented as a bounded local complex face, not as an extensible global complex plane.

ℂ_F is bounded by P.

---

## Axiom 4 — Contractual Space

F := ⟨A, B, P⟩

A: antecedent type
B: consequent type
P: constraint

---

## Axiom 5 — Non-Empty Contract

F := ⟨A, B, P⟩ must satisfy:
∃ (a, b) ∈ A × B such that P(a,b)

---

## Lemma 1 — Space as Admissible Relation

F = { (a, b) | a : A, b : B, P(a,b) }

---

## Lemma 2 — Geometry from Relation

Geom(F) ⊆ ℂ_F

Geom(F) = { a + b𝓲 ∈ ℂ_F | (a,b) ∈ F }

---

## Lemma 3 — Inference as Path Constraint

f : A → B

Graph(f) ⊆ F

---

## Lemma 4 — Boundary Defines Computability

Graph(f) ⊄ F ⇒ boundary violation

---

## Lemma 5 — Composition via Transformation

Connect(F₁, F₂) ⇔ ∃ G : B₁ → A₂

---

(* ═══ GEM² Composition Bridge ═══ *)

G_ij ≜ ⟨B_i, A_j, P_ij⟩

where:
  B_i = output type of predecessor contract F_i
  A_j = input type of successor contract F_j
  P_ij = bridge constraint governing admissible transfer

Connect(F_i, F_j) ⇔ ∃ G_ij : B_i → A_j

ValidHandoff(F_i, F_j, G_ij) ⇔
  ∃ b_i ∈ B_i, a_j ∈ A_j :
    (a_i, b_i) ∈ F_i
    ∧ (b_i, a_j) ∈ G_ij
    ∧ P_ij(b_i, a_j)

Rule:
  No agent may enter F_j from F_i without a valid G_ij.

Multi-agent orchestration in GEM² is not shared-context collaboration;
it is verified contract-to-contract composition through G_ij.

---

## Theorem — GEM² Structure

𝒰_GEM² = ( {F_i}, {G_ij} )

---

## Theorem — Computable Inference

f : A → B subject to P
Graph(f) ⊆ F

---

## Theorem — Separation of Judgment

Graph(f) ⊄ F ⇒ boundary violation
Epistemic judgment is external

---

## Core Identity

x      → invariant
{x}    → transformation
ℂ      → bounded contract space

F := ⟨A, B, P⟩
Geom(F) = A + B𝓲

Inference = constrained path inside F

---

## Core Consequence — Elegance

T(F) = Geom(F)

where:

F := ⟨A, B, P⟩
Geom(F) = A + B𝓲 subject to P


GEM² reduces:

- noumenon → ontology → {x, {x}, ℂ}
- phenomenon → topology → invariant, transformation, space
- inference → admissible relation over A × B
- geometry → complex plane representation (A + B𝓲)
- computation → bounded by P


Elegance arises because all layers collapse into a single structure:

{x, {x}, ℂ}
⇔ ⟨A, B, P⟩
⇔ (a, b)
⇔ a + b𝓲 ∈ ℂ_F

Thus, ontology, relation, and geometry share a single unified structure.
---

## One-line Core

GEM² approximates reality via invariant-preserving transformations within bounded contract-defined complex spaces.