--- MODULE TPMN_PSL ---


(* ═══ §0. OVERVIEW ═══ *)

Overview ≜ [
  name:    "TPMN-PSL",
  version: "v0.1.6",
  status:  "Public · General Purpose",
  purpose: "Formal epistemic protocol for structuring, validating, and auditing AI reasoning",
  tagline: "For complex, high-stakes AI workflows: don't write prompts. Write specifications.",
  extends: "None — this is the base specification"
]

Scope ≜ [
  covers: {
    "GEM² foundational framework and ΣΔ principle",
    "Ontological terms (DATA, STATE, STATUS, THRESHOLD)",
    "Notation grammar (TLA+, Panini, Math, NL)",
    "Symbol governance (Tier1 fixed — domain specifics belong in CONTRACT)",
    "Epistemic tagging system (EEF)",
    "Prohibited inference patterns (SPT)",
    "Three-phase checking protocol (P / Inline / O)",
    "Contract archetype",
    "Output format rules",
    "Extension protocol"
  },
  not_covers: {
    "Platform-specific actor pipelines (GEM².AI, etc.)",
    "Domain-specific symbol vocabularies",
    "Implementation details of any checker tool",
    "Training or fine-tuning of LLMs"
  }
]


(* ═══ §0.1 FOUNDATIONAL CONCEPTS ═══ *)

(* ─── GEM² Universe ─── *)
GEM²_Definition ≜ [
  acronym:   "Grounded Existence Matrix for Global Entropy Minimum",
  expansion: [
    Grounded:  "Every element has a verifiable basis — nothing enters the system ungrounded",
    Existence: "Ontological status is decidable — an element exists (⊢) or is absent (⊥),
                never ambiguous",
    Matrix:    "Discrete structural framework organizing elements and their relationships —
                finite, indexed, computable",
    Global:    "The mission — create ontological BEING that precisely, correctly reflects
                human NL intent across the entire system. This is the reason GEM² is defined
                and GEM².AI is built. TPMN-PSL is the protocol between human and AI
                to realize it.",
    Entropy:   "Epistemic disorder — context dilution, drift, hallucination, overclaim,
                untagged extrapolation, category boundary violation.
                What the system measures and reduces.",
    Minimum:   "Convergence goal — the closest approximation to human's need.
                Truth grounded by controlling AI entropy. The more agentic processing
                and autonomous AI working, the more entropy emerges. TPMN CONTRACT
                minimizes entropy growth over context and workflow — real AI tasks
                (SDLC, multi-step workflows) are not one-shot."
  ],
  shorthand: "GEM² ≜ Mathematical universe where AI operates with provable boundaries",
  status:    "Platform-agnostic — GEM² is the mathematical framework, not any specific
              implementation. GEM².AI is one platform realization of GEM²."
]

(* ─── ΣΔ Principle ─── *)
(* TPMN-PSL operates in ΣΔ space — finite sums of discrete units —            *)
(* not ∫δ space — continuous integration of infinitesimals.                     *)
(* Every domain is carved into countable categories.                            *)
(* Every claim belongs to a named set. Every evidence count is finite.          *)

ΣΔ_Principle ≜ [
  statement:   "TPMN-PSL is the world of finite Σ of Δ, not infinite ∫ of δ",
  discrete:    "Σ (finite summation) of Δ (discrete differences) —
                countable, bounded, decidable",
  continuous:  "∫ (continuous integration) of δ (infinitesimals) —
                what TPMN-PSL structurally prohibits",
  implication: "All categories are finite sets. All evidence is enumerable.
                All membership is decidable.",
  connection:  "SPT violation Δe→∫de is the direct prohibition:
                discrete evidence cannot yield continuous conclusions",
  foundation:  "SET theory is the mathematical base —
                Panini extracts SETs from the NL world"
]

(* ─── Ontological Terms ─── *)
OntologicalTerms ≜ [
  DATA:      "Discrete, computable, verifiable, falsifiable element",
  STATE:     "Discrete label from finite set",
  STATUS:    "Continuous measurement from DATA within a STATE",
  THRESHOLD: "Cut point for STATE transitions",
  note:      "STATUS is the ∫δ world observed; THRESHOLD discretizes it into ΣΔ space.
              Platform extensions define domain-specific STATUS→STATE transition rules."
]


(* ═══ §1. GRAMMAR ═══ *)

