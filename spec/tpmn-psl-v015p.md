--- MODULE TPMN_PSL_RefImpl ---

(* ════════════════════════════════════════════════════════════════════════════ *)
(* TPMN-PSL v0.1.5-p — Public Reference Implementation Specification          *)
(* EXTENDS TPMN_PSL v0.1.4                                                    *)
(* Suffix "-p" = public reference appendix                                     *)
(* ════════════════════════════════════════════════════════════════════════════ *)
(*                                                                              *)
(* Purpose: Define what a CONFORMANT public TPMN checker MUST implement.       *)
(* This spec enables third-party developers to build interoperable checkers    *)
(* that produce valid P_Record, O_Record, and TruthReport outputs.            *)
(*                                                                              *)
(* Changelog v0.1.5-p (2026-03-16):                                           *)
(*   REF-1:  Three-mode workflow formalized (strict / refine / interpolate)    *)
(*   REF-2:  Response contracts typed as JSON-serializable records             *)
(*   REF-3:  Consensus algorithm formalized for multi-provider mode            *)
(*   REF-4:  Calibration interface defined — μ=1 default, SAS hook declared   *)
(*   REF-5:  Three conformance levels (L1 minimal, L2 full, L3 calibrated)    *)
(*   REF-6:  Public/SAS boundary explicitly fenced                             *)
(*   REF-7:  Composer semantics formalized (strip overclaims, preserve ground) *)
(*                                                                              *)
(* Backward compatibility:                                                      *)
(*   · Fully compatible with v0.1.4 — no base definitions changed             *)
(*   · Implementations of v0.1.4 are valid L0 (spec-only, no checker)         *)
(*   · This appendix adds implementation requirements, not protocol changes    *)
(* ════════════════════════════════════════════════════════════════════════════ *)

EXTENDS TPMN_PSL  (* v0.1.4 *)


(* ═══ §R0. OVERVIEW ═══ *)

RefImpl_Overview ≜ [
  name:    "TPMN-PSL Reference Implementation Specification",
  version: "v0.1.5-p",
  status:  "Public · Reference Appendix",
  purpose: "Define conformance requirements for TPMN checker implementations",
  base:    "EXTENDS TPMN-PSL v0.1.4 — all base definitions inherited",
  suffix:  "-p denotes public reference appendix (not a protocol change)"
]

RefImpl_Scope ≜ [
  covers: {
    "Checker conformance levels and requirements",
    "Three-mode workflow semantics (strict / refine / interpolate)",
    "Response contract types (JSON-serializable)",
    "Multi-provider consensus algorithm",
    "Calibration interface (μ hook)",
    "Public / SAS boundary definition"
  },
  not_covers: {
    "SAS-specific calibration data or anchor sets",
    "Domain-specific weight matrices",
    "Multi-layer domain detection architecture",
    "Exact LLM prompt templates",
    "Authentication, authorization, or pricing",
    "Platform-specific deployment patterns"
  }
]


(* ═══ §R1. CONFORMANCE LEVELS ═══ *)

ConformanceLevel ≜ {"L1", "L2", "L3"}

L1_Minimal ≜ [
  name:        "Level 1 — Minimal Conformant Checker",
  description: "Single-provider truth filter with P-phase and O-phase checks",
  requirements: {
    MUST: {
      "Implement truth_filter endpoint accepting content + session_context",
      "Execute SPT_Check per §4 of base spec",
      "Produce EEF_Record per §3 of base spec",
      "Compute epistemic_score ∈ [0,1] and contract_score ∈ [0,1]",
      "Compute truth_score = round(min(100, epistemic_score · contract_score · 100))",
      "Return TruthReport conforming to §R3 response contract",
      "Support at least one LLM provider"
    },
    SHOULD: {
      "Implement P-phase checks P0-P5 per §5.1 of base spec",
      "Implement O-phase checks O1-O8 per §5.3 of base spec",
      "Return P_Record and O_Record conforming to §R3"
    },
    MAY: {
      "Support multiple LLM providers",
      "Implement mode parameter (strict/refine/interpolate)"
    }
  }
]

