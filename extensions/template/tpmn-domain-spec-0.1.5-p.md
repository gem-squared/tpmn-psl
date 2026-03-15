# TPMN-PSL Domain Extension Specification
# [DOMAIN NAME] — Truth-Provenance Markup Notation

**Version:** v0.1.0-draft
**Base:** TPMN-PSL v0.1.5-p
**Status:** Draft · Community Contribution
**Domain:** [DOMAIN — e.g. Medical / Legal / SDLC / Research / Finance]
**Updated:** YYYY-MM-DD
**Maintainer:** [Name / Organization]

---

```tla
--- MODULE [DOMAIN]_TPMN_PSL ---

EXTENDS TPMN_PSL  (* v0.1.5-p *)

(*
  Domain Extension: [DOMAIN NAME]
  Purpose: [One sentence — what epistemic problems does this domain face that
            the base spec does not cover?]
  Scope:   [What content types, workflows, or actors does this extension govern?]
*)

(* ═══ §0. EXTENSION OVERVIEW ═══ *)

Extension_Overview ≜ [
  name:        "[DOMAIN]_TPMN_PSL",
  version:     "v0.1.0-draft",
  base:        "TPMN_PSL v0.1.5-p",
  domain:      "[DOMAIN]",
  purpose:     "[What epistemic reliability problem does this domain extension solve?]",
  extends:     {
    "Tier2 domain-specific epistemic glyphs",
    "Domain P-phase checks (P6+)",
    "Domain O-phase checks (O9+)",
    "Domain SPT violations",
    "Domain CONTRACT archetypes"
  },
  preserves:   {
    "All Tier1 glyphs (⊢ ⊨ ⊬ ⊥ ?)",
    "P0–P5 base checks",
    "O1–O8 base checks",
    "EEF_Record structure",
    "SPT base violations (S→T, L→G, Δe→∫de)",
    "Response contracts (TruthReport, PReport, OReport)"
  }
]


(* ═══ §1. DOMAIN CONTEXT ═══ *)

(*
  Describe WHY this domain requires its own epistemic rules.
  What makes a claim "grounded" in this domain?
  What types of extrapolation are especially dangerous here?
*)

Domain_Context ≜ [
  epistemic_environment: "[e.g. peer-reviewed evidence hierarchy / legal precedent /
                           code specification / financial regulation]",
  grounding_sources:     {
    "[Primary source type — e.g. RCT evidence / statute / spec document / audit trail]",
    "[Secondary source type]",
    "[...]"
  },
  high_risk_extrapolations: {
    "[Domain-specific extrapolation that causes real harm — e.g. off-label dosing from
      general pharmacology / applying case law across jurisdictions]"
  },
  claim_types:           {
    "[Claim type 1 — e.g. diagnostic / prognostic / causal]",
    "[Claim type 2]",
    "[...]"
  }
]


(* ═══ §2. TIER2 DOMAIN GLYPHS ═══ *)

(*
  Define domain-specific epistemic symbols here.
  MUST NOT conflict with Tier1: ⊢ ⊨ ⊬ ⊥ ?
  Each glyph MUST have: symbol, name, meaning, usage rule.
*)

Tier2_Domain_Glyphs ≜ [

  (* Example — replace or extend as needed *)

  (* --- SDLC domain examples --- *)
  (* "✓s": "SPEC-GROUNDED — claim directly traceable to a written specification",  *)
  (* "⚙":  "IMPLEMENTATION-INFERRED — derived from observed system behavior",       *)
  (* "Δ":  "STATE-CHANGE — claim about a mutable system state at a point in time",  *)

  (* --- Medical domain examples --- *)
  (* "⊢rct": "RCT-GROUNDED — supported by randomized controlled trial evidence",    *)
  (* "⊨obs": "OBSERVATIONAL-INFERRED — derived from cohort or case-control study",  *)
  (* "⊬off": "OFF-LABEL — extrapolation beyond approved indication",                *)

  (* --- Legal domain examples --- *)
  (* "⊢jx":  "JURISDICTION-GROUNDED — directly supported by applicable statute",    *)
  (* "⊨ana": "ANALOGICAL-INFERRED — derived by case analogy",                       *)
  (* "⊬cj":  "CROSS-JURISDICTION — extrapolated across legal boundaries",           *)

  (* --- Research domain examples --- *)
  (* "⊢rep": "REPLICATED — finding reproduced across ≥2 independent studies",       *)
  (* "⊨meta":"META-INFERRED — derived from systematic review or meta-analysis",     *)
  (* "⊬gen": "GENERALIZATION — extrapolated beyond study population",               *)

  (* --- Finance domain examples --- *)
  (* "⊢reg": "REGULATORY-GROUNDED — directly stated in applicable regulation",      *)
  (* "⊨mdl": "MODEL-INFERRED — derived from validated financial model",             *)
  (* "⊬pro": "PROJECTION — extrapolated from historical data to future state",      *)

  placeholder: "Replace this block with domain-specific Tier2 glyph definitions"

]


(* ═══ §3. DOMAIN P-PHASE EXTENSIONS ═══ *)

(*
  Add domain-specific pre-flight checks (P6 onward).
  P0–P5 from base spec are preserved and MUST still run.
  P6 in base spec: Categories defined — apply when Panini discretization is used.
  Extensions begin domain-specific checks at P6 if not using Panini, otherwise P7.
*)

Domain_P_Checks ≜ [

  P6: "Categories defined (if domain is bounded) — has domain D been carved into
       mutually exclusive, exhaustive, decidable sets S₁...Sₙ? (Panini set_contract)",
  P7: "[Domain check — e.g. Evidence tier declared: is the evidence quality level stated?]",
  P8: "[Domain check — e.g. Jurisdiction scoped: is the applicable jurisdiction explicit?]"

  (* Add as many as the domain requires *)

]

Domain_P_Rationale ≜ [
  P6: "Ontological discretization (Panini) — required when domain has bounded, classifiable content",
  P7: "[Why is this check necessary in this domain?]",
  P8: "[Why is this check necessary in this domain?]"
]


(* ═══ §4. DOMAIN O-PHASE EXTENSIONS ═══ *)

(*
  Add domain-specific post-flight verification checks (O9 onward).
  O1–O8 from base spec are preserved and MUST still run.

  Base spec O8 (DO NOT redefine here):
    O8: Category integrity (conditional) — verify no claim crossed a Panini
        category boundary without ⊬ escalation. SKIP if no category structure
        was defined in P-phase.

  Domain extensions begin at O9.

  O_Record (from §R3 of v0.1.5-p) includes:
    epistemic_score:  Real ∈ [0,1] — grounding quality
    contract_score:   Real ∈ [0,1] — contract conformance
    truth_score:      Integer ∈ [0,100] — composite heuristic %
    formula: truth_score = round(min(100, epistemic_score · contract_score · μ · 100))
    μ = 1 in PSL base (identity); calibrated by SAS at runtime

  Conformance: domain extensions SHOULD target L2 conformance (§R1 of v0.1.5-p).
*)

Domain_O_Checks ≜ [

  O9:  "[Domain check — e.g. Evidence tier consistent: output cites evidence at declared tier?]",
  O10: "[Domain check — e.g. Regulatory citations current: referenced regulations in force?]",
  O11: "[Domain check — e.g. Population scope respected: claims stay within study population?]"

]

Domain_O_Rationale ≜ [
  O9:  "[Why is this verification necessary in this domain?]",
  O10: "[Why is this verification necessary in this domain?]",
  O11: "[Why is this verification necessary in this domain?]"
]


(* ═══ §5. DOMAIN SPT EXTENSIONS ═══ *)

(*
  Define domain-specific prohibited inference patterns.
  S→T, L→G, Δe→∫de from base spec are preserved and still apply.
  Add patterns that are structurally common in this domain.
*)

Domain_SPT_Violations ≜ [

  (* Example structure — define your own patterns below *)

  "D1→[pattern name]": [
    name:    "[VIOLATION NAME]",
    pattern: "[Describe the specific faulty inference common in this domain]",
    signal:  "[Linguistic or structural signals that trigger this check]",
    action:  "retag(claim, ⊬) ∧ name violation ∧ [domain-specific remediation]",
    example: "[Concrete example of this violation in the domain]"
  ],

  "D2→[pattern name]": [
    name:    "[VIOLATION NAME]",
    pattern: "[...]",
    signal:  "[...]",
    action:  "retag(claim, ⊬) ∧ name violation",
    example: "[...]"
  ]

  (*
    Suggested domain-specific SPT seeds:

    MEDICAL:
      "C→P":      Correlation-to-Causation — inferring causal mechanism from observational correlation
      "Pop→Ind":  Population-to-Individual — applying group statistics to individual prognosis

    LEGAL:
      "Jx→Jx":    Cross-Jurisdiction — applying one jurisdiction's ruling to another
      "Dict→Bind": Dictum-to-Binding — treating obiter dictum as binding precedent

    SDLC:
      "Dev→Prod":  Dev-to-Production — inferring production behavior from dev/test environment
      "Spec→Impl": Spec-to-Implementation — asserting implementation detail not in spec

    RESEARCH:
      "Pilot→Pop":            Pilot-to-Population — generalizing from pilot study to full population
      "Correlation→Mechanism": Statistical finding to mechanistic explanation
      Note: PREPRINT is ⊨ at best — insufficient for grounding broad claims alone

    FINANCE:
      "Hist→Future": Historical-to-Forecast — treating backtested performance as predictive
                     Note: BACKTEST is ⊨ (inferred) — past performance does not ground
                     forward-looking claims (EEF: ⊬); insufficient for grounding broad claims
      "Model→Market": Model output treated as market fact
  *)

]


(* ═══ §6. DOMAIN CONTRACT ARCHETYPES ═══ *)

(*
  Define domain-specific CONTRACT templates.
  Each archetype extends the base CONTRACT structure.
*)

Domain_Contracts ≜ [

  Archetype_1 ≜ [
    name:         "[CONTRACT TYPE — e.g. Clinical Summary / Legal Opinion / Code Review]",
    input:        "[Input schema — what information is required to run this contract?]",
    output:       "[Output schema — what structured output is expected?]",
    constraints:  {
      "[Constraint 1 — e.g. all claims must be tagged with Tier2 evidence glyphs]",
      "[Constraint 2 — e.g. off-label claims must carry ⊬off tag with basis]"
    },
    negatives:    {
      "[Forbidden output 1 — e.g. no dosing recommendations without ⊢rct grounding]",
      "[Forbidden output 2]"
    },
    p_extensions: {"P6", "P7"},   (* Which domain P-checks apply to this contract *)
    o_extensions: {"O9", "O10"}   (* Which domain O-checks apply to this contract *)
  ],

  Archetype_2 ≜ [
    name:         "[CONTRACT TYPE 2]",
    input:        "[...]",
    output:       "[...]",
    constraints:  {"[...]"},
    negatives:    {"[...]"},
    p_extensions: {"[...]"},
    o_extensions: {"[...]"}
  ]

]


(* ═══ §7. DOMAIN GLOSSARY ═══ *)

(*
  Define domain-specific terms.
  Extends base TPMN-PSL Glossary — do not redefine base terms.
*)

Domain_Glossary ≜ [

  "[Term 1]": "[Definition — grounded in domain standard or authoritative source]",
  "[Term 2]": "[Definition]",
  "[Term 3]": "[Definition]"

  (*
    Examples by domain:

    MEDICAL:
      "RCT":       "Randomized Controlled Trial — highest evidence tier for intervention claims",
      "Off-label":  "Use beyond approved indication — requires ⊬off tag and explicit basis",
      "PREPRINT":   "Not yet peer-validated — ⊨ at best; insufficient for grounding broad claims alone",

    LEGAL:
      "Obiter dictum":   "Judicial remark not essential to the decision — not binding precedent",
      "Ratio decidendi": "Legal reasoning essential to the decision — binding in jurisdiction",

    SDLC:
      "Spec-grounded": "Claim directly traceable to a written, versioned specification",
      "MANDATE":       "Computable, verifiable, traceable specification space established by P-phase —
                        comprises CONTRACT + A_Priori_Grid + Panini_Categories",
      "Regression":    "Behavior change in previously verified functionality",

    RESEARCH:
      "p-value":     "Probability of observed result under null hypothesis — not effect size",
      "Replication": "Independent reproduction of a finding — required for ⊢rep tag",

    FINANCE:
      "Backtesting":    "Applying a model to historical data — ⊨ (inferred); does not ground
                         forward-looking claims; insufficient for grounding broad claims alone",
      "Mark-to-market": "Valuation at current market price — a state, not a trait"
  *)

]


(* ═══ §8. EXTENSION SUMMARY ═══ *)

Domain_Summary ≜ [
  base:             "TPMN_PSL v0.1.5-p",
  domain:           "[DOMAIN]",
  tier2_glyphs:     "[Count] domain-specific epistemic glyphs defined",
  p_extensions:     "[Count] additional P-phase checks (P6+)",
  o_extensions:     "[Count] additional O-phase checks (O9+)",
  spt_extensions:   "[Count] domain-specific SPT violation patterns",
  contract_types:   "[Count] domain CONTRACT archetypes",
  preserved:        "All Tier1 glyphs · P0–P5 · O1–O8 · S→T · L→G · Δe→∫de",
  conformance:      "Target: L2 (full three-mode checker with P/O phases)",
  version_note:     "This is a draft — community review required before v1.0.0 status"
]

===
```

---

## How to Contribute

The TPMN-PSL base specification is open. This domain extension template is the starting point — not the finish line.

**What makes a good domain extension:**
- Tier2 glyphs that map to real epistemic distinctions your field already uses
- P/O checks that catch errors professionals in your domain actually make
- SPT violations grounded in documented failure modes, not intuition
- CONTRACT archetypes derived from real workflows, not hypothetical ones

**To contribute your domain extension:**
1. Fork the repository on GitHub
2. Copy this template into `/extensions/[domain]/`
3. Fill in every `[placeholder]` with domain-grounded content
4. Submit a pull request with a brief rationale for each addition
5. Community review · maintainer sign-off · version assignment

**Target domains currently open:** SDLC · Medical · Research · Legal · Finance · and any domain where AI makes claims that carry real consequences.

The specification gets better when domain experts write the rules for their own field.