TPMN_Grammar ≜ [

  (* ═══ 1.1 TLA+ Conventions ═══ *)
  (*                                                                         *)
  (* Reference: Leslie Lamport, "Specifying Systems" (2002).                *)
  (* TLA+ ASCII syntax is canonical; Unicode forms are display aliases.     *)
  (* TPMN-PSL uses TLA+ as the structural expression layer — for            *)
  (* definitions, records, sets, sequences, and functions.                   *)
  (* TLA+ is one of four notation layers, not the whole system.             *)
  (* Temporal/action operators (□, ◇, ′, UNCHANGED, ENABLED) are           *)
  (* outside TPMN-PSL scope.                                                 *)
  (*                                                                         *)

  TLA_Conventions ≜ [
    scope:        "TLA+ expresses structure, flow, and relationships between
                   components in a CONTRACT. It is the formal backbone —
                   Panini defines WHAT exists, TLA+ expresses HOW it is structured.",

    (* ── Constructs used in TPMN-PSL ── *)
    module:       "---- MODULE Name ----  ...  ====",
    extends:      "EXTENDS TPMN_PSL  (* version *)",
    definitions:  "op ≜ expr  (* display form of TLA+ op == expr *)",
    records:      "[field: value, ...]  (* display shorthand for [field |-> value] *)",
    record_access:"r.field",
    sets:         "{e₁, e₂, ..., eₙ}   (* enumeration *)
                   {x ∈ S : P(x)}       (* filter / comprehension *)",
    membership:   "x ∈ S, x ∉ S, S ⊆ T",
    sequences:    "<<e₁, e₂, ...>>      (* finite ordered sequence *)
                   Seq(S)                (* set of all finite sequences over S *)",
    functions:    "[x ∈ S ↦ expr]       (* function constructor *)
                   f(x) ≜ expr          (* named operator with parameters *)",
    conditionals: "IF cond THEN e₁ ELSE e₂",
    let_in:       "LET x ≜ e₁ IN e₂    (* local binding *)",
    comments:     "(* ... *)             (* block comment — standard TLA+ *)",

    (* ── TPMN-PSL display conventions beyond standard TLA+ ── *)
    tpmn_display: [
      "≜  — display form of ==  (used throughout TPMN-PSL)",
      "⊥  — explicit unknown/absent value (not in standard TLA+)",
      "𝕊  — display alias for STRING",
      "ℕ  — display alias for Nat",
      "ℤ  — display alias for Int",
      "ℝ  — display alias for Real",
      "∀ ∃ ∧ ∨ ⟹ ⟺ ∈ ⊆ ∪ ∩ ↦  — Unicode display of TLA+ ASCII operators"
    ]
  ],

  (* ═══ 1.2 Panini Adaptation ═══ *)
  (*                                                                         *)
  (* PRIMARY FUNCTION: Ontological discretization layer                     *)
  (* MATHEMATICAL BASE: SET theory                                           *)
  (*                                                                         *)
  (* Pāṇini's method: extract SETs from the NL world — carve a continuous, *)
  (* ambiguous domain into a finite set of mutually exclusive, exhaustive   *)
  (* categories via explicit membership rules.                               *)
  (* Each rule is a set-membership assertion.                                *)
  (*                                                                         *)
  (* In TPMN: Panini is the bridge from NL ambiguity → computable MANDATE  *)
  (* In GEM²: Panini defines the ontological objects that exist in the      *)
  (*          GEM² universe — what CAN be reasoned about.                   *)
  (* In ΣΔ:   Panini is the mechanism that transforms ∫δ (continuous NL)   *)
  (*          into ΣΔ (finite, discrete, decidable categories).             *)

  Panini_Adaptation ≜ [

    primary_function: "SET extraction from NL — define the SET structure of
                       the target domain BEFORE reasoning begins.
                       SET theory is the mathematical base of all Panini operations.",

    (* ─── Set Contract (FIX-7: normative design requirement, not universal guarantee) ─── *)
    set_contract: [
      role:             "Normative category design contract for bounded domains",
      mutual_exclusion: "Target condition: ∀ i ≠ j: Sᵢ ∩ Sⱼ = ∅",
      exhaustion:       "Target condition: S₁ ∪ S₂ ∪ ... ∪ Sₙ = D",
      decidability:     "Target condition: ∀x ∈ D: membership(x, Sᵢ) is operationally computable",
      note:             "These are design requirements for domains that choose Panini discretization.
                         In open-ended NL domains, full satisfaction may be approximate,
                         extension-bounded, or workflow-scoped rather than globally guaranteed."
    ],

    method: [
      step_1: "Identify target domain D from the prompt",
      step_2: "Carve D into mutually exclusive, exhaustive categories S₁...Sₙ",
      step_3: "Define explicit membership rule per category",
      step_4: "Fix category structure as immutable — becomes part of A_Priori_Grid"
    ],

    phase_binding: [
      P_phase:      "Panini defines SET structure → establishes the computable MANDATE",
      Inline_phase: "Every claim declares membership: ∀ claim c: c ∈ Sᵢ must be stated",
      O_phase:      "Verify no claim crossed a category boundary without ⊬ escalation"
    ],

    (* ─── Drift Model (FIX-6: tpmn_response retagged ⊢ → ⊨) ─── *)
    drift_model: [
      observation:   "⊨ LLM reasoning may degrade across long, high-density content —
                       category boundaries can blur and inference may drift",
      mechanism:     "⊨ One plausible model: continuous embedding space lacks hard
                       categorical walls; without recalibration, inference may cross
                       set boundaries silently. Other mechanisms (attention dilution,
                       recency bias, decoding instability) may also contribute.",
      tpmn_response: "⊨ Inline set-membership declaration is intended to re-anchor
                       reasoning to the P-phase category structure by repeatedly
                       exposing category boundaries during generation.
                       This is a design hypothesis of TPMN, not yet a universally
                       established empirical law."
    ],

    secondary_functions: [
      acronym_pattern:   "NAME ≜ [Letter: \"Meaning\", ...] — compact decomposition",
      predicate_pattern: "Predicate(args) ≜ expression — category-membership assertion",
      compact_rule:      "Minimize tokens while preserving categorical precision"
    ],

    kantian_note: "A_Priori_Grid ⊇ Panini_Categories — the SET structure
                   IS the a priori imposed before experience is processed"
  ],

  (* ═══ 1.3 Math Notation ═══ *)
  Math_Notation ≜ [
    quantifiers: "∀ (for all), ∃ (exists), ∃! (unique exists)",
    connectives: "∧ (and), ∨ (or), ¬ (not), ⟹ (implies), ⟺ (iff)",
    sets:        "∈ (in), ∉ (not in), ⊆ (subset), ∪ (union), ∩ (intersect)",
    usage_rule:  "Prefer math notation over NL when expressing logic"
  ],

  (* ═══ 1.4 NL Rules ═══ *)
  NL_Rules ≜ [
    comments:   "(* ... *) for inline explanation",
    values:     "String values for NL meanings",
    prohibited: {"markdown tables", "ASCII trees", "verbose paragraphs"},
    usage_rule: "NL for prompts and messages — NOT for definitions"
  ]

]


(* ═══ §2. SYMBOL GOVERNANCE ═══ *)

Symbol_Governance ≜ [

  (* ═══ 2.1 Tier1 — Fixed Core Glyphs ═══ *)
  (*                                                                           *)
  (* Five epistemic tags form a complete, exhaustive partition of epistemic    *)
  (* status. No domain requires a sixth epistemic state.                      *)
  (* Domain-specific distinctions (evidence tier, jurisdiction, source type)   *)
  (* are domain SEMANTICS, not epistemic STATUS — they belong in CONTRACT     *)
  (* constraints (F: A → B | P), not in the glyph system.                    *)
  (*                                                                           *)

  Glyphs ≜ [
    nature:  "FIXED — immutable, universal, sufficient",
    rule:    "Use exactly as defined. No reassignment. No extension.",
    design:  "Glyphs mark EPISTEMIC STATUS only. Domain semantics are expressed
              in CONTRACT constraints, not in additional symbols.",

    epistemic: [
      "⊢": "GROUNDED — supported by input or verifiable fact",
      "⊨": "INFERRED — derived from grounded claims; inference chain visible",
      "⊬": "EXTRAPOLATED — beyond evidence; basis must be explicitly stated",
      "⊥": "UNKNOWN — knowledge gap; stops inference chain",
      "?": "SPECULATIVE — possible but unverified"
    ],

    logic: [
      "∀": "for all",        "∃": "there exists",
      "∧": "and",            "∨": "or",
      "¬": "not",            "⟹": "implies",
      "⟺": "iff",           "≜": "defined as",
      "∈": "element of",     "⊆": "subset of",
      "∪": "union",          "∩": "intersection"
    ]
  ]

]


(* ═══ §3. EEF — EPISTEMIC EVIDENCE FRAMEWORK ═══ *)

EEF ≜ [
  name:    "Epistemic Evidence Framework",
  purpose: "Tag every non-trivial claim with its epistemic status",
  scope:   "Applies to any AI-generated content under TPMN protocol",

  evolution: [
    origin:    "Originally designed as Explicit Extrapolation Flag — a BOOLEAN gate",
    current:   "Evolved to five-tag epistemic taxonomy (⊢ ⊨ ⊬ ⊥ ?)",
    invariant: "Core intent preserved — flag epistemic status so enforcement layer can react"
  ]
]

EpistemicTag ≜ {"⊢", "⊨", "⊬", "⊥", "?"}

TagRules ≜ [
  R1_inline:   "∀ non-trivial claim ∈ Output: ∃ tag ∈ EpistemicTag attached",
  R2_basis:    "tag = ⊬ ⟹ explicit basis statement attached to claim",
  R3_terminal: "tag = ⊥ ⟹ no downstream claim depends on it without ⊬ escalation",
  R4_honest:   "tag reflects actual epistemic status — not desired status"
]

(* ─── Score Types (FIX-12) ─── *)
EpistemicScore ≜ {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0}
ContractScore  ≜ {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0}

(* ─── truth_score as composite heuristic % (FIX-17) ─── *)
(*                                                                              *)
(* truth_score is NOT pre-defined by assumption.                               *)
(* It is an emergent heuristic derived from accumulated SAS evaluation data.  *)
(*                                                                              *)
(* Formula:                                                                     *)
(*   truth_score ≜ round(min(100, epistemic_score · contract_score · μ · 100)) *)
(*                                                                              *)
(* Where μ (modification_factor):                                              *)
(*   PSL base:    μ = 1  (identity — no calibration effect)                   *)
(*   SAS runtime: μ = f(sim) derived from similarity query over                *)
(*                accumulated O_Records in TPMN-checker SAS                   *)
(*                                                                              *)
(* Epistemic status of μ calibration mechanism: ⊨ (design hypothesis)        *)
(* truth_score will emerge from piled data — it is not top-down designed      *)

TruthScorePercent ≜ {n ∈ ℕ : 0 ≤ n ∧ n ≤ 100}

TruthScorePolicy ≜ [
  formula:             "truth_score ≜ round(min(100, epistemic_score · contract_score · μ · 100))",
  psl_default:         "μ = 1  (* identity — formula reduces to round(e · c · 100) *)",
  sas_runtime:         "⊨ μ derived from similarity query against accumulated O_Records in SAS",
  emergence_note:      "⊬ truth_score is a heuristic that will emerge from accumulated data —
                         calibration mechanism is a design hypothesis, not yet empirically validated",
  output_format:       "Integer ∈ [0,100] — LLM MUST output truth_score as integer percent, not Real",
  output_example:      "truth_score: 75  (* not 0.75 *)"
]

(* ─── EEF Record (FIX-11: spt_violations null → Seq(𝕊)) ─── *)
NoViolations ≜ <<>>

EEF_Record ≜ [
  extrapolation:  BOOLEAN,
  confidence:     {"HIGH", "MEDIUM", "LOW", "UNKNOWN"},
  rules:          [GND, EXT, UNC, SPT: {"PASS", "FAIL", "N/A"}],
  spt_violations: Seq(𝕊),    (* empty = NoViolations = <<>>, never ⊥ or null *)
  ambiguity:      𝕊 ∪ {⊥}
]

ConfidenceCalibration ≜ [
  HIGH:   "all claims ⊢ or ⊨ · zero ⊬ · zero ⊥ on critical path",
  MEDIUM: "some ⊬ with basis stated · no ⊥ on critical path",
  LOW:    "⊥ on critical path ∨ multiple ⊬ without strong basis"
]


(* ═══ §4. SPT — STRUCTURAL PROHIBITION TAXONOMY ═══ *)

SPT ≜ [
  name:    "Structural Prohibition Taxonomy",
  purpose: "Define inference patterns that MUST NOT appear in TPMN-governed output"
]

SPT_Violations ≜ [

  "S→T": [
    name:    "STATE to TRAIT",
    pattern: "Treating a mutable, temporary state as an immutable, inherent trait",
    signal:  "always, never, inherently, fundamentally, by nature",
    action:  "retag(claim, ⊬) ∧ name violation"
  ],

  "L→G": [
    name:    "LOCAL to GLOBAL",
    pattern: "Extending a local observation to a universal claim without sufficient coverage",
    signal:  "all, every, none, no one — applied beyond surveyed scope",
    action:  "retag(claim, ⊬) ∧ scope the claim explicitly"
  ],

  "Δe→∫de": [
    name:    "INCREMENTAL to MASS",
    pattern: "Drawing large conclusions from thin or singular evidence",
    signal:  "|evidence| ≤ 2 supporting a broad claim",
    action:  "retag(claim, ⊬) ∧ state evidence count explicitly"
  ]

]

(* ─── SPT_Check rewritten — circularity removed (FIX-8) ─── *)
SPT_Signals(claim, evidence_count) ≜
  claim uses {"always", "never", "inherently", "fundamentally", "every", "none"}
  ∨ evidence_count ≤ 2

SPT_Classify(claim, evidence_count, scope) ≜
  IF claim uses {"always", "never", "inherently", "fundamentally"}
    THEN "S→T"
  ELSE IF claim uses {"every", "none", "all"} ∧ scope = "beyond surveyed set"
    THEN "L→G"
  ELSE IF evidence_count ≤ 2
    THEN "Δe→∫de"
  ELSE ⊥

SPT_Check(claim, evidence_count, scope) ≜
  LET violation ≜ SPT_Classify(claim, evidence_count, scope)
  IN IF violation = ⊥
       THEN [status |-> "PASS",  violation |-> ⊥]
       ELSE [status |-> "FAIL",  violation |-> violation,
             action |-> "retag(claim, ⊬) ∧ name(violation)"]


(* ═══ §5. THREE-PHASE CHECKING PROTOCOL ═══ *)

TPMN_PRO ≜ [
  name:   "TPMN Protocol — Pre / Inline / Output",
  phases: "P-phase → Inline → O-phase",
  note:   "P-phase MUST precede O-phase. Inline applies throughout generation."
]

(* ═══ 5.1 P-Phase — Pre-flight Prompt Validation (FIX-9: failure semantics added) ═══ *)
P_Phase ≜ [
  when:    "Before LLM execution",
  purpose: "Extract contract · validate constraints · establish A_Priori_Grid
            including Panini category structure when domain is bounded",

  checks: [
    P0: "Contract present — does the prompt define expected output?",
    P1: "Scope bounded — are domain limits stated?",
    P2: "Entities typed — are key terms defined?",
    P3: "Constraints explicit — are acceptance criteria present?",
    P4: "Schema defined — is output structure specified?",
    P5: "Context isolated — is the prompt self-contained?"
  ],

  result: "{PASS | FAIL | CONDITIONAL}",

  failure_policy: [
    PASS:        "Proceed to generation",
    FAIL:        "Do not execute LLM generation · return P_Record with diagnostic violations",
    CONDITIONAL: "Permit execution only after explicit downgrade / clarification / repair step"
  ],

  output: "A_Priori_Grid + P_Record"
]

(* ─── P_Record (FIX-18) ─── *)
P_Record ≜ [
  result:      {"PASS", "FAIL", "CONDITIONAL"},
  failed:      Seq(𝕊),
  conditional: Seq(𝕊),
  repair_hint: 𝕊 ∪ {⊥}
]

(* ─── A_Priori_Grid (FIX-10: immutability clarified) ─── *)
A_Priori_Grid ≜ [
  definition:  "Intermediate Representation extracted from prompt during P-phase",
  structure:   "[contract, constraints, entities, schema, scope, context,
                 ? categories: Seq(PaniniCategory)]",
  purpose:     "Shapes LLM generation · used as verification baseline in O-phase",
  immutable:   "TRUE within a single run",
  note:        "If generation reveals the grid is incomplete, contradictory, or mis-scoped,
                the correct action is P-phase restart / recompile — not silent mutation.
                Immutability applies per execution instance, not across revised runs."
]