L2_Full ≜ [
  name:        "Level 2 — Full Conformant Checker",
  description: "Multi-mode checker with all three workflows and optional multi-provider",
  requirements: {
    MUST: {
      "Satisfy all L1 MUST requirements",
      "Implement all three modes: strict, refine, interpolate (§R2)",
      "Implement P-phase checks P0-P5",
      "Implement O-phase checks O1-O8",
      "Return P_Record, O_Record, and TruthReport per §R3",
      "Implement composer for refine mode (§R2.2)",
      "Implement search suggestion generation for interpolate mode (§R2.3)"
    },
    SHOULD: {
      "Support multiple LLM providers with consensus (§R4)",
      "Implement TPMN extraction pipeline (T-P-M-N) in reports",
      "Implement alignment checking when prompt is provided"
    },
    MAY: {
      "Implement calibration interface (§R5) with μ=1 default",
      "Implement domain detection for profile selection",
      "Implement cost tracking per response"
    }
  }
]

L3_Calibrated ≜ [
  name:        "Level 3 — Calibrated Checker (SAS-only)",
  description: "Full checker with runtime calibration via accumulated data",
  note:        "L3 is declared for completeness — it requires SAS-specific
                calibration data, anchor sets, and domain weight matrices
                that are NOT part of this public specification.
                L3 conformance is verified by the GEM2 SAS platform only.",
  requirements: {
    MUST: {
      "Satisfy all L2 MUST requirements",
      "Implement calibration interface (§R5) with μ ≠ 1",
      "Maintain anchor data set for calibration baseline",
      "Track provider drift via calibration history",
      "Apply domain-specific weight matrices for P/O scoring"
    }
  },
  boundary: "L3 details are intentionally omitted — see §R6"
]


(* ═══ §R2. THREE-MODE WORKFLOW ═══ *)

ModeSet ≜ {"strict", "refine", "interpolate"}

(* ─── R2.0 Common Input ─── *)
CheckerInput ≜ [
  content:         𝕊,                             (* REQUIRED — text to check *)
  session_context: 𝕊,                             (* REQUIRED — session state summary *)
  provider:        𝕊 ∪ {⊥},                      (* OPTIONAL — LLM provider name *)
  mode:            ModeSet ∪ {⊥},                 (* OPTIONAL — defaults to "strict" *)
  prompt:          𝕊 ∪ {⊥},                      (* OPTIONAL — for alignment checking *)
  domain_override: 𝕊 ∪ {⊥}                       (* OPTIONAL — skip auto-detection *)
]

DefaultMode ≜ "strict"

(* ─── R2.1 Strict Mode ─── *)
StrictMode ≜ [
  name:        "strict",
  description: "Diagnosis only — evaluate content, block on extrapolation",

  pipeline: <<
    "1. Run truth filter on content with session_context",
    "2. Produce TruthReport with epistemic_score, contract_score, truth_score",
    "3. Execute SPT_Check on each non-trivial claim",
    "4. Compute EEF_Record",
    "5. IF EEF.extrapolation = TRUE: report FLAGGED, do NOT compose",
    "6. Return TruthReport as diagnosis"
  >>,

  semantics: [
    halts_on_extrapolation: TRUE,
    produces_rewrite:       FALSE,
    returns:                "TruthReport"
  ]
]

(* ─── R2.2 Refine Mode ─── *)
RefineMode ≜ [
  name:        "refine",
  description: "Always compose — strip overclaims using ONLY provided input",

  pipeline: <<
    "1. Run truth filter on content (same as strict step 1-4)",
    "2. Run composer: rewrite content stripping SPT violations and ⊬ overclaims",
    "3. Composer MUST use ONLY information present in original content + session_context",
    "4. Composer MUST NOT introduce new claims, evidence, or external knowledge",
    "5. Run truth filter on composed output (re-verification)",
    "6. Return both original TruthReport and composed output with re-verified TruthReport"
  >>,

  composer_rules: [
    CR1: "Strip claims tagged ⊬ that lack explicit basis",
    CR2: "Downgrade universals ('always', 'never', 'all') to qualified scope",
    CR3: "Remove predictions without evidence (Δe→∫de)",
    CR4: "Preserve all ⊢ and ⊨ claims unchanged",
    CR5: "Preserve factual citations and sourced data",
    CR6: "NEVER add information not present in input — this is refinement, not augmentation"
  ],

  semantics: [
    halts_on_extrapolation: FALSE,
    produces_rewrite:       TRUE,
    returns:                "TruthReport + ComposedOutput + ReverifyTruthReport"
  ]
]

