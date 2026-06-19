# TPMN-PSL Domain Extension Template
**Base:** TPMN-PSL v0.1.6 | **License:** CC-BY 4.0

---

```tla
--- MODULE [DOMAIN]_TPMN_PSL ---

EXTENDS TPMN_PSL  (* v0.1.6 *)

(* ═══ §0. EXTENSION CONTRACT ═══ *)

Extension ≜ [
  domain:    "[DOMAIN]",
  version:   "v0.1.0-draft",
  base:      "TPMN_PSL v0.1.6",

  (* ── What extensions MUST preserve ── *)
  preserves: {
    "GEM² foundational framework",
    "ΣΔ Principle",
    "OntologicalTerms (DATA, STATE, STATUS, THRESHOLD)",
    "Tier1 glyphs (⊢ ⊨ ⊬ ⊥ ?) — complete, no extension",
    "P0–P5 · O1–O8",
    "SPT base (S→T, L→G, Δe→∫de)",
    "EEF_Record structure"
  },

  (* ── What extensions CAN add ── *)
  extends: {
    "Domain OntologicalTerms binding (§1)",
    "Domain P-phase checks P6+ (§2)",
    "Domain O-phase checks O9+ (§3)",
    "Domain SPT violations (§4)",
    "Domain CONTRACT archetypes (§5) —
     domain semantics expressed as CONTRACT constraints, not as additional glyphs"
  }
]


(* ═══ §1. DOMAIN ONTOLOGICAL TERMS ═══ *)
(*
  Bind DATA / STATE / STATUS / THRESHOLD to this domain.
  STATUS is ∫δ observed; THRESHOLD discretizes into ΣΔ.
*)

Domain_OntologicalTerms ≜ [
  DATA:            "[domain-specific discrete elements]",
  STATE:           "[finite set of discrete labels]",
  STATUS:          "[continuous measurements]",
  THRESHOLD:       "[cut points for STATE transitions]",
  transition_rules: "[STATUS → THRESHOLD → STATE mappings]"
]


(* ═══ §2. DOMAIN P-PHASE CHECKS ═══ *)
(* P0–P5 preserved. P6 = Panini discretization (if bounded domain). P7+ = domain. *)

Domain_P_Checks ≜ [
  P6: "Categories defined — Panini set_contract satisfied?",
  P7: "[domain check]"
]


(* ═══ §3. DOMAIN O-PHASE CHECKS ═══ *)
(* O1–O8 preserved. O9+ = domain. *)

Domain_O_Checks ≜ [
  O9:  "[domain check]"
]


(* ═══ §4. DOMAIN SPT VIOLATIONS ═══ *)
(* S→T, L→G, Δe→∫de preserved. Domain patterns below. *)

Domain_SPT ≜ [
  "D1→[name]": [
    pattern: "[prohibited inference]",
    signal:  "[detection trigger]",
    action:  "retag(claim, ⊬) ∧ name violation"
  ]
]


(* ═══ §5. DOMAIN CONTRACT ARCHETYPES ═══ *)
(*
  Domain semantics (evidence tier, jurisdiction, source type) belong here —
  as CONTRACT constraints in F: A → B | P, not as additional glyphs.
*)

Domain_Contracts ≜ [
  Archetype_1 ≜ [
    name:        "[CONTRACT TYPE]",
    input:       "[A schema]",
    output:      "[B schema]",
    constraints: {"[P — domain-specific constraints]"},
    negatives:   {"[forbidden outputs]"}
  ]
]


(* ═══ §6. DOMAIN GLOSSARY ═══ *)
(* Extends base glossary (§10 of v0.1.6). Do not redefine base terms. *)

Domain_Glossary ≜ [
  "[term]": "[definition]"
]

===
```