PaniniCategory ≜ [
  name:            𝕊,
  domain:          𝕊,
  membership_rule: 𝕊,
  set_contract:    [mutual_exclusion: BOOLEAN, exhaustion: BOOLEAN, decidability: BOOLEAN]
]

(* ═══ 5.2 Inline Phase — Generation Tagging ═══ *)
Inline_Phase ≜ [
  when:    "During LLM output generation",
  purpose: "Tag every non-trivial claim with EpistemicTag as it is written",
  rule:    "TagRules.R1–R4 apply continuously during generation",
  note:    "Inline phase is spec-defined; implementation depends on platform"
]

(* ═══ 5.3 O-Phase — Post-flight Output Verification ═══ *)
O_Phase ≜ [
  when:    "After LLM output is produced",
  purpose: "Verify output against A_Priori_Grid contract · gate or pass",

  checks: [
    O1: "Schema conformance — output matches declared structure",
    O2: "Constraint satisfaction — explicit constraints met",
    O3: "Entity consistency — typed entities used consistently",
    O4: "SPT clean — no S→T, L→G, Δe→∫de violations",
    O5: "EEF coherent — ⊬ claims have stated basis · ⊥ not on critical path",
    O6: "Scope respected — output stays within P-phase bounds",
    O7: "Contract fulfilled — promise of P-phase delivered",
    O8: "Category integrity — if categories ∈ A_Priori_Grid,
         verify no claim crossed a category boundary without ⊬ escalation"
  ],

  result: "{PASS | FAIL | CONDITIONAL}",
  output: "O_Record"
]