(* ─── R2.3 Interpolate Mode ─── *)
InterpolateMode ≜ [
  name:        "interpolate",
  description: "Diagnosis + search suggestions — meta-level, no rewrite",

  pipeline: <<
    "1. Run truth filter on content (same as strict step 1-4)",
    "2. For each ⊬ or ⊥ claim, generate search queries that could ground it",
    "3. Return TruthReport + search suggestions",
    "4. Caller is expected to fetch search results externally, then re-run with mode=refine"
  >>,

  search_suggestion_rules: [
    SS1: "One suggestion per ungrounded claim (⊬ or ⊥)",
    SS2: "Suggestion MUST be a concrete, searchable query string",
    SS3: "Suggestion MUST target the specific knowledge gap — not a generic topic search",
    SS4: "Suggestions are advisory — caller decides whether to use them"
  ],

  semantics: [
    halts_on_extrapolation: FALSE,
    produces_rewrite:       FALSE,
    produces_suggestions:   TRUE,
    returns:                "TruthReport + SearchSuggestions"
  ]
]


(* ═══ §R3. RESPONSE CONTRACTS ═══ *)
(* All responses MUST be JSON-serializable using these record types *)

(* ─── R3.1 CheckResult — per-check outcome ─── *)
CheckResult ≜ [
  status:    {"PASS", "WARN", "FAIL"},
  score:     {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0},
  reasoning: 𝕊
]

(* ─── R3.2 TPMNExtraction — T-P-M-N pipeline output ─── *)
TPMNExtraction ≜ [
  T: 𝕊,  (* TLA+ extraction *)
  P: 𝕊,  (* Panini term discretization *)
  M: 𝕊,  (* Math logic supplement *)
  N: 𝕊   (* Natural language check summary *)
]

(* ─── R3.3 EEFFlag — extrapolation detection ─── *)
EEFFlag ≜ [
  flagged:                   BOOLEAN,
  extrapolation_possibility: {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0},
  explanation:               𝕊
]

(* ─── R3.4 SPTIssue — individual SPT violation ─── *)
SPTIssue ≜ [
  type:        {"S→T", "L→G", "Δe→∫de"},
  claim:       𝕊,
  explanation: 𝕊
]

(* ─── R3.5 TruthReport — truth filter response ─── *)
TruthReport ≜ [
  provider:         𝕊,
  epistemic_score:  EpistemicScore,                   (* [0,1] — grounding quality *)
  contract_score:   ContractScore,                    (* [0,1] — contract conformance *)
  truth_score:      TruthScorePercent,                (* [0,100] — composite heuristic % *)
  eef:              EEFFlag,
  spt_issues:       Seq(SPTIssue),                    (* <<>> if none *)
  tpmn_extraction:  TPMNExtraction,
  explanation:      𝕊,                                (* plain English summary *)
  alignment_score:  {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0} ∪ {⊥},  (* ⊥ when no prompt *)
  alignment_issues: Seq(𝕊) ∪ {⊥}                     (* ⊥ when no prompt *)
]

TruthReport_Rules ≜ [
  TR1: "epistemic_score MUST measure grounding quality only",
  TR2: "contract_score MUST measure contract/schema/scope satisfaction only",
  TR3: "truth_score MUST be integer — use TruthScorePolicy.formula from v0.1.4 §3",
  TR4: "spt_issues MUST be <<>> (empty sequence) when no violations — never ⊥ or null",
  TR5: "alignment_score and alignment_issues MUST be ⊥ when no prompt provided",
  TR6: "explanation MUST be plain English — no TPMN notation in explanation field"
]

(* ─── R3.6 PReport — P-phase check report ─── *)
PReport ≜ [
  provider:        𝕊,
  context_frame:   [role: 𝕊, audience: 𝕊, domain: 𝕊, constraints: Seq(𝕊), gaps: Seq(𝕊)],
  tpmn_extraction: TPMNExtraction,
  checks:          [𝕊 ↦ CheckResult],                (* "P0"..."P5" → CheckResult *)
  eef_audit:       EEF_Record,
  spt_compliance:  [clean: BOOLEAN, issues: Seq(SPTIssue)],
  verdict:         {"PASS", "WARN", "FAIL"},
  score:           {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0},
  suggestions:     Seq(𝕊)
]

