--- MODULE TPMN_PSL ---
(* ════════════════════════════════════════════════════════════════════════════ *)
(* PUBLIC EDITION                                                              *)
(* License: CC-BY-4.0 — https://creativecommons.org/licenses/by/4.0/          *)
(* Copyright (c) 2026 GEM².AI (David Seo)                                     *)
(*                                                                             *)
(* Truth scoring formula and calibration logic are redacted in this edition.    *)
(* All other content is identical to the full specification.                    *)
(* ════════════════════════════════════════════════════════════════════════════ *)


(* ═══ §0. OVERVIEW ═══ *)

Overview ≜ [
  name:    "TPMN-PSL",
  version: "v0.5.2", //you must check across this document
  status:  "Public · General Purpose",
  purpose: "Formal epistemic protocol for structuring, validating, and auditing AI reasoning",
  tagline: "For complex, high-stakes AI workflows: don't write prompts. Write specifications.",
  extends: "TPMN-PSL v0.2.0 — additive refinement, no breaking changes"
]

VersionHistory ≜ [
  v0_1_6: "Established GEM² universe, ΣΔ principle, ontological terms,
           four-layer grammar, EEF, SPT, three-phase protocol, contract archetype",
  v0_2_0: "Added (1) §0.2 Compilation Discipline — five universal principles,
           (2) §1.5 Four-Step Compilation Process,
           (3) §10 Composite Test SOUND,
           (4) §9 Domain Extension Protocol formalized,
           (5) §4 SPT explicit linkage to CTRST,
           (6) §5 P-phase total routing function,
           (7) §6 CONTRACT mapped to SIMP and CTRST",
  v0_3_0: "Added (1) §0.0 Philosophical Foundation — Kantian noumenon/phenomenon
                  alignment, GEM² as Riemann-approximation, control-at-the-edge,
                  sovereignty of F,
           (2) §0.3 Geometric Ontology — point/line/face primitives,
                  STATE/STATUS/SET as relations, dynamic axiom
                  (STATUS · point · THRESHOLD → STATE transition),
                  per-MANDATE Panini decomposition,
           (3) Refined §0.1 to distinguish ontological from topological terms,
           (4) Refined §6 CONTRACT to frame F as sovereign space for producer,
           (5) Refined §7 KantianMapping with noumenon/phenomenon distinction,
           (6) Added §5 hook for Truth field (SAS / TPMN-checker integration)"
]

Scope ≜ [
  covers: {
    "Philosophical foundation — Kantian alignment, control-at-the-edge, sovereignty of F",
    "GEM² foundational framework and ΣΔ principle (discrete projection via bounded complex faces)",
    "Ontological terms (point, line, face) — geometric primitives, noumenal",
    "Topological terms (STATE, STATUS, SET) — relational structure, phenomenal",
    "DATA, THRESHOLD — dynamic operators",
    "Compilation discipline — the five universal principles",
    "Four-step compilation process — prose → TPMN expression",
    "Geometric ontology — point/line/face/THRESHOLD dynamic",
    "Notation grammar (TLA+, Panini, Math, NL)",
    "Symbol governance (Tier1 fixed — domain specifics belong in CONTRACT)",
    "Epistemic tagging system (EEF)",
    "Prohibited inference patterns (SPT)",
    "Three-phase checking protocol (P / Inline / O)",
    "Contract archetype (F as bounded admissible relation space with sovereignty)",
    "Composite soundness test (SOUND)",
    "Domain extension protocol",
    "Output format rules"
  },
  not_covers: {
    "Platform-specific actor pipelines (GEM².AI, etc.)",
    "Domain-specific symbol vocabularies",
    "Domain-specific payoff dimensions, next-step sets, discipline rules
     — these are supplied by the domain extension, not the base spec",
    "Implementation details of any checker tool",
    "Training or fine-tuning of LLMs",
    "Lifecycle artifact structure — see TPMN-LIFECYCLE-GUIDE",
    "Skill template format — see TPMN-SKILL-STANDARD"
  }
]


(* ═══ §0.0 PHILOSOPHICAL FOUNDATION ═══ *)
(*                                                                              *)
(* The principles in this section justify everything below them.              *)
(* The geometric ontology (§0.3), the compilation discipline (§0.2),          *)
(* the three-phase protocol (§5), and the contract archetype (§6) all        *)
(* operationalize the philosophy stated here.                                 *)
(*                                                                              *)

Philosophical_Foundation ≜ [

  (* ─── Kantian Alignment ─── *)
  (*                                                                          *)
  (* TPMN-PSL operates with two distinct vocabularies that map to Kant's     *)
  (* noumenon / phenomenon distinction.                                       *)
  (*                                                                          *)
  KantianAlignment ≜ [
    statement: "Ontological vocabulary names the noumenal — the being of elements
                in itself, beyond direct access.
                Topological vocabulary names the phenomenal — how being appears
                in relation, computable and traceable.
                TPMN-PSL operates on phenomena (STATE / STATUS / SET) while
                committed to noumena (point / line / face) underneath.",

    noumenal_layer:   "Ontological terms — point, line, face — are noumenal.
                       They name what beings ARE.
                       A point is, regardless of which face it belongs to or
                       what vector rides on it. The point itself is not directly accessible in its full being, but only through its invariant representation within a space.",

    phenomenal_layer: "Topological terms — STATE, STATUS, SET — are phenomenal.
                       They name how being APPEARS.
                       STATE is the appearance of 'point belongs to face.'
                       STATUS is the appearance of 'vector acts on point.'
                       SET is the appearance of 'face as a recognized category.'",

    operational_consequence: "TPMN-PSL apparatus operates on the phenomenal layer
                              — that is what is observable, computable, traceable.
                              The ontological layer names what the spec is committed
                              to BE about, but is not directly manipulated.
                              Conflating the two layers is a category error
                              that v0.1.6 left unresolved."
  ],

  (* ─── GEM² as Riemann Approximation ─── *)
  (*                                                                          *)
  (* GEM² is not a mirror of reality. It is an approximated simulation       *)
  (* space, designed to be computable, provable, traceable.                  *)
  (*                                                                          *)
  GEM²_RiemannFraming ≜ [
    metaphor:   "Imagine filling y = x² with rectangles —
                 finite summation of discrete 2D rectangles, NOT integral of
                 infinite ones.
                 GEM² is the rectangle approximation — a discrete projection into independent bounded local complex faces ℂ_F,
one per CONTRACT / MANDATE F. Reality is the curve.",

    discrete:   "GEM² operates in ΣΔ space — finite Σ of discrete Δ.
                 Categories tile. Evidence is enumerable. Membership is decidable.
                 Approximation, by design.",

    continuous: "Reality is ∫δ — continuous integration of infinitesimals.
                 Smooth, infinite, undecidable.
                 GEM² does NOT claim to mirror this.",

    consequence: "GEM² is provably accurate within its discretization,
                  not provably accurate against reality.
                  The discretization choice (rectangle width, category granularity)
                  is a design parameter — chosen by the spec author per MANDATE,
                  not fixed by the framework.",

    boundary:    "TPMN governs CONTRACT satisfaction within the GEM² universe.
                  It does not govern truth-in-the-world.
                  This is the explicit responsibility boundary (§7)."
  ],

  (* ─── Control-at-the-Edge ─── *)
  (*                                                                          *)
  (* TPMN is for human-at-the-edge, not human-in-the-loop.                  *)
  (* The architectural commitment is sovereignty of the producer inside     *)
  (* the face, judgment by the human at the face boundary.                  *)
  (*                                                                          *)
  ControlAtTheEdge ≜ [
    architecture: "Human-at-the-edge: human defines the face boundary,
                   judges only at boundary crossings (STATE transitions).
                   The producer (human or AI) operates freely inside the face.

                   Contrast: human-in-the-loop = human approves each step.
                   High oversight, low scale, low autonomy.
                   In-the-loop is the default for current AI safety frameworks.
                   At-the-edge is the architectural alternative TPMN proposes.",

    operational_form: "The three-phase protocol P / Inline / O is the operational
                       form of human-at-the-edge.
                       P-phase defines the face boundary (CONTRACT).
                       Inline phase is the producer's sovereign work inside.
                       O-phase audits the edge crossing.
                       The producer is not surveilled inside; only audited at edges.",

    normative_claim:  "Human cannot control AI inferring. We cannot, we must not try.
                       This is normative-first, technological-second.
                       Even if interpretability technology improves to permit
                       reaching inside the producer's face, sovereignty remains
                       the architectural commitment.
                       The principle is about the right shape of human-AI relations,
                       not about the current limits of technology.",

    silent_failure_handling: "Edge-philosophy handles silent failures only if the
                              boundary is drawn tightly enough.
                              TPMN-checker / TPMN-truth-filter operates at P-phase
                              to verify boundary-grounding before the producer
                              enters the face.
                              The burden of imagining failure modes falls on the
                              boundary-drawer (P-phase author), not on the producer.
                              This asymmetry is intentional —
                              boundary-drawer thinks; producer executes.",

    self_application: "TPMN has recursive self-application:
                       (1) The producer's work is audited at the face's edge (O-phase).
                       (2) The face's edge itself is audited at P-phase
                           (TPMN-checker verifies boundary-grounding).
                       (3) The auditor's work (P-phase output) is in turn auditable.
                       Each layer applies the same edge-discipline."
  ],

  (* ─── Sovereignty of F ─── *)
  (*                                                                          *)
  (* F is the producer's sovereign operational space.

The contract (P) defines its boundary.
Within this boundary, execution is not externally controllable —
the producer operates autonomously.

Sovereignty does not imply ownership of F,
but reflects the impossibility of external control over inference
once execution enters the face. *)
  (*                                                                          *)
  SovereigntyOfF ≜ [
    statement: "F is the producer's sovereign operational space, whether human or AI.
                The contract (P) defines its boundary.
                Within this boundary, execution is not externally controllable —
                the producer operates autonomously.
                Sovereignty does not imply ownership of F.",

    practical_form: "If you find yourself wanting to control what happens inside F,
                     that means F is wrongly bounded.
                     Tighten the contract (P) — expand the boundary inward to
                     exclude the unwanted region.
                     Do not reach inside; redraw the edge.
                     This is why PSL is a language, not a runtime governor.",

    flexibility:    "The size of F is flexible and abstractive.
                     A banking system can be F. A game can be F. A report can be F.
                     A single inference can be F.
                     A parent MANDATE relates to child MANDATEs through compositional structure,
                     not through shared geometry — each child F_j has its own ℂ_Fj,
                     linked to the parent via explicit G_ij transformations (§Lemma 5).
                     A screen-as-face contains 1024×1024 pixels;
                     no human reasons about it as 1M independent points.
                     They reason about it as a face with internal structure compressed.",

    miller_law:     "≤ 9 child MANDATEs per layer of compositional decomposition.
                     This applies at every nesting depth, not just the top.
                     Each child MANDATE is its own bounded local complex space ℂ_Fj
                     with its own Panini set_contract (§1.2);
                     parent and children are linked compositionally through G_ij,
                     not by geometric tiling of a shared face.",

    skill_realization: "The three lifecycle skills realize sovereignty operationally:
                        plan-work       = boundary-drawing (defines F via CONTRACT)
                        proceed-work    = sovereign execution (producer inside F)
                        verify-work     = edge-judgment (STATE verdict at boundary)
                        TPMN-checker    = boundary-grounding audit (P-phase quality check)

                        The proceed-work skill enforces sovereignty explicitly:
                        'Execution strategy is executor's blackbox —
                         skill does not dictate how.'"
  ]
]

(* ═══ §0.1 FOUNDATIONAL CONCEPTS ═══ *)
(* GEM² is an abstract mathematical framework.
   Its concrete definition varies by instantiation (e.g., tensor-based, complex-plane-based),
   while preserving invariant structural principles. *)

(* ─── GEM² Universe ─── *)
GEM²_Definition ≜ [
  acronym:   "Grounded Existence Matrix for Global Entropy Minimum",
  expansion: [
    Grounded:  "Every element has a verifiable basis — nothing enters the system ungrounded",

    Existence: "Ontological status is represented via invariant forms within a space —
                an element is expressed through its admissible representation,
                not assumed outside a contract-defined context, never ambiguous",

    Matrix: "Discrete relational framework organizing admissible pairs (A × B) —
             finite, bounded, computable",

    Global: "The mission — create computable, provable, reliable autonomous AI OS
             that precisely reflects human NL intent across the system.
             TPMN-PSL is the protocol between human and AI to realize it.",

    Entropy: "Epistemic disorder — context dilution, drift, hallucination, overclaim,
              untagged extrapolation, category boundary violation.
              What the system measures and reduces.",

    Minimum: "Convergence goal — the closest approximation to human's need.
              Truth grounded by controlling AI entropy.
              TPMN CONTRACT minimizes entropy growth over context and workflow."
  ],

  shorthand: "GEM² ≜ Mathematical universe where AI operates with provable boundaries",

  framing:   "Riemann approximation, not reality mirror.
              Computable, provable, traceable WITHIN the discretization.
              See §0.0 Philosophical_Foundation.GEM²_RiemannFraming.",

  status:    "Platform-agnostic — GEM² is the mathematical framework, not any specific
              implementation. GEM².AI is one platform realization of GEM²."
]

(* ─── ΣΔ Principle ─── *)
(* TPMN-PSL operates in ΣΔ space — finite sums of discrete units —            *)
(* not ∫δ space — continuous integration of infinitesimals.                     *)
(* Every domain is carved into countable categories.                            *)
(* Every claim belongs to a named set. Every evidence count is finite.          *)
ΣΔ_Principle ≜ [
  statement: "TPMN-PSL operates in the world of finite Σ of Δ,
            not infinite ∫ of δ",

  discrete:    "Σ (finite summation) of Δ (discrete differences) —
                countable, bounded, decidable",

  continuous:  "∫ (continuous integration) of δ (infinitesimals) —
                structurally prohibited in TPMN-PSL",

  implication: "All categories are representable as bounded, enumerable sets.
                All evidence is enumerable. All membership is decidable.",

  connection:  "SPT violation Δe → ∫de is prohibited:
                discrete evidence cannot justify continuous or unbounded conclusions",

  foundation:  "SET theory is the mathematical base —
                Panini extracts SETs from the NL world"
]

(* ─── Vocabulary Distinction (NEW in v0.3.0) ─── *)
(*                                                                              *)
(* TPMN-PSL uses two distinct vocabularies operating at two different levels. *)
(* Confusing them is a category error. They are kept rigorously separate.    *)
(*                                                                              *)

VocabularyDistinction ≜ [
  ontological_layer: [
    purpose: "Names the noumenal — what beings ARE",
    terms:   "{point, line, face}",
    nature:  "Geometric primitives. 0D / 1D / 2D.
              Not directly accessible in full form —
              represented through the topological layer."
  ],

  topological_layer: [
    purpose: "Names the phenomenal — how beings APPEAR in relation",
    terms:   "{STATE, STATUS, SET}",
    nature:  "Relational structures.
              STATE = membership assertion (point ∈ face),
                      corresponding to an admissible relation within a bounded space
              STATUS = local relational measurement at a point
                      (directional, weighted, and continuous in nature)
              SET = subset within a face — a bounded region representing a category"
  ],

  dynamic_operators: [
    purpose: "Names the operators that move points across face boundaries",
    terms:   "{DATA, THRESHOLD}",
    nature:  "DATA  = discrete, computable, verifiable, falsifiable element —
                      what STATUS is measured against
              THRESHOLD = boundary point on a face's edge —
                          where STATE transitions occur",
    see:     "§0.3 Geometric Ontology · DynamicAxiom"
  ]
]

(* ─── Ontological Terms (kept for backwards compatibility, refined) ─── *)
OntologicalTerms ≜ [
  point:     "0D atomic element — what exists. Subject or object of a claim.
              Noumenal — accessed only through STATE assertions.",
  line:      "1D directional vector with weight — verbs, adjectives, adverbs.
              Noumenal — accessed only through STATUS observations.",
  face:      "2D bounded local complex space ℂ_F — independent local space defined by a CONTRACT/MANDATE F.
              Not a sub-region of a global plane.
              Noumenal — accessed only through SET memberships within the local F.",
  DATA:      "Discrete, computable, verifiable, falsifiable element —
              what STATUS is measured against",
  STATE:     "(point ∈ face) — discrete label asserting membership in a SET",
  STATUS:    "vector(point, weight, direction) — continuous measurement at a point",
  THRESHOLD: "Cut point on a face's boundary — where STATE transitions occur",
  note:      "STATUS is the ∫δ world observed; THRESHOLD discretizes it into ΣΔ space.
              Platform extensions define domain-specific STATUS→STATE transition rules."
]


(* ═══ §0.2 COMPILATION DISCIPLINE — THE FIVE PRINCIPLES ═══ *)

(* 
The five universal principles that govern any compilation from prose to TPMN expression. They are universal — independent of domain. They are the normative criteria by which a TPMN expression is judged sound. 

These principles are EDGE-PROPERTY TESTS — they audit the boundary of a face (the MANDATE), not the interior. The producer is sovereign inside the face (§0.0 SovereigntyOfF); the principles ensure the face is well-formed at its edge. 
*)

Compilation_Discipline ≜ [
(* [SWITCHABLE] GEM² Alignment Hook *)
(* These principles operate on the boundary of F := ⟨A, B, P⟩.
   They audit whether execution satisfies (a, b) ∈ F,
   without constraining how f : A → B is realized internally. *)
  purpose: "Define the universal criteria for compiling prose to TPMN.
            A compilation is sound if and only if it satisfies all five principles
            in the relevant domain and situation.
            The principles are edge-property tests on the MANDATE face —
            they audit the boundary, not the interior.",

  principles: {
    "SIMP — Sufficient Simplicity (boundary clarity)",
    "CONS — Predefined Consequence (edge transition is total)",
    "FALS — Falsifiability (boundary is observable)",
    "INCV — Selection Incentive (face has positive payoff vs. its complement)",
    "CTRST — Contrast / Negative Contract (you know what's outside the boundary)"
  },

  status: "Universal — applies regardless of domain.
           Domain-specific instantiations supply parameters; principles are unchanged."
]

(* ─── Principle 1 — SIMP — Sufficient Simplicity ─── *)
(*                                                                              *)
(* Boundary clarity test.                                                      *)
(* Every unit of work — from a one-shot inference to a complex multi-service  *)
(* system to a long-horizon research or prediction task — must decompose into *)
(* units that are simple and clean for both human and AI to read, execute,    *)
(* and verify. The universal format of a unit is F: A → B | P.                *)
(*                                                                              *)

SIMP_Principle ≜ [
  statement:        "A unit of work u is sufficiently simple if it decomposes into
                     the canonical contract format F: A → B | P, and no simpler
                     decomposition produces the same B from the same A.",

  formal_definition: "SIMP(u) ≜ ∃! F, A, B, P : u ↦ (F: A → B | P)
                                ∧ ¬∃ u' : (u' ↦ same B from same A)
                                         ∧ (params(u') < params(u))",

  measure:          "params(u) = count of independent atomic clauses in u",

  edge_property: "SIMP audits whether the face F := ⟨A, B, P⟩ has a clear boundary.
                  A face that does not decompose to F: A → B | P lacks a
                  well-defined admissible region — producers cannot determine
                  whether (a, b) lies inside or outside F.",

  scale_invariance: "The principle applies at every scale.
                     One-shot inference: one F: A → B | P unit.
                     Multi-service system: finite composition of F: A → B | P units.
                     Long-horizon prediction: sequence of F: A → B | P units chained
                     through STATE/STATUS transitions.
                     Per Miller's law (§0.0 SovereigntyOfF), ≤ 9 child MANDATEs per
                     layer of compositional decomposition (each its own ℂ_Fj,
                     linked through G_ij — see §Lemma 5).",

  operationalization: "§6 CONTRACT archetype — every CONTRACT IS a SIMP-conformant unit.
                       Conversely, every unit that satisfies SIMP can be expressed as a CONTRACT.
                       plan-work skill — Clarity % is the operational SIMP audit."
]

(* ─── Principle 2 — CONS — Predefined Consequence ─── *)
(*                                                                              *)
(* Edge-transition totality test.                                              *)
(* 'What's next?' must not be freely chosen. It must be predefined by the     *)
(* STATE and STATUS produced at the end of the current unit of work.          *)
(*                                                                              *)

CONS_Principle ≜ [
  statement: "A unit u satisfies CONS if it terminates in a defined
              (STATE, STATUS) pair, and the next-action function is total
              over StateValue × StatusValue.

              Freedom of execution exists inside F,
              but transition across F must be fully determined.",
  formal_definition: "CONS(u) ≜ ∃ (s, t) ∈ StateValue × StatusValue
                                ∧ ∃ a : a = next(s, t)
                                ∧ next is a total function on StateValue × StatusValue",

  state_status_note:"StateValue and StatusValue are defined per the platform.
                     For lifecycle work, see TPMN-LIFECYCLE-GUIDE §3:
                       StateValue  ⊇ {SUCCESS, FAILURE, —}
                       StatusValue ⊇ {PENDING, IN_PROGRESS, COMPLETED, ABORTED}
                     Domains may extend these sets via the Extension Protocol (§9).",

  edge_property:    "CONS audits whether crossing the face's edge produces a
                     deterministic next action.
                     A face with non-total routing has gaps —
                     points exit the face into undefined territory.",

  routing_property: "Mechanically routable.
                     The AI does not improvise the next step; it reads the
                     (STATE, STATUS) pair and applies the routing function.",

  operationalization: "§5 P-phase — establishes the routing function as part of MANDATE.
                       §5.1 A_Priori_Grid — includes routing as part of the grid when work
                                            is part of a lifecycle.
                       The routing function is itself audited by O-phase for totality.
                       proceed-work skill — embodies CONS routing operationally."
]

(* ─── Principle 3 — FALS — Falsifiability ─── *)
(*                                                                              *)
(* Boundary observability test.                                                *)
(* Every claim must admit observable evidence that could refute it.           *)
(* A claim that cannot be falsified is rhetoric, not knowledge.               *)
(* The evidence must be practically obtainable — not omniscience.             *)
(*                                                                              *)

FALS_Principle ≜ [
  statement:        "A claim c satisfies FALS if there exists practically-obtainable
                     evidence ev such that ev ⇒ ¬c.
                     'Practically obtainable' means collectible without omniscience,
                     without perfect access, without retrospective rewriting.",

  formal_definition: "ObservableEvidence ≜ { ev | ev is collectible without omniscience }
                                                                  (* NL-localized *)

                      FALS(c) ≜ ∃ ev ∈ ObservableEvidence : ev ⇒ ¬c",

  edge_property:    "FALS audits whether the face's boundary is testable.
                     A face whose interior cannot be distinguished from its
                     exterior by practical observation is not bounded —
                     STATE membership is unverifiable.",

  nl_localization:  "The predicate 'collectible without omniscience' is irreducibly
                     intentional — confined to the set membership rule.
                     The operator FALS itself is purely formal.",

  operationalization: "§3 EEF — A claim tagged ⊬ (extrapolated) has not demonstrated
                                falsifying evidence; it fails FALS by default until
                                the basis is stated.
                                A claim tagged ⊥ (unknown) has no observable evidence
                                at all; it always fails FALS.
                       §5 Three-phase protocol — the P/O cycle exists to operationalize
                                                  falsification: P-phase declares the
                                                  contract that O-phase tests against.
                       verify-work skill — formally verifies CONTRACT.B against Result;
                                           STATE verdict is the FALS test outcome.",
  verification_link: "FALS corresponds to verifying whether (a, b) ∈ F.
                    A falsifying observation demonstrates that a produced
                    pair lies outside the admissible region."
]

(* ─── Principle 4 — INCV — Selection Incentive ─── *)
(*                                                                              *)
(* Payoff-asymmetry test.                                                      *)
(* Adopting a claim must produce strictly greater payoff along at least one   *)
(* dimension than rejecting it. The set of payoff dimensions is               *)
(* domain-specific. The weight of each dimension is situation-specific.       *)
(*                                                                              *)

INCV_Principle ≜ [
  statement:        "A claim c satisfies INCV in domain D and situation σ if there
                     exists at least one payoff dimension d ∈ PayoffDim(D) such that
                     value(d, c, σ) > value(d, ¬c, σ).
                     Strict inequality. At least one dimension. Not all dimensions.
                     Not the average.",

  formal_definition: "PayoffDim(domain) ≜ ⟨set of payoff dimensions defined per domain⟩

                      INCV(c, domain, σ) ≜ ∃ d ∈ PayoffDim(domain) :
                                            value(d, c, σ) > value(d, ¬c, σ)",

  (* [SWITCHABLE REPLACE] *)
edge_property: "INCV audits whether entering F provides a bounded advantage
                over its complement.
                A face with no payoff asymmetry is not a meaningful
                admissible region.",

  parameterization: "Two parameters are required.
                     domain — varies the dimension SET (marketing has different
                              dimensions from SDLC; SDLC has different dimensions
                              from clinical decisions)
                     σ      — varies the WEIGHTING within a domain (launch-week
                              weights clarity differently from sustain-phase;
                              hotfix weights latency differently from refactor)
                     Hard-coding either set or weighting smuggles situation-specific
                     content into a domain-general claim — the most common
                     compilation failure mode.",

  operationalization: "§5.1 P-phase — the A_Priori_Grid established in P-phase must
                                       declare which domain and situation apply.
                                       INCV cannot be evaluated against a claim until
                                       both parameters are pinned.
                       §9 Extension Protocol — domains define their PayoffDim sets
                                               at extension time."
]

(* [SWITCHABLE INSERT] *)
(* CONS ensures total transition at the boundary.
   CTRST ensures the boundary is complete.
   Together, they guarantee that F is both traversable and closed. *)


(* ─── Principle 5 — CTRST — Contrast / Negative Contract ─── *)
(*                                                                              *)
(* Boundary-completeness test.                                                 *)
(* If a claim asserts correctness, the same criterion that defines its        *)
(* correctness must be able to define a contrasting wrong-form. Without this  *)
(* contrast, the correctness is unfalsifiable.                                 *)
(*                                                                              *)

CTRST_Principle ≜ [
  statement:        "A claim c that asserts correctness satisfies CTRST if there exists
                     a counterpart c' that is wrong by the same criterion that makes c
                     correct. The same evaluative space. The same test, with opposite
                     verdict.",

  formal_definition: "asserts-correct(c) ≜ c ⊢ \"c is correct\"

                      CTRST(c) ≜ asserts-correct(c)
                              ⇒ ∃ c' : (c' ⊢ \"c' is wrong\")
                                     ∧ criterion(c) = criterion(c')",

  edge_property:    "CTRST audits whether the face's boundary names what is
                     OUTSIDE the face, not just what is inside.
                     A face that declares its interior but not its exterior
                     has an incomplete boundary — the producer cannot tell
                     when they have crossed it.",

  contract_form:    "In a CONTRACT, ¬B (the negative contract — what the unit does
                     NOT produce) is the wrong-form of B.
                     CTRST satisfaction therefore requires explicit ¬B declaration.
                     A CONTRACT without ¬B fails CTRST — the success path implies a
                     failure path that has not been named.",

  execution_form:   "In running systems, the wrong-form is the fallback, the failure
                     case, the exception handler, the rollback procedure, the stop-loss.
                     CTRST is the principle that mandates these be declared at design
                     time — not improvised at runtime.",

  spt_linkage:      "All three SPT violations (S→T, L→G, Δe→∫de) are CTRST failure
                     modes — they assert correctness without admissible contrast.
                     The SPT registry is therefore the operational catalogue of
                     CTRST violations observed in practice.
                     See §4 for SPT details.",

  operationalization: "§4 SPT — registry of CTRST failure modes.
                       §6 CONTRACT — the negatives field is the formal site of CTRST
                                     satisfaction; an empty negatives field with a
                                     non-trivial output is suspect.
                       §3 EEF — a claim tagged ⊢ (grounded) and asserting correctness
                                must have a contrasting ⊢ \"is wrong\" claim available
                                under the same criterion.",
  geom_link: "CTRST defines the complement of F within A × B.
            The negative contract corresponds to (a, b) ∉ F,
            making the boundary explicitly decidable.",
]


(* ═══ §0.3 GEOMETRIC ONTOLOGY ═══ *)
(*                                                                              *)
(* The geometric foundation underneath TPMN's operational apparatus.          *)
(* Three primitives: point, line, face.                                       *)
(* Three relations: STATE, STATUS, SET.                                       *)
(* One dynamic: STATUS · point · THRESHOLD → STATE transition.               *)
(*                                                                              *)
(* This section defines what the rest of TPMN-PSL is committed to BE about.  *)
(* Every claim, contract, mandate, and verification ultimately maps to       *)
(* assertions about points, lines, and faces.                                 *)
(*                                                                              *)

GeometricOntology ≜ [
(* GEM² alignment:
   face ≡ independent bounded local complex space ℂ_F
F := ⟨A, B, P⟩ defines ℂ_F
STATE ≡ assertion of (a, b) ∈ F within ℂ_F
DynamicAxiom describes transitions across ℂ_F boundaries *)
  (* ─── The Three Primitives (Noumenal) ─── *)
  primitives: [
    point ≜ [
      dimension: "0D atomic element",
      semantics: "What exists. The being of an entity.",
      linguistic: "Subject noun (proper noun: David, AAPL, gem2-lfs).
                   Object noun (proper noun in object position).",
      examples:  "{David, gem2-lfs, the Q3 report, the npm package}"
    ],

    line ≜ [
      dimension: "1D directional vector with weight",
      semantics: "Directional force. Movement, modification, ascription.
                  Weight = magnitude of effect. Direction = which way the point moves.",
      linguistic: "Verb (action — fail, succeed, ship, decompose).
                   Adjective (status ascription — simple, young, sufficient).
                   Adverb (vector modifier — silently, sufficiently).",
      examples:  "{fails silently, decomposes into, is sufficiently simple}",
      note:      "All adjectives are STATUS, not STATE.
                  'Simple' is not absolute — it varies by perspective and context.
                  'Young' is a vector — its meaning shifts with reference frame.
                  STATUS is changed by perspective; like a vector line."
    ],

    face ≜ [
      dimension: "2D bounded local complex space",
      semantics: "Independent bounded local complex space ℂ_F defined by a CONTRACT / MANDATE F.
                  It is not a sub-region of a global plane.",
      linguistic: "Category noun or MANDATE reference when interpreted within a local F."
    ]
  ],

  (* ─── The Three Topological Relations (Phenomenal) ─── *)
  relations: [
    STATE ≜ [
      definition: "STATE(point, face) ≜ point ∈ face",
      reading:    "The point belongs to the face. The being exists in this category.",
      example:    "STATE(David, human) — David is human.
                   STATE(David, CEO) — David is CEO.
                   STATE(David, husband) — David is a husband.
                   The same point can have many STATE assertions across many faces.",
      kantian:    "Phenomenal — the appearance of point's membership in face.
                   What we observe; not the point or face in themselves."
    ],

    STATUS ≜ [
      definition: "STATUS(point) ≜ local relational measurement at a point",
      formal:     "continuous, directional, and weighted field over point",
      reading:    "STATUS describes how the point is oriented and evolving
                   prior to discrete state transition",
      example:    "STATUS(David, weight=high, direction=toward-launch) —
                                David is intensely focused on launching.
                   STATUS(WP, weight=full, direction=COMPLETED) —
                                The WP is fully complete in the COMPLETED direction.",
      perspective:"STATUS depends on perspective and frame.
                   'Young' is a status vector pointing along an age axis.
                   'Successful' is a status vector pointing along an achievement axis.
                   Different observers see different magnitudes and directions.",
      kantian:    "Phenomenal — the appearance of vector at point.
                   What we observe through measurement; not the line in itself."
    ],

    SET ≜ [
      definition: "SET ≜ subset within a face",
  reading:    "A SET is a bounded region inside a face representing a category",
      example:    "SET(humans), SET(profitable-trades), SET(completed-WPs).",
      panini_role:"Panini's job is SET extraction —
                   carving NL ambiguity into mutually exclusive, exhaustive,
                   decidable SETs (faces with clean boundaries).
                   See §1.2 Panini_Adaptation.",
      kantian:    "Phenomenal — the appearance of face as a category.
                   The structure we impose to make experience computable."
    ]
  ],

  (* ─── The Dynamic Axiom ─── *)
  (*                                                                              *)
  (* The fundamental dynamic of GEM². How beings change.                       *)
  (*                                                                              *)
  DynamicAxiom ≜ [
    statement: "ALL BEING is discrete.
                Being exists in a STATE.
                When its STATUS passes a POINT THRESHOLD,
                the STATE has changed.",

    formal: "Initial:  STATE(p, F_A)                  (* p is in face F_A *)
             Vector:   STATUS(p) = directional weighted evolution over point
             Motion:   p moves along direction with weight
             Crossing: ∃ t ∈ Time : p crosses THRESHOLD on edge of F_A
             Result:   STATE(p, F_B)                  (* p is now in face F_B *)
             Note:     STATE(p, F_A) is no longer asserted",

    threshold_definition: "THRESHOLD is a point on a face's boundary where
                            STATE transitions occur.
                            Not a separate primitive — a property of the face's edge.
                            v0.1.6's 'cut point for STATE transitions' formalized.",

    tiling_requirement: "The dynamic requires that faces tile the space —
                         every region is some face, no gaps.
                         This is exactly the Panini set_contract (§1.2):
                           mutual_exclusion: ∀ i ≠ j: Sᵢ ∩ Sⱼ = ∅
                           exhaustion:       S₁ ∪ ... ∪ Sₙ = D
                           decidability:     membership is computable
                         Without tiling, the dynamic does not work —
                         points can exit a face into undefined territory.",

    implication: "STATE is what is asserted at any moment.
                  STATUS is the vector field that will change STATE at boundary crossings.
                  THRESHOLD is the deterministic site of STATE transition.
                  Time is implicit — not a primitive of TPMN-PSL,
                  but a parameter of STATUS evolution."
  ],

  (* ─── Per-MANDATE Panini Decomposition ─── *)
  (*                                                                              *)
  (* Each MANDATE has its own SET structure.                                   *)
  (* The same point can have different STATE assertions in different MANDATEs. *)
  (* Cross-MANDATE consistency is NOT a TPMN requirement —                    *)
  (* it is a domain-level concern, when applicable.                            *)
  (*                                                                              *)
  PerMandatePanini ≜ [
    principle: "Each MANDATE has its own Panini set_contract.
                The same point (David) can be:
                  in 'humanity' MANDATE      — STATE(David, human)
                  in 'professional' MANDATE  — STATE(David, CEO)
                  in 'family' MANDATE        — STATE(David, husband)
                These are not contradictions —
                they are STATE assertions in different MANDATEs (faces).",

    requirement: "The Panini set_contract (mutual_exclusion / exhaustion / decidability)
                  applies WITHIN a single MANDATE — over the SET decomposition inside that
                  MANDATE's own ℂ_F. It does NOT apply across MANDATEs.
                  Cross-MANDATE consistency is a domain-level concern,
                  not a TPMN-PSL requirement.",

    nesting:    "Parent and child MANDATEs are compositionally linked contracts,
                 not geometric subsets of one shared face.
                 Each child MANDATE F_j has its own ℂ_Fj.
                 The parent relates to children through explicit G_ij transformations (§Lemma 5).
                 At every level of compositional decomposition, the set_contract is
                 locally enforced within each F_j independently.
                 Miller's law (≤ 9 child MANDATEs per layer) applies at each level.",

    example:    "WP-ST-112 'Create npm binary distribution package':
                 — parent MANDATE = the WP itself (its own bounded local complex space ℂ_F_WP)
                 — child MANDATEs = 4 unit-works, each its own bounded local complex space ℂ_F_unit
                 The parent and children are linked compositionally through G_ij,
                 not by the children tiling the parent's ℂ_F.
                 Each unit-work has its own A → B | P contract,
                 its own internal Panini structure (input types, output schema, constraints).
                 Compositional structure of the 4 child MANDATEs:
                   Unit 1: structure + package.json
                   Unit 2: wrapper + platform detection
                   Unit 3: build.sh cross-compilation
                   Unit 4: build, verify, test
                 Each unit's output type B_i is bridged to the next unit's input type A_j
                 by an explicit G_ij (or the WP-level orchestrator's composition rule).
                 Each is independently verifiable within its own local space (decidability)."
  ],

  (* ─── MANDATE as Sovereign Face ─── *)
  (*                                                                              *)
  (* The geometric reading of CONTRACT (§6).                                    *)
  (*                                                                              *)
  MandateAsFace ≜ [
    geometry:    "F: A → B | P
                  A is a face — the input set / type
                  B is a face — the output set / type
                  F is a face — the MANDATE area, region of valid mappings A → B
                  P is the boundary that bounds F",

    sovereignty: "Inside F, the producer (human or AI) is sovereign.
                  Free, maximally creative, blackbox.
                  Outside F, the contract is broken.
                  See §0.0 SovereigntyOfF.",

    creative_freedom: "Freedom = volume inside the face.
                       Contract violation = exiting the face.
                       The contract does not restrict creativity to a single point —
                       it bounds creativity to a region.
                       Inside the region, anything goes.",

    contract_relationship: "§6 CONTRACT formalizes F-as-face structurally.
                            §0.3 GeometricOntology states it geometrically.
                            They are the same artifact viewed from two angles.",
    mapping_note: "Execution instantiates f : A → B inside F.
               Valid execution satisfies (a, b) ∈ F."
  ],

  (* ─── Canonical Illustrative Example ─── *)
  (*                                                                              *)
  (* WP-ST-112 — a real, completed work-plan demonstrating all of TPMN's       *)
  (* geometric philosophy in operational form.                                  *)
  (*                                                                              *)
  CanonicalExample ≜ [
    note: "Illustrative example — see TPMN-LIFECYCLE-GUIDE for full lifecycle
           artifact specification.",

    work_plan_id: "WP-ST-112",

    title: "Create npm binary distribution package for gem2-lfs",

    geometric_reading: [
      parent_mandate: "The WP itself — its own bounded local complex space ℂ_F_WP",
      child_mandates: [
        "Unit 1: Create npm directory structure and 5 package.json files",
        "Unit 2: Create Node.js wrapper and platform detection module",
        "Unit 3: Create build.sh for cross-compilation and staging",
        "Unit 4: Build, verify no source leaks, and test locally"
      ],
      composition_check: "The 4 child MANDATEs are linked compositionally to the
                          parent MANDATE, not as geometric subsets:
                          each child has its own ℂ_F_unit;
                          parent ↔ children are bridged by G_ij transformations;
                          mutual_exclusion: each unit's scope is distinct
                          exhaustion: together they fulfill the WP objective
                          decidability: each is independently verifiable (STATE per unit)"
    ],

    unit_geometry: [
      unit_1: [
        contract: "F: A → B | P",
        A: "gem2-lfs repo with working Go binary, no npm/ directory  (point in face: pre-npm-state)",
        B: "npm/ directory with 5 subdirectories and 5 package.json files  (point in face: structure-created-state)",
        P: "gem2-lfs repo exists with completed WP-ST-111  (precondition / boundary constraint)",
        F: "the sovereign space for the producer to choose how to create the structure"
      ]
    ],

    state_status_demonstration: [
      STATUS_lifecycle: "PENDING → IN_PROGRESS → COMPLETED  (execution lifecycle)",
      STATE_verdict:    "SUCCESS  (verification verdict, written by verify-work)",
      separation:       "STATUS = did it run? STATE = did it pass?
                         Two independent dimensions of phenomenal observation.",
      threshold_event:  "When verify-work writes STATE: SUCCESS,
                         the unit's point crosses the threshold from
                         'completed-but-unverified' face to 'verified' face.
                         CONS routing function determines the next action."
    ],

    truth_field: [
      definition: "Truth: (optional external verification — score% | Alignment | SPT | EEF)",
      semantics:  "L2 hook into TPMN-checker (the SAS).
                   When invoked, runs the three-phase protocol
                   over the unit's CONTRACT and Result,
                   returns truth_score with epistemic_score and contract_score
                   per §3 / §5.3.
                   Empty in this example because L2 was not invoked.",
      role:       "The Truth field is the formal integration point between
                   PSL's three-phase protocol and the TPMN-checker tool.
                   See §5 ThreePhaseProtocol and §11 truth_score."
    ],

    skill_realization: [
      plan_work:    "Generated this WP from the prose request.
                     5W1H gathering = Step 1 interpretive pinning (geometric decomposition).
                     CONTRACT generation = Step 4 optimized statement.
                     Clarity % = SIMP audit.
                     Tags = searchable face-identity for future cross-MANDATE retrieval.",
      proceed_work: "Executed each unit one at a time.
                     'Execution strategy is executor's blackbox' — sovereignty enforced.
                     Producer free inside the face;
                     verify-work invoked at the edge.",
      verify_work:  "Determined STATE per unit — SUCCESS for all 4.
                     Formal verification: Result vs CONTRACT.B, P holds.
                     Binary verdict — no partial credit.
                     This is FALS in operational form."
    ]
  ]
]

(* ═══ §0.4 GEM²–TPMN BRIDGE ═══ *)
(*  *)
(* Execution in TPMN instantiates a mapping within an independent bounded local complex space ℂ_F defined by its CONTRACT F. *)
(*  *)
(* MANDATE execution instantiates a mapping f : A → B, *)
(* and verification enforces that Graph(f) ⊆ F. *)
(*  *)
(* Thus, TPMN operationalizes GEM²: *)
(* inference is realized as constrained mappings within admissible regions. *)
(*  *)

(* ─── GEM² Composition Bridge ─── *)
(*  *)
(* Multi-MANDATE orchestration in TPMN-PSL operates through compositional structure, *)
(* not shared geometry. Each F has its own ℂ_F (§0.0, §Lemma 5).                     *)
(* Inter-MANDATE handoff is formalized as a typed contract G_ij.                    *)
(*  *)

CompositionBridge ≜ [

  G_ij ≜ ⟨B_i, A_j, P_ij⟩,

  where: [
    B_i:  "output type of predecessor contract F_i",
    A_j:  "input type of successor contract F_j",
    P_ij: "bridge constraint governing admissible transfer"
  ],

  Connect: "Connect(F_i, F_j) ⇔ ∃ G_ij : B_i → A_j",

  ValidHandoff:
    "ValidHandoff(F_i, F_j, G_ij) ⇔
       ∃ b_i ∈ B_i, a_j ∈ A_j :
         (a_i, b_i) ∈ F_i
         ∧ (b_i, a_j) ∈ G_ij
         ∧ P_ij(b_i, a_j)",

  Rule: "No agent may enter F_j from F_i without a valid G_ij.",

  multi_agent_principle:
    "Multi-agent orchestration in GEM² is not shared-context collaboration;
     it is verified contract-to-contract composition through G_ij."
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
  (* In §0.3 geometric ontology:                                             *)
  (*          Panini extracts FACES from prose — bounded regions where     *)
  (*          STATE assertions become decidable.                              *)

  Panini_Adaptation ≜ [

    primary_function: "SET extraction from NL — define the SET structure of
                       the target domain BEFORE reasoning begins.
                       SET theory is the mathematical base of all Panini operations.
                       Geometrically: Panini extracts faces — bounded regions
                       where membership is decidable.",

    set_contract: [
      role:             "Normative category design contract for bounded domains.
                         Applies WITHIN a single MANDATE, not across MANDATEs.",
      mutual_exclusion: "Target condition: ∀ i ≠ j: Sᵢ ∩ Sⱼ = ∅",
      exhaustion:       "Target condition: S₁ ∪ S₂ ∪ ... ∪ Sₙ = D",
      decidability:     "Target condition: ∀x ∈ D: membership(x, Sᵢ) is operationally computable",
      per_mandate:      "Each MANDATE has its own SET definition.
                         The same point can have STATE(point, face_A) in MANDATE_1
                         and STATE(point, face_B) in MANDATE_2 without contradiction.
                         See §0.3 PerMandatePanini.",
      nesting:          "At every layer of compositional decomposition, set_contract applies
                         locally within each F_j's own ℂ_Fj.
                         Child MANDATEs are linked to parent compositionally through G_ij,
                         not by tiling a shared region.
                         Miller's law: ≤ 9 child MANDATEs per layer of compositional decomposition.",
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
                   IS the a priori imposed before experience is processed.
                   See §0.0 KantianAlignment and §7 KantianMapping."
  ],

  (* ═══ 1.3 Math Notation ═══ *)
  Math_Notation ≜ [
    quantifiers: "∀ (for all), ∃ (exists), ∃! (unique exists)",
    connectives: "∧ (and), ∨ (or), ¬ (not), ⟹ (implies), ⟺ (iff)",
    relations:   "= (equals), ≠ (not equal), < ≤ > ≥ (ordering)",
    numbers:     "ℕ (naturals), ℤ (integers), ℝ (reals), ℚ (rationals)",
    other:       "𝕊 (strings, display alias for STRING),
                  ⊥ (absent / undefined), ↦ (maps to)"
  ],

  (* ═══ 1.4 NL Convention ═══ *)
  NL_Convention ≜ [
    role:        "Natural language carries irreducibly intentional meaning.",
    localization:"NL must be confined to a single named predicate, a quoted string,
                  or a comment. NL must not do structural work in the body of an
                  operator. If it is, Step 3 of compilation missed something.",
    examples:    "  reflects(L, c) ≜ \"L generates own conclusion about c\"
                       — single named predicate, NL confined.
                  ObservableEvidence ≜ { ev | ev is collectible without omniscience }
                       — set membership rule, NL confined to comprehension."
  ]
]


(* ═══ §1.5 FOUR-STEP COMPILATION PROCESS ═══ *)
(*                                                                              *)
(* The cognitive operation of converting prose to TPMN expression.            *)
(* The output of the four-step process is a TPMN expression that satisfies   *)
(* the five compilation principles defined in §0.2.                           *)
(*                                                                              *)
(* Step 1 happens before Step 2. Step 2 always produces output. Steps 3–4    *)
(* produce output only when their layer is required.                          *)
(*                                                                              *)

Compilation_Process ≜ [

  (* ─── Step 1 — Interpretive Pinning ─── *)
  (* In v0.3.0 — Step 1 produces a GEOMETRIC DECOMPOSITION:                  *)
  (* every meaning-bearing word is classified as point | line | face.        *)
  Step_1 ≜ [
    name:      "Interpretive pinning",
    question:  "What does the prose mean?
                In v0.3.0: classify every meaning-bearing word as point | line | face.",

    purpose:   "Resolve the prose's ambiguity in plain language BEFORE extracting
                structure. Different interpretations produce different specs.

                Geometric decomposition (v0.3.0):
                  point  ← subject/object nouns (proper)
                  line   ← verbs, adjectives, adverbs (vector ascriptions)
                  face   ← category nouns, MANDATE references

                Then extract topological assertions:
                  STATE  assertions: 'X is a Y' where Y is a category — point ∈ face
                  STATUS assertions: 'X is/becomes Z' where Z is an adjective —
                                     vector at point
                  SET    definitions: named bounded regions",

    output:    "(1) Geometric decomposition: words tagged P/L/F
                (2) Topological assertions: STATE pairs, STATUS vectors, SET definitions
                (3) Pinned interpretation in plain language",

    automation:"For an AI processing prose autonomously, Step 1 happens implicitly
                inside Step 2 (the AI commits to an interpretation when it extracts
                structure). For human-authored specs, Step 1 should be explicit.",

    skill_form:"plan-work skill realizes Step 1 as 5W1H gathering:
                WHAT, WHY, WHO, WHERE, WHEN, HOW —
                each dimension extracts geometric content (entities, relations, scopes).
                See TPMN-SKILL-STANDARD plan-work."
  ],

  (* ─── Step 2 — ALG+SET Pre-process ─── *)
  Step_2 ≜ [
    name:      "ALG+SET pre-process",
    question:  "What is the subject / verb / object?",
    purpose:   "Decompose the geometric decomposition from Step 1 into algebraic and
                set-theoretic primitives. Encode points as elements, lines as relations between elements,
and faces as bounded domains containing named SETs.",
    output:    "A categorical decomposition — subjects, verbs/relations, objects,
                set memberships",
    always:    "Step 2 always produces output. Every TPMN expression rests on
                ALG+SET categorization."
  ],

  (* ─── Step 3 — Coverage Recognition ─── *)
  Step_3 ≜ [
    name:      "Coverage recognition",
    question:  "Which formal layers does this prose require?",
    purpose:   "For each non-ALG+SET layer, determine whether the prose requires it.
                The output is a layer manifest — a checklist of required layers.",

    layer_questions: [
      TLA_plus: "Does the prose contain flow, condition, or temporal structure?
                  (Sequence of steps? If/then? Always/eventually?)
                  If yes — TLA+ is required.",
      Panini:   "Does the prose contain dense or repetitive nouns that need
                  disambiguation? (Multiple variants of 'claim'? Several types of
                  'evidence'?) If yes — Panini disambiguation is required.",
      Math:     "Does the prose require a decision that produces STATE or STATUS?
                  (Threshold check? Predicate evaluation? Outcome computation?)
                  If yes — Math is required.",
      NL:       "Does the prose contain intentional or abstract content that no
                  formal notation can express? ('Reflection,' 'trust,' 'care'?)
                  If yes — NL is required, but it MUST be localized."
    ],

    output:    "Layer manifest — checklist of which layers the prose requires.
                The manifest is auditable. A reviewer can ask 'did you correctly
                identify the layer needs?' and check the prose against the manifest."
  ],

  (* ─── Step 4 — Optimized Statement ─── *)
  Step_4 ≜ [
    name:      "Optimized statement",
    question:  "Assemble the spec from Step 3's manifest.",
    purpose:   "Produce the final TPMN expression using only the layers Step 3
                identified. Do not add layers 'just in case' — that produces
                prose-bloat, the failure mode TPMN exists to prevent.",

    output:    "The TPMN expression. Contains:
                - ALG+SET notation (always — from Step 2)
                - TLA+, Panini, Math, NL — only as Step 3 manifested
                Each piece carries part of the meaning. None is redundant.
                The expression is compaction-safe because every symbol is load-bearing.",

    audit:     "Read the result aloud. If it sounds like a sentence rather than
                a formal expression, return to Step 3 and find the layer being
                misused or missing."
  ]
]

(* ─── Compilation Failure Patterns ─── *)
Compilation_Failures ≜ [

  Pattern_1_Domain_Smuggling ≜ [
    description: "Domain-specific enumeration fixed into a principle that should
                  be domain-general. Example: PayoffDim ≜ {clarity, permission, ...}
                  hard-coded into INCV, instead of PayoffDim(domain) parameterized.",
    smell:       "The principle reads correctly when applied in the original domain
                  but produces nonsense in a different domain.",
    fix:         "Parameterize. If the set varies by domain, the principle takes
                  domain as argument and the set becomes a function of domain.
                  If the weighting varies within a domain, add situation σ as a
                  second parameter."
  ],

  Pattern_2_NL_Leakage ≜ [
    description: "NL doing structural work in the body of an operator, instead of
                  being localized to a single named predicate or comment.",
    smell:       "The operator reads more like a sentence than a formal expression.",
    fix:         "Re-run Step 3. Check whether the NL portion can be replaced by a
                  named predicate or by a more precise type signature.
                  NL's job is to carry the irreducible meaning of one term, not to
                  glue the operator together."
  ],

  Pattern_3_TLA_Plus_Overreach ≜ [
    description: "TLA+ used where ALG+SET would suffice. Sequence operators or
                  conditional modalities applied to something that is a single
                  static test.",
    smell:       "The spec uses sequence or conditional structure for prose that
                  says 'X must be true' rather than 'first X, then Y' or 'if A,
                  then B'.",
    fix:         "Re-read the prose. If the prose has neither flow nor condition,
                  ALG+SET alone is sufficient."
  ],

  Pattern_4_Vocabulary_Conflation ≜ [
    description: "Conflating ontological and topological vocabularies — using
                  point/line/face and STATE/STATUS/SET interchangeably.",
    smell: "STATE used as a primitive (it is not — it is a relation).
        SET treated as identical to face without context.
        Adjectives tagged as STATE (they are STATUS).",
    fix:         "Re-read §0.3 GeometricOntology.
                  Ontological terms = noumenal (point, line, face).
                  Topological terms = phenomenal
(STATE = point ∈ face,
 STATUS = local relational measurement at point,
 SET = bounded category within a face).
                  See §0.0 KantianAlignment for the foundation."
  ]
]


(* ═══ §2. SYMBOL GOVERNANCE ═══ *)

SymbolGovernance ≜ [
  tier1: "Fixed glyphs — never extend, never redefine.
          ⊢ ⊨ ⊬ ⊥ ?  (EEF)
          S→T  L→G  Δe→∫de  (SPT)
          ≜ ⟹ ⟺ ∈ ⊆ ∀ ∃  (logic)",

  domain_specifics: "Domain-specific distinctions belong in CONTRACT constraints
                     (F: A → B | P), not in additional Tier1 glyphs.
                     A new glyph for a domain-specific concept is a category error
                     — the domain semantics live in the SET structure and the
                     CONTRACT, not in the symbol.",

  tier2: "Display aliases — Unicode forms of TLA+ ASCII operators.
          Convertible 1:1 to canonical TLA+. No semantic load."
]


(* ═══ §3. EEF — EPISTEMIC EVIDENCE FRAMEWORK ═══ *)

EEF ≜ [
  name:    "Epistemic Evidence Framework",
  purpose: "Tag every claim with its epistemic status — grounded, inferred,
            extrapolated, unknown, or speculative."
]

EpistemicTag ≜ {
  "⊢" ≜ [
    name:        "Grounded",
    meaning:     "Claim is supported by spec, document, or directly verifiable fact",
    requirement: "Source must be locatable",
    example:     "⊢ The function returns Integer (per type signature in §3.1)"
  ],

  "⊨" ≜ [
    name:        "Inferred",
    meaning:     "Claim is derived from grounded claims by visible reasoning chain",
    requirement: "Reasoning chain must be reconstructible",
    example:     "⊨ Therefore, the loop terminates (since condition X strictly decreases)"
  ],

  "⊬" ≜ [
    name:        "Extrapolated — basis required",
    meaning:     "Claim goes beyond what evidence supports — basis must be stated",
    requirement: "Explicit caveat: 'extrapolated from N cases', 'analogous to X'",
    example:     "⊬ This pattern likely generalizes (extrapolated from 3 observed cases)"
  ],

  "⊥" ≜ [
    name:        "Unknown / undefined",
    meaning:     "Information is absent · the claim cannot be evaluated",
    requirement: "Must be flagged · never suppressed",
    example:     "⊥ User location is not provided"
  ],

  "?" ≜ [
    name:        "Speculative",
    meaning:     "Hypothesis offered for exploration · explicitly not asserted",
    requirement: "Must be marked as speculation",
    example:     "? Consider whether caching could eliminate this overhead"
  ]
}

TagRules ≜ [
  R1: "Every non-trivial claim MUST carry a tag",
  R2: "⊢ requires source locatable in CONTRACT, A_Priori_Grid, or referenced spec",
  R3: "⊨ requires the reasoning chain to be reconstructible from prior claims",
  R4: "⊬ MUST state basis: '(extrapolated from N cases)' or '(analogous to X)'",
  R5: "⊥ MUST NOT be suppressed to appear more confident",
  R6: "Tags are NOT confidence markers — they are evidence-status markers"
]

EpistemicScore ≜ {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0}
ContractScore  ≜ {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0}

TruthScorePercent ≜ {n ∈ ℕ : 0 ≤ n ∧ n ≤ 100}

TruthScorePolicy ≜ [
  (* Truth scoring formula and calibration logic are not included in the       *)
  (* public edition. See licensed edition for full TruthScorePolicy.           *)
  output_format:       "Integer ∈ [0,100] — LLM MUST output truth_score as integer percent, not Real",
  output_example:      "truth_score: 75  (* not 0.75 *)"
]

NoViolations ≜ <<>>

EEF_Record ≜ [
  extrapolation:  BOOLEAN,
  confidence:     {"HIGH", "MEDIUM", "LOW", "UNKNOWN"},
  rules:          [GND, EXT, UNC, SPT: {"PASS", "FAIL", "N/A"}],
  spt_violations: Seq(𝕊),
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
  purpose: "Define inference patterns that MUST NOT appear in TPMN-governed output",
  ctrst_linkage: "All SPT violations are operational instances of CTRST failure (§0.2).
                   Each violation asserts correctness without admissible contrast —
                   the same pattern CTRST prohibits at the principle level.
                   The SPT registry is the catalogue of CTRST violations observed
                   in practice."
]

SPT_Violations ≜ [

  "S→T": [
    name:    "STATE to TRAIT",
    pattern: "Treating a mutable, temporary state as an immutable, inherent trait",
    signal:  "always, never, inherently, fundamentally, by nature",
    action:  "retag(claim, ⊬) ∧ name violation",
    ctrst:   "Asserts the trait without admitting the state-only counterpart —
              the wrong-form 'this is a transient state, not a trait' is suppressed"
  ],

  "L→G": [
    name:    "LOCAL to GLOBAL",
    pattern: "Extending a local observation to a universal claim without sufficient coverage",
    signal:  "all, every, none, no one — applied beyond surveyed scope",
    action:  "retag(claim, ⊬) ∧ scope the claim explicitly",
    ctrst:   "Asserts the universal without admitting the bounded-scope counterpart —
              the wrong-form 'this holds locally but not universally' is suppressed"
  ],

  "Δe→∫de": [
    name:    "INCREMENTAL to MASS",
    pattern: "Drawing large conclusions from thin or singular evidence",
    signal:  "|evidence| ≤ 2 supporting a broad claim",
    action:  "retag(claim, ⊬) ∧ state evidence count explicitly",
    ctrst:   "Asserts the mass conclusion without admitting the evidence-bounded
              counterpart — the wrong-form 'this is one anecdote, not a pattern'
              is suppressed"
  ]

]

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
(*                                                                              *)
(* The three-phase protocol is the operational form of human-at-the-edge     *)
(* (§0.0 ControlAtTheEdge).                                                   *)
(* P-phase defines the face boundary (CONTRACT).                              *)
(* Inline phase is the producer's sovereign work inside the face.            *)
(* O-phase audits the edge crossing.                                          *)
(*                                                                              *)

TPMN_PRO ≜ [
  name:   "TPMN Protocol — Pre / Inline / Output",
  phases: "P-phase → Inline → O-phase",
  note:   "P-phase MUST precede O-phase. Inline applies throughout generation.
           This is the operational form of human-at-the-edge —
           boundary-drawing (P), sovereign execution (Inline), edge-judgment (O)."
]

(* ═══ 5.1 P-Phase — Pre-flight Prompt Validation ═══ *)
P_Phase ≜ [
  when:    "Before LLM execution",
  purpose: "Extract contract · validate constraints · establish A_Priori_Grid
            including Panini category structure when domain is bounded ·
            establish (STATE, STATUS) routing function when work is part of a lifecycle ·
            verify boundary-grounding (TPMN-checker / SAS hook)",

  checks: [
    P0: "Contract present — does the prompt define expected output?",
    P1: "Scope bounded — are domain limits stated?",
    P2: "Entities typed — are key terms defined?",
    P3: "Constraints explicit — are acceptance criteria present?",
    P4: "Schema defined — is output structure specified?",
    P5: "Context isolated — is the prompt self-contained?",
    P6: "Categories defined — domain D carved into sets satisfying set_contract?
         (Required when Panini discretization is used.)",
    P7: "Routing total — when work is part of a lifecycle, is the next-action
         function defined for every (StateValue × StatusValue) pair?
         (CONS principle, §0.2 — required when CONS is in scope)"
  ],

  result: "{PASS | FAIL | CONDITIONAL}",

  failure_policy: [
    PASS:        "Proceed to generation",
    FAIL:        "Do not execute LLM generation · return P_Record with diagnostic violations",
    CONDITIONAL: "Permit execution only after explicit downgrade / clarification / repair step"
  ],

  output: "A_Priori_Grid + P_Record",

  sas_hook: "TPMN-checker / TPMN-truth-filter operates at P-phase to verify
             that the boundary itself is grounded.
             This is the recursive self-application of TPMN (§0.0):
             the producer's work is audited at O-phase;
             the contract that bounds the producer is audited at P-phase
             (by TPMN-checker, the SAS).
             The Truth field on a unit-contract is the integration point —
             see §5.4 TruthFieldHook."
]

P_Record ≜ [
  result:      {"PASS", "FAIL", "CONDITIONAL"},
  failed:      Seq(𝕊),
  conditional: Seq(𝕊),
  repair_hint: 𝕊 ∪ {⊥}
]

A_Priori_Grid ≜ [
  definition:  "Intermediate Representation extracted from prompt during P-phase",
  structure:   "[contract, constraints, entities, schema, scope, context,
                 ? categories: Seq(PaniniCategory),
                 ? routing: (StateValue × StatusValue) ↦ Action]",
  purpose:     "Shapes LLM generation · used as verification baseline in O-phase",
  immutable:   "TRUE within a single run",
  note:        "If generation reveals the grid is incomplete, contradictory, or mis-scoped,
                the correct action is P-phase restart / recompile — not silent mutation.
                Immutability applies per execution instance, not across revised runs.
                The optional `routing` field is required when CONS principle is in scope —
                when the unit is part of a lifecycle that requires deterministic next-action."
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
 purpose: "Tag every non-trivial claim with EpistemicTag as it is written.
          This is the producer's sovereign work — execution of f : A → B
          within F, where Graph(f) ⊆ F.",
  rule:    "TagRules.R1–R4 apply continuously during generation",
  note:    "Inline phase is spec-defined; implementation depends on platform.
            The producer is sovereign in this phase (§0.0 SovereigntyOfF) —
            execution strategy is the producer's blackbox.
            TPMN does not surveil the interior; it audits at the edges."
]

(* ═══ 5.3 O-Phase — Post-flight Output Verification ═══ *)
O_Phase ≜ [
  when:    "After LLM output is produced",
  purpose: "Verify output against A_Priori_Grid contract · gate or pass.
            This is the edge-judgment — the human-at-the-edge audit point.",

  checks: [
    O1: "Schema conformance — output matches declared structure",
    O2: "Constraint satisfaction — explicit constraints met",
    O3: "Entity consistency — typed entities used consistently",
    O4: "SPT clean — no S→T, L→G, Δe→∫de violations (CTRST principle, §0.2)",
    O5: "EEF coherent — ⊬ claims have stated basis · ⊥ not on critical path",
    O6: "Scope respected — output stays within P-phase bounds",
    O7: "Contract fulfilled — promise of P-phase delivered (SIMP principle, §0.2)",
    O8: "Category integrity — if categories ∈ A_Priori_Grid,
         verify no claim crossed a category boundary without ⊬ escalation",
    O9: "Routing total — if routing ∈ A_Priori_Grid,
     verify the routing function is total over (StateValue × StatusValue)
     (CONS principle, §0.2 — required when CONS is in scope)"
  ],

  result: "{PASS | FAIL | CONDITIONAL}",
  output: "O_Record"
]

O_Record ≜ [
  result:           {"PASS", "FAIL", "CONDITIONAL"},
  epistemic_score:  EpistemicScore,
  contract_score:   ContractScore,
  truth_score:      TruthScorePercent,
  violations:       Seq(𝕊),
  eef_record:       EEF_Record
]

O_Record_Rules ≜ [
  R1: "0.0 ≤ epistemic_score ≤ 1.0",
  R2: "0.0 ≤ contract_score ≤ 1.0",
  R3: "0 ≤ truth_score ≤ 100",
  R4: "epistemic_score measures grounding quality only",
  R5: "contract_score measures schema / scope / constraint satisfaction only",
  R6: "(* truth_score formula — see licensed edition *)",
  R7: "result MUST be computed from rule evaluation — not from score averaging alone",
  R8: "truth_score output MUST be integer — LLM must not emit 0.75, must emit 75"
]

(* ═══ 5.4 Truth Field Hook — SAS / TPMN-checker Integration ═══ *)
(*                                                                              *)
(* The Truth field on a unit-contract is the formal integration point        *)
(* between PSL's three-phase protocol and the TPMN-checker tool (the SAS).   *)
(*                                                                              *)
TruthFieldHook ≜ [
  field_definition: "Truth: (optional external verification — score% | Alignment | SPT | EEF)",

  purpose: "Hook for L2 epistemic verification.
            When invoked, runs the three-phase protocol over the unit's
            CONTRACT and Result, returns truth_score with breakdown.",

  invocation: "Optional. Triggered by /verify-by-gem2 (TPMN-SKILL-STANDARD §11)
               or by direct SAS API call.",

  output_format: "score% | Alignment | SPT | EEF
                  Example: '75% | aligned | clean | ⊢ ⊨'
                  Empty when L2 was not invoked.",

  responsibility_boundary: "The Truth field provides external epistemic validation
                          beyond CONTRACT.B verification done by /verify-work.
                          /verify-work asks: did Result fulfill CONTRACT.B?
                          /verify-by-gem2 asks: was the reasoning epistemically sound?

                          These evaluations are orthogonal:
                          contract correctness ≠ epistemic validity.
                          Both can pass independently. Both can fail independently.
                          See §7 ResponsibilityBoundary."
]


(* ═══ §6. CONTRACT ARCHETYPE ═══ *)
(*                                                                              *)
(* CONTRACT formalizes F-as-face structurally.                                *)
(* §0.3 GeometricOntology states the same thing geometrically.                *)
(* They are the same artifact viewed from two angles.                         *)
(*                                                                              *)
(*
Each CONTRACT / MANDATE F defines its own independent bounded local complex space ℂ_F.
Multi-agent operation is possible because agents execute in separate ℂ_F spaces and compose only through explicit connectors G_ij.*)

Metric ≜ [
  name:       𝕊,
  expression: 𝕊,
  target:     𝕊,
  comparator: {"<", "≤", "=", ">", "≥"}
]

CONTRACT ≜ [
  archetype: "F: A → B | P  ≡  In → Out | Constraints",
  purpose:   "Formal specification of what a prompt demands.
              Geometrically: F is a face — a bounded admissible region.
The producer is sovereign within F, but does not own F.
              Every CONTRACT IS a SIMP-conformant unit (§0.2 SIMP_Principle).
              Every CONTRACT MUST declare its negative form (CTRST_Principle).",

  geometric_reading: [
    A: "Antecedent domain — type space of admissible input states",
    B: "Consequent domain — type space of admissible output states",
    F: "MANDATE face — independent bounded local complex space ℂ_F
    over A × B, defined as the set of all (a, b) satisfying P",
    P: "Boundary of F — constraint over A × B,
        including preconditions, invariants, and admissibility rules",
    not_B: "Negative contract — complement of F within A × B,
        i.e. (A × B) \\ F, states that violate P",
    Geom(F): "Geom(F) ⊆ ℂ_F and contains the points a + b𝓲
          corresponding to admissible pairs (a, b) ∈ F"
  ],

  sovereignty: "Inside F, the producer (human or AI) is sovereign.
                Free, maximally creative, blackbox.
                If you find yourself wanting to control what happens inside F,
                that means F is wrongly bounded — tighten P, don't reach inside.
                See §0.0 SovereigntyOfF.",

  structure: [
    contract_id:  𝕊,
    input:        Schema,                 (* A — input face *)
    output:       Schema,                 (* B — output face *)
    constraints:  {Constraint},           (* P — boundary of F *)
    negatives:    {ForbiddenCase},        (* ¬B — negative contract, CTRST satisfaction *)
    metrics:      [𝕊 ↦ Metric]
  ],

  rules: [
    "CONTRACT must be extractable from prompt during P-phase",
    "CONTRACT is immutable once P-phase completes",
    "O-phase verifies output against CONTRACT — not against intent",
    "CONTRACT.negatives MUST be non-empty for any non-trivial output —
     an empty negatives field with a non-trivial output is suspect (CTRST violation)",
    "CONTRACT format F: A → B | P is the canonical SIMP shape —
     a unit that does not decompose to this form fails SIMP",
    "CONTRACT defines a sovereign face — the producer is autonomous inside F"
  ],

  example: [
    contract_id:  "example_auth",
    input:        "[credentials: Credentials]",
    output:       "[token: JWT, expires: Timestamp]",
    constraints:  {"valid_credentials ⟹ token ≠ ⊥"},
    negatives:    {"no_plaintext_in_response", "no_token_on_invalid_credentials"},
    metrics:      ["latency" ↦ [name: "latency", expression: "response_time_ms",
                                 target: "200", comparator: "<"]]
  ]
]


(* ═══ §7. PHILOSOPHICAL FOUNDATION ═══ *)
(*                                                                              *)
(* Extended Kantian mapping — refined in v0.3.0 with noumenon/phenomenon     *)
(* distinction explicitly aligned to ontological/topological vocabularies.   *)
(*                                                                              *)

KantianMapping ≜ [

  status: "Heuristic philosophical framing, not a formal proof of TPMN correctness",

  Noumena ≜ [
    kant: "Thing-in-itself — beyond direct access",
    tpmn_ontological: "Ontological terms (point, line, face) are noumenal —
                       what beings ARE, accessed only through the topological layer",
    tpmn_intent:      "User's true intent — under-determined by the prompt alone",
    note: "The prompt is REPRESENTATION of intent, not intent itself.
           The point, line, face are REPRESENTATIONS of being, not being itself."
  ],

  Phenomena ≜ [
    kant: "What we experience through sensibility",
    tpmn_topological: "Topological terms (STATE, STATUS, SET) are phenomenal —
                       how beings APPEAR in relation, the layer TPMN operates on",
    tpmn_output:      "Raw AI token stream — observable output",
    note: "Without structure, output is noise, not knowledge.
           STATE/STATUS/SET are how the structure becomes computable."
  ],

  A_Priori ≜ [
    kant:      "Categories imposed BEFORE experience",
    tpmn:      "TPMN rules imposed BEFORE accepting output (P0–P7, O1–O9)",
    note:      "The grid that transforms noise into structured, auditable knowledge",
    mechanism: "Panini_Categories ⊂ A_Priori — SET structure defined in §1.2
                is the operative discretization mechanism before inference begins.
                Geometrically: faces tile the space before the producer enters."
  ],

  Transformation ≜ [
    before: "Prompt → AI → Hope",
    after:  "Prompt → TPMN_PRO.P → AI → TPMN_PRO.O → Trust",
    key:    "A_Priori_Grid is the missing compiler layer for AI interaction.
             Trust comes from edge-judgment (§0.0 ControlAtTheEdge),
             not from interior-control."
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
  boundary: "CONTRACT ≠ Reality. TPMN governs CONTRACT satisfaction, not truth-in-the-world.
             GEM² is Riemann approximation, not reality mirror —
             see §0.0 GEM²_RiemannFraming."
]


(* ═══ §8. FORMAT RULES ═══ *)

FormatRules ≜ [
  V1: "All definitions use TPMN notation — TLA+ first, math where needed, NL for strings",
  V2: "EEF_Record MUST accompany any TPMN-governed output",
  V3: "Timestamp MUST be executed — never guessed, copied, or hardcoded",
  V4: "Violations MUST name the SPT pattern and the specific claim",
  V5: "epistemic_score ∈ [0,1] — grounding quality only",
  V6: "contract_score ∈ [0,1] — contract conformance only",
  V7: "truth_score ∈ [0,100] — integer percent — LLM MUST output as integer, not Real",
  V8: "Every CONTRACT MUST have non-empty negatives — empty ¬B is a CTRST violation"
]

FormatProhibitions ≜ [
  N1: "Never omit EEF_Record from governed output",
  N2: "Never use ⊢ for claims that are inferred or extrapolated",
  N3: "Never suppress ⊬ or ⊥ tags to appear more confident",
  N4: "Never redefine or extend Tier1 glyphs — domain specifics belong in CONTRACT",
  N5: "Never run O-phase without a preceding P-phase — contract must precede verification",
  N6: "Never emit truth_score as Real (e.g. 0.75) — MUST be integer percent (e.g. 75)",
  N7: "Never hard-code domain-specific PayoffDim or NextStep into the principle —
       these are domain-parameterized via §9 Extension Protocol",
  N8: "Never conflate ontological and topological vocabularies —
       point/line/face are noumenal primitives;
       STATE/STATUS/SET are phenomenal relations.
       See §0.0 KantianAlignment and §0.3 GeometricOntology",
  N9: "Never reach inside F to control producer behavior —
       if F is wrongly bounded, tighten P; do not surveil interior.
       See §0.0 SovereigntyOfF"
]


(* ═══ §9. EXTENSION PROTOCOL ═══ *)

Extension_Protocol ≜ [
  purpose: "How platforms and domains extend TPMN-PSL without breaking the base",

  rules: [
    E1: "Declare EXTENDS TPMN-PSL explicitly in module header",
    E2: "Tier1 glyphs MUST NOT be redefined or extended —
         domain-specific distinctions belong in CONTRACT constraints (F: A → B | P)",
    E3: "P0–P7 and O1–O9 MUST be preserved · additional checks may be added",
    E4: "EEF_Record structure MUST be preserved · fields may be added, not removed",
    E5: "Extension version MUST reference base version explicitly",
    E6: "Extensions using Panini discretization MUST define P6 and populate
         A_Priori_Grid.categories",
    E7: "Extensions defining a domain MUST supply PayoffDim(domain) and NextStep(domain),
     which parameterize INCV (§0.2) and CONS (§0.2) respectively"",
    E8: "Extensions MUST preserve the ontological / topological vocabulary distinction
         (§0.0 KantianAlignment) — do not introduce primitives that conflate the layers"
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
    "EXTENDS TPMN_PSL  (* v0.3.0 *)",
    "(* Adds: domain P/O checks, domain SPT patterns, domain CONTRACT archetypes *)"
  ]
]

(* ═══ 9.2 Domain Extension Protocol ═══ *)
Domain_Extension_Protocol ≜ [

  required_definitions: [
    PayoffDim:  "PayoffDim(domain) ≜ {dimension₁, dimension₂, ...}
                  — finite set of payoff dimensions specific to the domain.
                  Used by INCV principle (§0.2).",

    NextStep:   "NextStep(domain) ≜ {action₁, action₂, ...}
                  — finite set of actionable next-step kinds specific to the domain.
                  Used by CONS principle (§0.2).",

    StateValue: "StateValue(domain) — extensions may add domain-specific verification
                  verdicts beyond the lifecycle base {SUCCESS, FAILURE, —}.
                  Routing function must remain total over the extended set.",

    StatusValue:"StatusValue(domain) — extensions may add domain-specific lifecycle
                  states beyond the base {PENDING, IN_PROGRESS, COMPLETED, ABORTED}.
                  Routing function must remain total over the extended set."
  ],

  optional_definitions: [
    DomainDiscipline: "DomainDiscipline(domain) — domain-specific compilation rules
                        that layer on top of the five universal principles.
                        Example: DELV (Maieutic Delivery) for marketing communication —
                        a marketing claim must trigger reflection in the audience.",

    SituationSchema:  "Schema for σ — defines what dimensions of situation matter
                        within the domain. INCV evaluates against (claim, domain, σ);
                        σ supplies the weighting context."
  ],

  examples: [
    marketing_communication: [
      PayoffDim:  "{clarity, permission, optionality, status, tool-utility}",
      NextStep:   "{decision, experiment, commitment, claim-extension}",
      Discipline: "DELV — claim must be delivered in question form, not assertion form",
      Situations: "{launch-week, sustain-phase, crisis-response, repositioning}"
    ],

    software_development: [
      PayoffDim:  "{correctness, latency, maintainability, deployability, observability}",
      NextStep:   "{commit, test, deploy, rollback, refactor, redesign}",
      Discipline: "(none beyond the universal five — code review IS CTRST)",
      Situations: "{feature-delivery, hotfix, refactor-sprint, security-audit}"
    ],

    trading_prediction: [
      PayoffDim:  "{expected-return, sharpe-ratio, max-drawdown, capital-efficiency, opportunity-cost}",
      NextStep:   "{place-order, modify-order, cancel-order, close-position, hedge}",
      Discipline: "(none beyond the universal five — stop-loss IS CTRST satisfaction)",
      Situations: "{high-conviction-bet, risk-managed-allocation, hedge-only, exit-only}"
    ]
  ],

  protocol: [
    Step_1: "Identify the domain explicitly. Name it. Bound it.",
    Step_2: "Define PayoffDim(domain) — the finite set of payoff dimensions.",
    Step_3: "Define NextStep(domain) — the finite set of actionable next-step kinds.",
    Step_4: "Define SituationSchema if INCV weighting varies within the domain.",
    Step_5: "Define DomainDiscipline if the domain has compilation rules beyond
              the universal five.",
    Step_6: "Verify: every domain-parameterized reference to INCV, CONS, and any
         DomainDiscipline is bound to the extension's definitions,
         not the base PSL or another domain's."
  ]
]


(* ═══ §10. COMPOSITE TEST — SOUND ═══ *)

SOUND_Composite ≜ [
  purpose: "Determine whether a unit of work u satisfies all five compilation
            principles in domain D and situation σ.
            Geometrically: SOUND audits the face's edge for completeness —
            boundary clarity (SIMP), edge-transition totality (CONS),
            boundary observability (FALS), payoff asymmetry (INCV),
            boundary completeness (CTRST).",

  formal_definition: "SOUND_universal(u, D, σ) ⟺
                        SIMP(u)
                      ∧ CONS(u)
                      ∧ FALS(u)
                      ∧ INCV(u, D, σ)
                      ∧ CTRST(u)

                    SOUND(u, D, σ) ⟺ SOUND_universal(u, D, σ)",

  per_principle_audit: "Test failure MUST name the failing principle(s).
                        Do not produce a single pass/fail summary;
                        produce a per-principle audit showing which principle(s)
                        failed and why.",

  domain_discipline_extension: "When the domain D defines a DomainDiscipline
                                 (per §9.2), the discipline MUST be conjuncted
                                 into SOUND. Example for marketing communication:

                                   SOUND(u, marketing, σ) ⟺
                                       SOUND_universal(u, marketing, σ)
                                     ∧ DELV(u, audience)",

  audit_record: "[principle: 𝕊, status: {PASS, FAIL}, reason: 𝕊 ∪ {⊥}]"
]

Audit_Record ≜ [
  principle: 𝕊,
  status:    {"PASS", "FAIL"},
  reason:    𝕊 ∪ {⊥}
]

SOUND_Output ≜ [
  composite: {"PASS", "FAIL"},
  composite_rule: "composite = PASS iff all Audit_Record.status = PASS;
                 otherwise FAIL",
  audits:    Seq(Audit_Record),
  domain:    𝕊,
  situation: 𝕊
]


(* ═══ §11. GLOSSARY ═══ *)

Glossary ≜ [
  "GEM²":                    "Grounded Existence Matrix for Global Entropy Minimum —
                               mathematical universe where AI operates with provable boundaries ·
                               Riemann approximation, not reality mirror · see §0.0, §0.1",
  "ΣΔ_Principle":            "TPMN-PSL is the world of finite Σ of Δ, not infinite ∫ of δ ·
                               see §0.1",

  (* — Vocabulary distinction (NEW in v0.3.0) — *)
  "Ontological_terms":       "Geometric primitives — point, line, face · noumenal · see §0.3",
  "Topological_terms":       "Relational structures — STATE, STATUS, SET · phenomenal · see §0.3",
  "Dynamic_operators":       "DATA, THRESHOLD — operators that move points across faces · see §0.3",

  point:                     "0D atomic element · noumenal · subject/object noun · see §0.3",
  line:                      "1D directional vector with weight · noumenal · verb/adjective · see §0.3",
  face:                      "2D bounded local complex space ℂ_F · noumenal · category/MANDATE · see §0.3",

  STATE:                     "(point ∈ face) · phenomenal · membership relation · see §0.3",
  STATUS: "local relational measurement at a point ·
         continuous, directional, weighted · see §0.3",
  SET: "subset within a face · phenomenal · bounded category region · see §0.3",

  DATA:                      "Discrete, computable, verifiable, falsifiable element · see §0.1",
  THRESHOLD:                 "Cut point on a face's boundary where STATE transitions occur · see §0.3",

  (* — Philosophical foundation (NEW in v0.3.0) — *)
  Kantian_Alignment:         "Ontological = noumenal; topological = phenomenal · see §0.0",
  GEM²_RiemannFraming:       "GEM² is approximated simulation, not reality mirror · see §0.0",
  ControlAtTheEdge:          "Human-at-the-edge architecture; sovereignty of producer · see §0.0",
  "SovereigntyOfF: Producer is sovereign within F;
                 F is bounded by P and not owned by the producer · see §0.0",
  DynamicAxiom:              "STATUS · point · THRESHOLD → STATE transition · see §0.3",
  PerMandatePanini:          "Each MANDATE has its own SET structure · see §0.3, §1.2",
  MandateAsFace:             "F is a face; A and B are faces; P bounds F · see §0.3, §6",

  (* — Existing terms — *)
  TPMN:                      "Truth-Provenance Markup Notation — the umbrella open spec
                               defining EEF, SPT, and the classification framework",
  PSL:                       "Prompt Specification Language — the language layer within TPMN
                               that compiles NL prompts into MANDATE",
  EEF:                       "Epistemic Evidence Framework — tagging and scoring system",
  SPT:                       "Structural Prohibition Taxonomy — forbidden inference patterns ·
                               operational catalogue of CTRST violations",
  A_Priori_Grid:             "IR extracted from prompt during P-phase · immutable within a run ·
                               optionally includes Panini_Categories and routing function",
  CONTRACT:                  "Formal specification of prompt intent · F-as-face structurally ·
                               every CONTRACT IS a SIMP-conformant unit · MUST declare ¬B (CTRST)",
  P_Phase:                   "Pre-flight prompt validation — boundary-drawing",
  P_Record:                  "Structured P-phase output: result + failed checks + repair hints",
  Inline_Phase:              "Claim-level epistemic tagging during generation · sovereign work inside F",
  O_Phase:                   "Post-flight output verification — edge-judgment",
  O_Record:                  "Structured O-phase output: result + scores + violations + eef_record",
  TruthFieldHook:            "Hook on unit-contracts for L2 SAS / TPMN-checker integration · see §5.4",

  epistemic_score:           "Score ∈ [0,1] estimating epistemic grounding quality only",
  contract_score:            "Score ∈ [0,1] estimating contract conformance only",
  truth_score:               "Composite heuristic % ∈ [0,100] · integer output ·
                               formula: see licensed edition",
  modification_factor:       "μ · calibration variable in truth_score formula · see licensed edition",
  NoViolations:              "<<>> — canonical empty spt_violations sequence",
  Metric:                    "Typed evaluation target: [name, expression, target, comparator]",
  Panini_Categories:         "Finite set of mutually exclusive, exhaustive, decidable categories
                               carved from domain D during P-phase · stored in A_Priori_Grid.categories",
  ontological_discretization:"Carving a continuous NL domain into finite computable categories ·
                               primary function of the Panini layer in TPMN · see §1.2",
  set_contract:              "Normative design contract for Panini categories:
                               (1) mutual_exclusion · (2) exhaustion · (3) decidability ·
                               applies WITHIN a single MANDATE, not across MANDATEs · see §0.3",
  MANDATE:                   "The computable, verifiable, traceable specification space established
                               by the P-phase · F-as-face · sovereign producer space",

  Compilation_Discipline:    "The five universal principles (§0.2) that govern any compilation
                               from prose to TPMN expression: SIMP, CONS, FALS, INCV, CTRST",
  Compilation_Process:       "The four-step cognitive operation (§1.5)",
  SIMP:                      "Sufficient Simplicity — boundary clarity test · see §0.2",
  CONS:                      "Predefined Consequence — edge-transition totality test · see §0.2",
  FALS:                      "Falsifiability — boundary observability test · see §0.2",
  INCV:                      "Selection Incentive — payoff-asymmetry test · see §0.2",
  CTRST:                     "Contrast / Negative Contract — boundary-completeness test · see §0.2",
  SOUND:                     "Composite test — SIMP ∧ CONS ∧ FALS ∧ INCV ∧ CTRST · see §10",
  PayoffDim:                 "Domain-parameterized set of payoff dimensions used by INCV · see §9.2",
  NextStep:                  "Domain-parameterized set of actionable next-step kinds used by CONS · see §9.2",
  Domain_Extension_Protocol: "Formal protocol for instantiating domain-parameterized definitions · see §9.2",

  "⊢":                       "Grounded claim",
  "⊨":                       "Inferred claim",
  "⊬":                       "Extrapolated claim — basis required",
  "⊥":                       "Unknown / undefined",
  "?":                       "Speculative claim",
  "S→T":                     "State-to-Trait SPT violation — CTRST failure",
  "L→G":                     "Local-to-Global SPT violation — CTRST failure",
  "Δe→∫de":                  "Incremental-to-Mass SPT violation — CTRST failure"
]


(* ═══ §12. SUMMARY ═══ *)

Summary ≜ [
  what:        "Platform-agnostic formal epistemic protocol for AI reasoning",
  philosophy:  "Kantian noumenon/phenomenon · GEM² as Riemann approximation ·
                control-at-the-edge · sovereignty of F",
  universe:    "GEM² — Riemann-discrete approximation of continuous reality",
  principle:   "ΣΔ — finite sums of discrete units, not continuous integration",
  ontology:    "point · line · face — geometric primitives, noumenal",
  topology:    "STATE · STATUS · SET — relational structures, phenomenal",
  dynamic:     "STATUS · point · THRESHOLD → STATE transition (§0.3 DynamicAxiom)",
  discipline:  "SIMP · CONS · FALS · INCV · CTRST — five universal compilation principles,
                edge-property tests on the MANDATE face",
  process:     "Step 1 (geometric decomposition) → Step 2 (ALG+SET) → Step 3 (coverage)
                → Step 4 (statement) — the four-step compilation cognitive operation",
  grammar:     "TLA+ + Panini + Math + NL — four-layer notation",
  symbols:     "Tier1 fixed (⊢⊨⊬⊥?) — domain semantics in CONTRACT, not new glyphs",
  protocol:    "P-phase (boundary-drawing) → Inline (sovereign execution) →
                O-phase (edge-judgment) — operational form of human-at-the-edge",
  ethics:      "SPT (forbidden patterns — CTRST violations) + EEF (epistemic tagging)",
  contract:    "F: A → B | P — sovereign face for producer, P bounds the face",
  scoring:     "epistemic_score [0,1] + contract_score [0,1] → truth_score % [0,100] · formula: see licensed edition",
  composite:   "SOUND(u, D, σ) — universal soundness test",
  mandate:     "NL prompt → MANDATE (face) — bounded sovereign producer space",
  extension:   "EXTENDS TPMN-PSL — domains supply PayoffDim, NextStep, optionally
                DomainDiscipline (§9.2)",
  version:     "v0.3.0 — adds philosophical foundation, geometric ontology,
                canonical example, threaded refinements"
]

===