(* ─── O_Record (FIX-12, FIX-17, FIX-18) ─── *)
O_Record ≜ [
  result:           {"PASS", "FAIL", "CONDITIONAL"},
  epistemic_score:  EpistemicScore,    (* Real ∈ [0,1] — grounding quality *)
  contract_score:   ContractScore,     (* Real ∈ [0,1] — contract conformance *)
  truth_score:      TruthScorePercent, (* ℕ ∈ [0,100] — composite heuristic % *)
  violations:       Seq(𝕊),
  eef_record:       EEF_Record
]

O_Record_Rules ≜ [
  R1: "0.0 ≤ epistemic_score ≤ 1.0",
  R2: "0.0 ≤ contract_score ≤ 1.0",
  R3: "0 ≤ truth_score ≤ 100",
  R4: "epistemic_score measures grounding quality only",
  R5: "contract_score measures schema / scope / constraint satisfaction only",
  R6: "truth_score = round(min(100, epistemic_score · contract_score · μ · 100))",
  R7: "result MUST be computed from rule evaluation — not from score averaging alone",
  R8: "truth_score output MUST be integer — LLM must not emit 0.75, must emit 75"
]

(* ─── Score Rules ─── *)
ScoreRules ≜ [
  epistemic_score: "Score ∈ [0,1] estimating epistemic grounding quality only",
  contract_score:  "Score ∈ [0,1] estimating contract conformance only",
  truth_score:     "Composite heuristic % ∈ [0,100] — emergent from SAS data accumulation",
  note:            "epistemic_score and contract_score MUST NOT be conflated"
]