PReport_Rules ≜ [
  PR1: "checks MUST include P0 through P5 — all six checks required",
  PR2: "verdict MUST be derived from check evaluation — not from score alone",
  PR3: "score is weighted average of check scores — weight selection is implementation-defined",
  PR4: "suggestions SHOULD provide actionable repair hints for FAIL/WARN checks"
]

(* ─── R3.7 OReport — O-phase check report ─── *)
OReport ≜ [
  provider:        𝕊,
  context_frame:   [role: 𝕊, audience: 𝕊, domain: 𝕊, constraints: Seq(𝕊), gaps: Seq(𝕊)],
  tpmn_extraction: TPMNExtraction,
  checks:          [𝕊 ↦ CheckResult],                (* "O1"..."O8" → CheckResult *)
  eef_audit:       EEF_Record,
  spt_compliance:  [clean: BOOLEAN, issues: Seq(SPTIssue)],
  verdict:         {"PASS", "WARN", "FAIL"},
  score:           {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0},
  suggestions:     Seq(𝕊)
]

OReport_Rules ≜ [
  OR1: "checks MUST include O1 through O8 — all eight checks required",
  OR2: "O8 (category integrity) is CONDITIONAL — required only when
        A_Priori_Grid.categories is populated from P-phase",
  OR3: "verdict MUST be derived from check evaluation — not from score alone",
  OR4: "score is weighted average of check scores — weight selection is implementation-defined"
]

(* ─── R3.8 Consensus — multi-provider agreement ─── *)
Consensus ≜ [
  verdict:     {"PASS", "WARN", "FAIL", "N/A"},
  agreement:   {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0},   (* fraction of checks with unanimous agreement *)
  avg_score:   {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0},
  divergences: Seq(𝕊),                              (* "P1: claude=PASS, openai=WARN" *)
  per_check:   [𝕊 ↦ 𝕊] ∪ {⊥}                     (* check → consensus status *)
]

(* ─── R3.9 SearchSuggestion — for interpolate mode ─── *)
SearchSuggestion ≜ [
  claim:  𝕊,       (* the ungrounded claim *)
  query:  𝕊,       (* suggested search query *)
  reason: 𝕊        (* why this search would help *)
]

(* ─── R3.10 ComposedOutput — for refine mode ─── *)
ComposedOutput ≜ [
  original_truth:   TruthReport,
  composed_text:    𝕊,
  changes:          Seq(𝕊),                          (* list of changes made *)
  refined_truth:    TruthReport,                     (* re-verification of composed text *)
  combined_score:   {r ∈ Real : 0.0 ≤ r ∧ r ≤ 1.0} (* implementation-defined combination *)
]


(* ═══ §R4. CONSENSUS ALGORITHM ═══ *)
(* Formal specification of the majority-vote multi-provider consensus *)

Consensus_Algorithm ≜ [
  name:     "Majority-Vote Provider Consensus",
  purpose:  "Aggregate P/O check results from multiple LLM providers into a single verdict",
  requires: "|providers| ≥ 2 — single provider returns trivial consensus (agreement=1.0)"
]

(* ─── R4.1 Algorithm Steps ─── *)
ConsensusSteps ≜ <<

  "Step 1: Collect check keys",
  (* Given: reports = Seq(CheckReport) where CheckReport = [provider, checks, verdict, score] *)
  (* Let checkKeys = ∪{keys(r.checks) : r ∈ reports} — union of all check keys across providers *)

  "Step 2: Per-check majority vote",
  (* ∀ key ∈ checkKeys:
       statuses ≜ {r.checks[key].status : r ∈ reports ∧ key ∈ dom(r.checks)}
       IF |statuses| = 1:
         perCheck[key] ≜ the single status  (* unanimous *)
       ELSE:
         perCheck[key] ≜ argmax_s(|{r : r.checks[key].status = s}|)  (* majority *)
         Record divergence: "key: provider1=status1, provider2=status2, ..." *)

  "Step 3: Verdict consensus",
  (* verdictCounts ≜ [v ↦ |{r : r.verdict = v}| : v ∈ {"PASS","WARN","FAIL"}]
     consensusVerdict ≜ argmax_v(verdictCounts[v]) *)

  "Step 4: Agreement metric",
  (* agreeCount ≜ |{key ∈ checkKeys : all providers report same status}|
     agreement ≜ agreeCount / |checkKeys|
     agreement ∈ [0.0, 1.0] *)

  "Step 5: Average score",
  (* avgScore ≜ sum(r.score : r ∈ reports) / |reports| *)

  "Step 6: Assemble Consensus record",
  (* Return Consensus {verdict, agreement, avgScore, divergences, perCheck} *)

