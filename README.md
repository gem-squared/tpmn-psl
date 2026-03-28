# TPMN-PSL — Truth-Provenance Markup Notation
## Prompt Specification Language

**Version:** v0.1.5-p | **Status:** Public | **License:** CC-BY 4.0

> *"For complex, high-stakes AI workflows: don't write prompts. Write specifications."*

---

## The Problem

AI outputs claims. Some are grounded in fact. Some are inferred. Some are extrapolated beyond evidence. Some are unknown. **Without a formal way to mark which is which, every AI output requires manual verification — or blind trust.**

TPMN-PSL is a platform-agnostic notation standard that solves this by imposing a formal epistemic structure on AI reasoning: before generation, during generation, and after.

---

## The 5 Symbols

Every non-trivial claim in a TPMN-governed output carries one of five tags:

| Symbol | Name | Meaning |
|--------|------|---------|
| `⊢` | GROUNDED | Directly supported by input or verifiable fact |
| `⊨` | INFERRED | Derived from grounded claims; inference chain visible |
| `⊬` | EXTRAPOLATED | Beyond evidence; basis must be explicitly stated |
| `⊥` | UNKNOWN | Knowledge gap; stops inference chain |
| `?` | SPECULATIVE | Possible but unverified |

**Before TPMN:**
> "This architecture scales well and will handle production load."

**After TPMN:**
> "This architecture has handled 10k RPS in staging ⊢. Production load is estimated at 15k RPS ⊨ (based on Q3 traffic model). It will handle the projected peak ⊬ (no production benchmark exists yet)."

---

## The Three-Phase Protocol

```
Prompt → [P-phase] → LLM → [Inline] → Output → [O-phase] → Trust
```

**P-phase** — Before execution: extract the CONTRACT, establish the A_Priori_Grid, define the computable MANDATE the LLM must satisfy.

**Inline** — During generation: tag every non-trivial claim with its epistemic status as it is written.

**O-phase** — After output: verify the output against the CONTRACT. Gate or pass. Produce O_Record with epistemic_score ∈ [0,1], contract_score ∈ [0,1], and truth_score ∈ [0,100] (integer %).

---

## The Panini Layer

TPMN's notation is built on four layers — but they are **hierarchical, not parallel**:

```
Panini (ontological discretization)   ← defines what can be reasoned about
  └── TLA+  (structure)               ← expresses it formally
  └── Math  (logic)                   ← adds quantifiers and connectives
  └── NL    (commentary)              ← explains in natural language
```

**Panini's role** is to carve the target domain into mutually exclusive, exhaustive, decidable categories *before reasoning begins* — transforming NL ambiguity into a computable MANDATE. This is the bridge from "what the human meant" to "what the LLM can be held to."

---

## Quick Example

```tla
(* P-phase: establish MANDATE *)
CONTRACT ≜ "SummarizeDocument(doc) → Summary | Constraints"

A ≜ [doc: Document]
B ≜ [summary: 𝕊, word_count: ℕ]
P ≜ [
  PRE:  "doc ≠ ⊥ ∧ doc.length > 0",
  POST: "word_count ≤ 200 ∧ summary covers main_claims(doc)",
  INV:  "¬ introduces_claims_not_in(doc, summary)"
]

(* Inline: tag claims during generation *)
"The document argues for distributed consensus ⊢.
 The author's position on CAP theorem is skeptical ⊨ (inferred from §3 framing).
 This may reflect a systems background ⊬ (no biographical data in doc)."

(* O-phase: O_Record *)
O_Record ≜ [
  result:          "PASS",
  epistemic_score: 0.8,
  contract_score:  0.9,
  truth_score:     72,
  violations:      <<>>,
  eef_record: [
    extrapolation: TRUE,
    confidence:    "MEDIUM",
    rules:         [GND: "PASS", EXT: "PASS", UNC: "N/A", SPT: "PASS"],
    spt_violations: <<>>
  ]
]
```

---

## What TPMN Prevents

Three structural inference violations — **Structural Prohibition Taxonomy (SPT)**:

| Pattern | Name | Example |
|---------|------|---------|
| `S→T` | State → Trait | "This model is slow" (current benchmark) → "This model is inherently slow" |
| `L→G` | Local → Global | "Works in our tests" → "Works in all production environments" |
| `Δe→∫de` | Incremental → Mass | One data point → universal claim |

---

## The MANDATE Concept

TPMN's P-phase transforms an NL prompt into a **MANDATE**:

```
NL prompt → MANDATE = CONTRACT + A_Priori_Grid + Panini_Categories
```

A well-formed MANDATE is:
- **Computable** — membership rules are decidable
- **Verifiable** — outputs can be verified against it
- **Traceable** — every claim traces back to a P-phase category
- **Bounded** — scope is explicit; out-of-scope claims require ⊬

Once the MANDATE is established, the LLM operates within it autonomously. The checker verifies against the MANDATE — not against intent.

---

## Extending TPMN-PSL

Any platform or domain can extend the base spec:

```tla
--- MODULE MyDomain_TPMN_PSL ---
EXTENDS TPMN_PSL  (* v0.1.5-p *)

(* Add Tier2 domain glyphs, domain P/O checks, domain SPT patterns *)
(* Preserve: all Tier1 glyphs · P0–P5 · O1–O8 · S→T · L→G · Δe→∫de *)
```

Domain extension template: [`/extensions/template/`](extensions/template/)

---

## Naming Hierarchy

**TPMN** — Truth-Provenance Markup Notation — is an open specification language for structuring and auditing AI reasoning.

**TPMN-PSL** (Prompt Specification Language) is the formal grammar that compiles NL prompts into computable, verifiable specifications (MANDATE).

**TPMN-checker** is a Sovereign AI Service (SAS) — the reference implementation. It runs the TPMN-PSL three-phase pipeline and returns a truth_score for any AI output.

A **SAS** (Sovereign AI Service) is a microservice exclusively owned and controlled by a dedicated AI actor. Each SAS has exactly one sovereign AI — the only entry point through which all access is mediated. Unlike traditional microservices where AI optimizes or consumes, in a SAS the AI *is* the sovereign controller.

---

## Repository Structure

```
tpmn-psl/
├── README.md                          ← this file
├── spec/
│   └── tpmn-psl-v015p.md              ← specification (authoritative)
├── extensions/
│   └── template/
│       └── tpmn-domain-spec-0.1.5-p.md ← domain extension template
├── docs/                              ← GitHub Pages
│   └── index.html
├── CITATION.cff                       ← machine-readable citation
├── CHANGELOG.md
├── CONTRIBUTING.md
└── LICENSE                            ← CC-BY 4.0
```

---

## IP and Architecture Boundary

TPMN-PSL is a **notation specification** — a platform-agnostic standard for epistemic markup. It operates entirely outside LLM internals:

- Does not modify transformer weights, embedding layers, or attention mechanisms
- Treats the LLM as a black box: text in → text out
- Can be implemented on any LLM (Claude, GPT, Gemini, open-source)
- The specification itself is open (CC-BY 4.0)

> Reference implementation: gem2-TPMN-checker (GEM²-AI) · implements TPMN-PSL v0.1.5-p
> Live checker: [tpmn-checker.gemsquared.ai](https://tpmn-checker.gemsquared.ai)

---

## Cite This Work

```bibtex
@software{tpmn_psl_2026,
  title   = {TPMN-PSL: Truth-Provenance Markup Notation — Prompt Specification Language},
  author  = {Seo, Inseok},
  year    = {2026},
  version = {0.1.5-p},
  license = {CC-BY-4.0},
  url     = {https://github.com/gem-squared/tpmn-psl}
}
```

---

## License

This specification is released under [Creative Commons Attribution 4.0 International (CC-BY 4.0)](LICENSE).

You are free to use, implement, extend, and build upon TPMN-PSL in any context — commercial or non-commercial — with attribution.

---

**TPMN-PSL v0.1.5-p · Inseok Seo · CC-BY 4.0 · 2026**