(* ═══ §6. CONTRACT ARCHETYPE ═══ *)

(* ─── Metric type defined (FIX-13) ─── *)
Metric ≜ [
  name:       𝕊,
  expression: 𝕊,
  target:     𝕊,
  comparator: {"<", "≤", "=", ">", "≥"}
]

CONTRACT ≜ [
  archetype: "In → Out | Constraints",
  purpose:   "Formal specification of what a prompt demands",

  structure: [
    contract_id:  𝕊,
    input:        Schema,
    output:       Schema,
    constraints:  {Constraint},
    negatives:    {ForbiddenCase},
    metrics:      [𝕊 ↦ Metric]
  ],

  rules: [
    "CONTRACT must be extractable from prompt during P-phase",
    "CONTRACT is immutable once P-phase completes",
    "O-phase verifies output against CONTRACT — not against intent"
  ],

  example: [
    contract_id:  "example_auth",
    input:        "[credentials: Credentials]",
    output:       "[token: JWT, expires: Timestamp]",
    constraints:  {"valid_credentials ⟹ token ≠ ⊥"},
    negatives:    {"no_plaintext_in_response"},
    metrics:      ["latency" ↦ [name: "latency", expression: "response_time_ms",
                                 target: "200", comparator: "<"]]
  ]
]