>>

ConsensusRules ≜ [
  C1: "Majority is simple count — no weighting by provider reputation",
  C2: "Ties broken by implementation-defined strategy (first-seen, alphabetical, etc.)",
  C3: "Single-provider returns agreement=1.0, no divergences",
  C4: "Zero-provider returns verdict='N/A', agreement=0.0"
]


(* ═══ §R5. CALIBRATION INTERFACE ═══ *)

CalibrationInterface ≜ [
  purpose: "Define the hook point where SAS calibration modifies truth_score via μ",

  (* ─── μ in public implementations ─── *)
  public_default: [
    mu:      1,
    formula: "truth_score = round(min(100, epistemic_score · contract_score · 1 · 100))",
    note:    "Public implementations use identity μ — no calibration effect.
              truth_score reduces to round(min(100, e · c · 100))"
  ],

  (* ─── μ in SAS implementations ─── *)
  sas_hook: [
    mu:      "f(sim) — derived from similarity query over accumulated O_Records",
    formula: "truth_score = round(min(100, epistemic_score · contract_score · μ · 100))",
    note:    "⊨ SAS-specific calibration mechanism — design hypothesis, not yet
              empirically validated. Details intentionally omitted from public spec."
  ],

  (* ─── CalibrateScore function signature ─── *)
  calibrate_score: [
    input:  "[raw_score: Real, provider: 𝕊, model: 𝕊]",
    output: "Real ∈ [0.0, 1.0]",
    logic:  "raw_score + offset(provider, model) — clamped to [0.0, 1.0]",
    note:   "Public implementations MAY set offset = 0.0 for all providers.
             SAS implementations compute offsets from anchor data."
  ],

  (* ─── Anchor concept (declared, not detailed) ─── *)
  anchors: [
    definition: "Human-validated reference scores for known content categories",
    purpose:    "Calibration baseline — compare LLM raw scores against known-good scores",
    public:     "Public implementations MAY maintain their own anchor sets",
    sas:        "SAS anchor data is NOT part of this specification"
  ]
]

(* ─── Weight Interface ─── *)
WeightInterface ≜ [
  purpose: "P/O check scores are combined via weighted average — weights are implementation-defined",

  contract: [
    W1: "∀ weight set W: sum(W) = 1.0",
    W2: "∀ w ∈ W: w > 0.0",
    W3: "P-check weights cover P0 through P5 (6 weights)",
    W4: "O-check weights cover O1 through O8 (up to 8 weights — O8 conditional)"
  ],

  public_guidance: [
    "Equal weights (1/6 for P-checks, 1/8 for O-checks) are a valid starting point",
    "Implementations SHOULD document their weight selection rationale",
    "Implementations MAY vary weights by domain if domain detection is implemented"
  ],

  sas_note: "SAS-specific weight matrices are NOT part of this specification"
]

(* ─── Verdict Derivation ─── *)
VerdictDerivation ≜ [
  purpose: "Map weighted score to verdict",
  note:    "Thresholds are implementation-defined. Reference thresholds provided as guidance.",

  reference_thresholds: [
    PASS: "weighted_score ≥ 0.8",
    WARN: "0.5 ≤ weighted_score < 0.8",
    FAIL: "weighted_score < 0.5"
  ],

  rules: [
    V1: "Verdict MUST be derived from rule evaluation — not from score averaging alone",
    V2: "A single FAIL check MAY override an otherwise passing score (implementation-defined)",
    V3: "Implementations MUST document their verdict derivation strategy"
  ]
]


(* ═══ §R6. PUBLIC / SAS BOUNDARY ═══ *)