(* ═══ §7. PHILOSOPHICAL FOUNDATION ═══ *)
(* Heuristic philosophical framing — explanatory, not required for execution  *)
(* or formal validity (FIX-16)                                                 *)

KantianMapping ≜ [

  status: "Heuristic philosophical framing, not a formal proof of TPMN correctness",

  Noumena ≜ [
    kant: "Thing-in-itself — beyond direct access",
    tpmn: "User's true intent — under-determined by the prompt alone",
    note: "The prompt is REPRESENTATION of intent, not intent itself"
  ],

  Phenomena ≜ [
    kant: "What we experience through sensibility",
    tpmn: "Raw AI token stream — observable output",
    note: "Without structure, output is noise, not knowledge"
  ],

  A_Priori ≜ [
    kant:      "Categories imposed BEFORE experience",
    tpmn:      "TPMN rules imposed BEFORE accepting output (P0–P5, O1–O8)",
    note:      "The grid that transforms noise into structured, auditable knowledge",
    mechanism: "Panini_Categories ⊂ A_Priori — SET structure defined in §1.2
                is the operative discretization mechanism before inference begins"
  ],

  Transformation ≜ [
    before: "Prompt → AI → Hope",
    after:  "Prompt → TPMN_PRO.P → AI → TPMN_PRO.O → Trust",
    key:    "A_Priori_Grid is the missing compiler layer for AI interaction"
  ]

]