Boundary ≜ [
  purpose: "Explicitly define what is public vs SAS-proprietary",

  public_domain: {
    "TPMN-PSL base spec (v0.1.4 and all prior versions)",
    "This reference implementation spec (v0.1.5-p)",
    "P-phase checks P0-P5 definitions",
    "O-phase checks O1-O8 definitions",
    "SPT_Check algorithm and violation taxonomy",
    "EEF tagging rules and EEF_Record structure",
    "TruthScorePolicy formula with μ=1",
    "Three-mode workflow semantics (strict/refine/interpolate)",
    "Consensus algorithm (majority-vote)",
    "Response contract types (TruthReport, PReport, OReport, Consensus)",
    "Calibration interface signature (CalibrateScore)",
    "Weight interface contract (sum=1, positive, documented)",
    "Composer rules CR1-CR6"
  },

  sas_domain: {
    "μ calibration function f(sim) implementation",
    "Anchor data sets (human-validated reference scores)",
    "Calibration history and drift tracking internals",
    "Domain-specific weight matrices (SDLC, research, medical, legal, etc.)",
    "Domain detection and multi-layer check architecture",
    "Exact LLM system prompt templates",
    "Composer prompt wording and examples",
    "Profile-specific context frame rules",
    "Score derivation heuristics for backward compatibility",
    "User authentication, tier policy, and pricing"
  },

  boundary_rule: "Implementations MUST NOT claim L3 conformance without
                   SAS-provided calibration data. L3 is verified by the
                   GEM2 SAS platform — self-certification is not valid."
]


(* ═══ §R7. COMPOSER SPECIFICATION ═══ *)
(* Formalized from refine mode — the overclaim stripping algorithm *)

Composer ≜ [
  purpose: "Rewrite content to remove epistemic overclaims while preserving grounded information",

  input:  "[content: 𝕊, session_context: 𝕊, truth_report: TruthReport]",
  output: "[composed_text: 𝕊, changes: Seq(𝕊)]",

  algorithm: <<
    "1. Parse truth_report.spt_issues — identify all SPT-violating claims",
    "2. Parse truth_report.eef — identify all ⊬ claims without explicit basis",
    "3. For each violating claim:",
    "   a. IF S→T: Replace absolute language with qualified temporal language",
    "   b. IF L→G: Scope the claim to the observed population/context",
    "   c. IF Δe→∫de: State evidence count explicitly, downgrade conclusion strength",
    "   d. IF ⊬ without basis: Remove claim OR add explicit uncertainty marker",
    "4. Preserve all ⊢ and ⊨ claims verbatim",
    "5. Preserve all citations, sourced data, and factual references",
    "6. Produce changes list documenting each modification"
  >>,

  invariants: [
    CI1: "composed_text contains NO new information not in original content",
    CI2: "|composed_text.claims_tagged_⊢| ≥ |content.claims_tagged_⊢|",
    CI3: "|composed_text.claims_tagged_⊬| ≤ |content.claims_tagged_⊬|",
    CI4: "composed_text preserves the author's core argument structure",
    CI5: "changes list is non-empty IF any modifications were made"
  ]
]


(* ═══ §R8. IMPLEMENTATION GUIDANCE ═══ *)
(* Non-normative — advisory for implementors *)

ImplementationGuidance ≜ [

  (* ─── LLM Integration ─── *)
  llm_integration: [
    note:     "TPMN checking is LLM-evaluated — the checker sends structured system prompts
               to an LLM and parses the structured JSON response",
    pattern:  "system_prompt(TPMN_grammar + check_definitions + content) → LLM → JSON → parse → report",
    guidance: {
      "System prompt SHOULD include TPMN grammar (§1 of base spec) for context",
      "System prompt SHOULD include check definitions (P0-P5 or O1-O8) as evaluation criteria",
      "System prompt SHOULD instruct LLM to return JSON conforming to response contracts (§R3)",
      "Response parsing SHOULD handle markdown-fenced JSON (```json ... ```)",
      "Response parsing SHOULD handle leading/trailing prose around JSON",
      "Response parsing SHOULD validate score ranges and clamp out-of-bounds values"
    }
  ],

  (* ─── Multi-Provider ─── *)
  multi_provider: [
    guidance: {
      "Providers SHOULD be called in parallel for latency optimization",
      "If a provider fails, other providers SHOULD still produce results",
      "Provider errors SHOULD be surfaced in the response, not silently dropped",
      "Consensus (§R4) requires ≥ 2 successful provider responses"
    }
  ],

  (* ─── Defensive Parsing ─── *)
  defensive_parsing: [
    guidance: {
      "LLMs may wrap JSON in markdown code fences — strip them before parsing",
      "LLMs may prepend explanatory prose — find first '{' as JSON start",
      "LLMs may append commentary after JSON — find matching '}' as JSON end",
      "Null/missing arrays SHOULD be normalized to empty sequences (<<>>)",
      "Score values outside [0,1] SHOULD be clamped, not rejected",
      "truth_score values < 2.0 MAY indicate legacy float format — multiply by 100 and round"
    }
  ],

  (* ─── Error Handling ─── *)
  error_handling: [
    guidance: {
      "LLM timeout SHOULD be configurable — recommended 120s per call",
      "Pipeline timeout (multi-step modes) SHOULD be configurable — recommended 5m",
      "Content length SHOULD be bounded — reject inputs exceeding implementation limit",
      "Empty content or session_context SHOULD return 400, not invoke LLM"
    }
  ]
]


(* ═══ §R9. CONFORMANCE VERIFICATION ═══ *)

ConformanceVerification ≜ [
  purpose: "How implementations demonstrate conformance",

  L1_verification: [
    "Submit TruthReport for 5 canonical test inputs (published separately)",
    "Verify truth_score is integer ∈ [0,100]",
    "Verify epistemic_score and contract_score are Real ∈ [0,1]",
    "Verify spt_issues is Seq (never null)",
    "Verify EEF flag is present and BOOLEAN"
  ],

  L2_verification: [
    "Pass all L1 verification",
    "Submit strict mode response — verify no composed output",
    "Submit refine mode response — verify composed output + re-verification",
    "Submit interpolate mode response — verify search suggestions present",
    "Submit P-check response — verify P0-P5 all present",
    "Submit O-check response — verify O1-O8 all present (O8 conditional)"
  ],

  L3_verification: [
    "L3 is verified by GEM2 SAS platform only",
    "Self-certification of L3 is not valid"
  ],

  test_inputs: "⊨ Canonical test input set will be published as a separate artifact.
                This is a forward reference — not yet available at v0.1.5-p publication."
]


(* ═══ §R10. GLOSSARY ADDITIONS ═══ *)

RefImpl_Glossary ≜ [
  L1:                  "Level 1 Conformance — minimal truth filter checker",
  L2:                  "Level 2 Conformance — full three-mode checker with P/O phases",
  L3:                  "Level 3 Conformance — calibrated SAS checker (proprietary)",
  strict_mode:         "Diagnosis only — halts on extrapolation, no rewrite",
  refine_mode:         "Always compose — strip overclaims using only input information",
  interpolate_mode:    "Diagnosis + search suggestions — meta-level, no rewrite",
  composer:            "Component that rewrites content to remove overclaims (refine mode)",
  consensus:           "Multi-provider agreement metric via majority-vote algorithm",
  CheckerInput:        "Standard input record for all checker endpoints",
  TruthReport:         "Response contract for truth filter evaluation",
  PReport:             "Response contract for P-phase (pre-flight) evaluation",
  OReport:             "Response contract for O-phase (post-flight) evaluation",
  ComposedOutput:      "Response contract for refine mode including rewrite + re-verification",
  SearchSuggestion:    "Advisory search query for interpolate mode ungrounded claims",
  public_domain:       "Spec content available to all implementors",
  sas_domain:          "Spec content restricted to GEM2 SAS platform",
  anchor:              "Human-validated reference score for calibration baseline",
  weight_interface:    "Contract for P/O check scoring weights (sum=1, positive, documented)"
]


(* ═══ §R11. SUMMARY ═══ *)

RefImpl_Summary ≜ [
  what:           "Public reference implementation specification for TPMN checkers",
  extends:        "TPMN-PSL v0.1.4 — no base protocol changes",
  levels:         "L1 (minimal) → L2 (full) → L3 (calibrated, SAS-only)",
  modes:          "strict (diagnose) · refine (compose) · interpolate (suggest)",
  contracts:      "TruthReport · PReport · OReport · Consensus · ComposedOutput · SearchSuggestion",
  consensus:      "Majority-vote over ≥2 providers — simple count, no weighting",
  calibration:    "μ=1 (public default) · μ=f(sim) (SAS hook, details omitted)",
  weights:        "Implementation-defined · sum=1 · positive · documented",
  boundary:       "Public domain = protocol + contracts + algorithms.
                    SAS domain = calibration data + weight matrices + prompt templates.",
  version:        "v0.1.5-p — public reference appendix"
]

===