ResponsibilityBoundary ≜ [
  tpmn_solves: {
    "Requirements → CONTRACT: formalize what is being asked",
    "CONTRACT → Output: satisfy contract under TPMN rules",
    "Output → Evidence: verify and score against contract"
  },
  not_tpmn: {
    "Whether requirements reflect reality",
    "Whether CONTRACT is correct",
    "Semantic truth of training data"
  },
  boundary: "CONTRACT ≠ Reality. TPMN governs CONTRACT satisfaction, not truth-in-the-world."
]


(* ═══ §8. FORMAT RULES ═══ *)

FormatRules ≜ [
  V1: "All definitions use TPMN notation — TLA+ first, math where needed, NL for strings",
  V2: "EEF_Record MUST accompany any TPMN-governed output",
  V3: "Timestamp MUST be executed — never guessed, copied, or hardcoded",
  V4: "Violations MUST name the SPT pattern and the specific claim",
  V5: "epistemic_score ∈ [0,1] — grounding quality only",
  V6: "contract_score ∈ [0,1] — contract conformance only",
  V7: "truth_score ∈ [0,100] — integer percent — LLM MUST output as integer, not Real"
]

FormatProhibitions ≜ [
  N1: "Never omit EEF_Record from governed output",
  N2: "Never use ⊢ for claims that are inferred or extrapolated",
  N3: "Never suppress ⊬ or ⊥ tags to appear more confident",
  N4: "Never redefine or extend Tier1 glyphs — domain specifics belong in CONTRACT",
  N5: "Never run O-phase without a preceding P-phase — contract must precede verification",
  N6: "Never emit truth_score as Real (e.g. 0.75) — MUST be integer percent (e.g. 75)"
]


(* ═══ §9. EXTENSION PROTOCOL ═══ *)

Extension_Protocol ≜ [
  purpose: "How platforms and domains extend TPMN-PSL without breaking the base",

  rules: [
    E1: "Declare EXTENDS TPMN-PSL explicitly in module header",
    E2: "Tier1 glyphs MUST NOT be redefined or extended —
         domain-specific distinctions belong in CONTRACT constraints (F: A → B | P)",
    E3: "P0–P5 and O1–O8 MUST be preserved · additional checks may be added",
    E4: "EEF_Record structure MUST be preserved · fields may be added, not removed",
    E5: "Extension version MUST reference base version explicitly",
    E6: "Extensions using Panini discretization MUST define P6 and populate
         A_Priori_Grid.categories"
  ],

  recommended_p6: [
    check: "P6: Categories defined — domain D carved into sets S₁...Sₙ
            satisfying set_contract (mutual exclusion, exhaustion, decidability)?",
    when:  "Apply when domain is explicitly bounded and Panini discretization
            is used in P-phase",
    note:  "Required in extensions · optional in base spec"
  ],

  example_header: [
    "--- MODULE MyPlatform_TPMN_PSL ---",
    "EXTENDS TPMN_PSL  (* v0.1.6 *)",
    "(* Adds: domain P/O checks, domain SPT patterns, domain CONTRACT archetypes *)"
  ]
]


(* ═══ §10. GLOSSARY ═══ *)

Glossary ≜ [
  "GEM²":                    "Grounded Existence Matrix for Global Entropy Minimum —
                               mathematical universe where AI operates with provable boundaries ·
                               platform-agnostic framework · see §0.1",
  "ΣΔ_Principle":            "TPMN-PSL is the world of finite Σ of Δ, not infinite ∫ of δ ·
                               all categories are finite sets · all evidence is enumerable ·
                               all membership is decidable · see §0.1",
  DATA:                      "Discrete, computable, verifiable, falsifiable element",
  STATE:                     "Discrete label from finite set",
  STATUS:                    "Continuous measurement from DATA within a STATE",
  THRESHOLD:                 "Cut point for STATE transitions —
                               the discretization boundary from ∫δ to ΣΔ",
  TPMN:                      "Truth-Provenance Markup Notation — the notation system",
  PSL:                       "Prompt Specification Language — grammar and rules",
  EEF:                       "Epistemic Evidence Framework — tagging and scoring system",
  SPT:                       "Structural Prohibition Taxonomy — forbidden inference patterns",
  A_Priori_Grid:             "IR extracted from prompt during P-phase · immutable within a run ·
                               optionally includes Panini_Categories when domain is bounded",
  CONTRACT:                  "Formal specification of prompt intent · immutable after P-phase",
  P_Phase:                   "Pre-flight prompt validation",
  P_Record:                  "Structured P-phase output: result + failed checks + repair hints",
  Inline_Phase:              "Claim-level epistemic tagging during generation",
  O_Phase:                   "Post-flight output verification",
  O_Record:                  "Structured O-phase output: result + scores + violations + eef_record",
  epistemic_score:           "Score ∈ [0,1] estimating epistemic grounding quality only ·
                               1.0 = fully grounded · 0.0 = fully extrapolated",
  contract_score:            "Score ∈ [0,1] estimating contract conformance only ·
                               measures schema / scope / constraint satisfaction",
  truth_score:               "Composite heuristic % ∈ [0,100] · integer output ·
                               formula: round(min(100, epistemic_score · contract_score · μ · 100)) ·
                               μ = 1 in PSL base · μ calibrated by SAS at runtime ·
                               emergent — not pre-defined top-down",
  modification_factor:       "μ ∈ [0,∞) · calibration variable in truth_score formula ·
                               PSL base: μ = 1 (identity, no effect) ·
                               SAS runtime: μ = f(sim) from similarity query over O_Records",
  NoViolations:              "<<>> — canonical empty spt_violations sequence",
  Metric:                    "Typed evaluation target: [name, expression, target, comparator] ·
                               distinct from Constraint (logical assertion)",
  Panini_Categories:         "Finite set of mutually exclusive, exhaustive, decidable categories
                               carved from domain D during P-phase · stored in A_Priori_Grid.categories",
  ontological_discretization:"Carving a continuous NL domain into finite computable categories ·
                               primary function of the Panini layer in TPMN · see §1.2",
  set_contract:              "Normative design contract for Panini categories:
                               (1) mutual_exclusion · (2) exhaustion · (3) decidability ·
                               target conditions for bounded domains — may be approximate in open NL",
  MANDATE:                   "The computable, verifiable, traceable specification space established
                               by the P-phase · comprises CONTRACT + A_Priori_Grid including
                               Panini_Categories · formal transformation of NL prompt into
                               bounded discrete structure the LLM must reason within",
  "⊢":                       "Grounded claim",
  "⊨":                       "Inferred claim",
  "⊬":                       "Extrapolated claim — basis required",
  "⊥":                       "Unknown / undefined",
  "?":                       "Speculative claim",
  "S→T":                     "State-to-Trait SPT violation",
  "L→G":                     "Local-to-Global SPT violation",
  "Δe→∫de":                  "Incremental-to-Mass SPT violation"
]


(* ═══ §11. SUMMARY ═══ *)

Summary ≜ [
  what:       "Platform-agnostic formal epistemic protocol for AI reasoning",
  universe:   "GEM² — mathematical universe where AI operates with provable boundaries",
  principle:  "ΣΔ — finite sums of discrete units, not continuous integration",
  ontology:   "DATA · STATE · STATUS · THRESHOLD — the four ontological terms",
  grammar:    "TLA+ (structure) + Panini (SET extraction from NL)
               + Math (logic) + NL (commentary) — four-layer notation,
               hierarchical: Panini defines what can be reasoned about
               before TLA+/Math/NL express it",
  symbols:    "Tier1 fixed (⊢⊨⊬⊥?) — complete epistemic partition,
               domain semantics expressed in CONTRACT, not in additional glyphs",
  protocol:   "P-phase → Inline → O-phase — three-stage checking",
  ethics:     "SPT (forbidden patterns) + EEF (epistemic tagging)",
  contract:   "In → Out | Constraints — formal specification archetype",
  scoring:    "epistemic_score [0,1] + contract_score [0,1] → truth_score % [0,100]",
  mandate:    "NL prompt → MANDATE (computable, verifiable, bounded) —
               the core transformation TPMN performs",
  extension:  "EXTENDS TPMN-PSL — any platform may extend without breaking base",
  version:    "v0.1.6 — public base specification"
]

===
