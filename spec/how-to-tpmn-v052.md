# How to TPMN — Field Manual

**A practitioner's guide for applying TPMN to real work**

**Version:** 0.5.2 | **Companion to:** TPMN-PSL v0.5.2
**Family:** TPMN-PSL · TPMN-SKILL-STANDARD · TPMN-LIFECYCLE-GUIDE · TPMN-Checker

---

## What this manual is

This is a field manual, not a specification. It tells practitioners how to use TPMN in real work. For normative definitions — the formal grammar, the five compilation principles, the three-phase protocol, the geometric ontology — see TPMN-PSL v0.5.2.

This manual is written for readers who:

- Work with AI agents (Claude Code, Codex, Gemini CLI, Cursor) or build AI-driven systems
- Have read at least the PSL v0.5.2 §12 Summary
- Want concrete recipes alongside the formal spec
- Are willing to learn one new mental model

If those don't describe you, this manual is not your starting point. The TPMN family includes other entry points — see Reader paths at the end.

---

## What TPMN gives you

Three properties that prose-based work does not enforce:

**1. Boundary clarity.** Every unit of work is expressed as `F: A → B | P` — input state A, expected output state B, preconditions P. Per PSL v0.5.2 §6:

> "F is the producer's sovereign space. Every CONTRACT IS a SIMP-conformant unit. Every CONTRACT MUST declare its negative form (CTRST_Principle)."

Operationally, when a unit fails verification, the comparison is structural: which field of B is missing, which constraint in P does the Result violate. Compare prose: "the function should handle errors gracefully" leaves the success/failure boundary undefined; `F: input → output | ∀ err ∈ ErrorSet: handled(err)` does not.

**2. Compaction safety against context drift.** Formal notation has fewer paraphrase variants than prose. Per PSL §1.2 Panini drift_model:

> "LLM reasoning may degrade across long, high-density content — category boundaries can blur and inference may drift. Inline set-membership declaration is intended to re-anchor reasoning to the P-phase category structure by repeatedly exposing category boundaries during generation."

Example: a prose instruction "use only validated user data" admits multiple interpretations across a long conversation (validated by what? when?). The formal form `validated: User → Bool` with `Bool` defined in P-phase admits one interpretation, repeatable across turns. (⊨ inferred from PSL §1.2 drift_model — the PSL notes this is "a design hypothesis of TPMN, not yet a universally established empirical law".)

**3. Sovereign execution within the contract.** Inside F, the producer is autonomous. Per PSL §0.0 SovereigntyOfF:

> "F is the producer's sovereign operational space, whether human or AI. The contract (P) defines its boundary. Within this boundary, execution is not externally controllable — the producer operates autonomously. Sovereignty does not imply ownership of F."

Operationally: the proceed-work skill (TPMN-SKILL-STANDARD §11) enforces this — "Execution strategy is executor's blackbox — skill does not dictate how." The producer's freedom is bounded by the contract, not by the orchestrator's intervention.

**Honest cost note.** TPMN imposes overhead. For one-shot prompts ("explain this code", "summarize this article"), the overhead is unjustified. The framework targets autonomous pipelines, multi-step workflows, long-running agentic systems, high-stakes work — situations where silent failure is expensive. The judgment of whether your situation justifies the overhead is yours.

---

## The mental model in one minute

In the domains TPMN governs — software development, prediction, communication, decision pipelines — work proceeds against situations that resist clean discrete categorization. TPMN imposes a discrete bounded structure on top so the work becomes auditable as one mental model. (As one mental model — see PSL §0.0 GEM²_RiemannFraming for the design framing of this approximation: "GEM² is the rectangle approximation. Reality is the curve.")

Three primitives describe what work is *about* (ontological — what beings ARE in PSL §0.3 terms):

- **point** — a 0D atomic element; an entity. *Examples: David, gem2-lfs, the Q3 report.*
- **line** — a 1D directional vector with weight; a verb, adjective, or adverb. *Examples: failing, decomposing, becoming-stable.*
- **face** — a 2D bounded local complex space ℂ_F; an independent local space defined by a CONTRACT/MANDATE F. Not a sub-region of a global plane. *Examples: humans, valid functions, completed work-plans — each its own ℂ_F.*

Per PSL §0.0 SovereigntyOfF.flexibility:

> "The size of F is flexible and abstractive. A banking system can be F. A game can be F. A report can be F. A single inference can be F. A parent MANDATE relates to child MANDATEs through compositional structure, not through shared geometry — each child F_j has its own ℂ_Fj, linked to the parent via explicit G_ij transformations (§Lemma 5)."

Three relations describe how work *appears* (topological — how beings APPEAR in relation):

- **STATE** — `point ∈ face`. *David is human. The WP is COMPLETED.*
- **STATUS** — vector at point. *The WP is becoming complete. The build is running.*
- **SET** — a recognized category within a face's local space. *The set of completed WPs.*

One dynamic governs change. Per PSL §0.3 DynamicAxiom:

> "ALL BEING is discrete. Being exists in a STATE. When its STATUS passes a POINT THRESHOLD, the STATE has changed."

A MANDATE is a face — the producer's sovereign space. F: A → B | P. A and B are typed faces (input and output sets). F is itself a bounded local complex space ℂ_F, defined as the set of all (a, b) admissible under P. P is the constraint that bounds ℂ_F. There is no shared global complex plane — each F has its own ℂ_F. MANDATEs relate to each other compositionally through G_ij transformations, not by sharing geometry (PSL §0.4 CompositionBridge).

That is the geometric vocabulary; subsequent sections show its application.

---

## The four-step compilation process

Converting prose into a TPMN expression takes four steps. Each one answers a different question. Per PSL §1.5 Compilation_Process.

### Step 1 — What does the prose mean?

Pin the interpretation. Then classify every meaning-bearing word geometrically, per PSL §1.5 Step_1:

- Subject and object nouns → **points**
- Verbs, adjectives, adverbs → **lines**
- Category nouns (humans, functions, packages) → **faces**

Then extract the topological assertions:

- "X is a Y" where Y is a category → STATE assertion `(X ∈ Y)`
- "X is/becomes Z" where Z is an adjective → STATUS vector at X
- Named bounded regions → SET definitions

Output of Step 1 is a geometric decomposition plus a pinned interpretation in plain language.

### Step 2 — What's the subject/verb/object?

Encode the geometric decomposition algebraically:

- Points become set elements
- Lines become relations between elements
- Faces become bounded local complex spaces ℂ_F; SETs become named bounded categories within those spaces

For prose with at least one extractable noun-verb structure, Step 2 produces output. The TPMN expressions throughout this manual rest on ALG+SET as their substrate.

### Step 3 — Which formal layers does this require?

Ask four questions, per PSL §1.5 Step_3.layer_questions:

- **TLA+ needed?** Is there flow, condition, or temporal structure? *(First X then Y? If A then B? Always/eventually?)*
- **Panini needed?** Are there dense or repetitive nouns to disambiguate? *(Multiple kinds of "claim"? Several types of "evidence"?)*
- **Math needed?** Is there a decision producing STATE or STATUS? *(Threshold check? Predicate evaluation?)*
- **NL needed?** Is there irreducibly intentional content that no formal notation can express? *(e.g., "reflection", "trust", "care" — but see Pattern 2 in §Patterns to watch for: NL must be confined to a single named predicate or comment, never used to glue operators together. Listing example NL words here does not authorize widespread NL use.)*

Check only what the prose actually requires. Output is a layer manifest — auditable.

### Step 4 — Assemble the spec

Write the formal expression using only the layers Step 3 identified. ALG+SET is the substrate; other layers appear when the manifest calls for them.

**Audit prompt** (per PSL §1.5 Step_4.audit):

> "Read the result aloud. If it sounds like a sentence rather than a formal expression, return to Step 3 and find the layer being misused or missing."

---

## A worked example, line by line

Here is the four-step process applied to one prose sentence.

**Prose:** *"This refactor is safe to merge."*

### Step 1 — Geometric decomposition

| Word | Geometric primitive | Topological role |
|---|---|---|
| this refactor | point | the entity under evaluation |
| is | line (linking) | STATE-assertion verb |
| safe | line (adjective) | STATUS vector — "safe-to-merge" direction |
| to merge | line (purposive) | implied future action |

**Pinned interpretation:** *"The refactor occupies the STATE 'safe-to-merge' — meaning, when the merge action is taken, the post-merge STATE will be SUCCESS rather than FAILURE."*

**Topological assertions extracted:**

- STATE: `refactor ∈ safe-to-merge-set`
- STATUS: vector "safe-to-merge" at the refactor point
- Implied SET: `safe-to-merge-set` — a bounded category within the local contract space F_refactor, needs explicit membership rule

### Step 2 — ALG+SET encoding

```
refactor: Point
SafeToMerge: Set
STATE: refactor ∈ SafeToMerge
```

### Step 3 — Coverage manifest

| Layer | Required? | Why |
|---|---|---|
| TLA+ | ✗ | The prose is a static predicate ("is safe"), not a flow ("first X then Y"). Conditional structure is absent unless the spec extends to merge sequencing. |
| Panini | ✓ | `SafeToMerge` needs explicit membership rule |
| Math | ✓ | `safe(refactor) ⟺ ∀ tests : pass(tests)` is a decision |
| NL | ✗ | "safe" reduces to "tests pass + no contract break"; no irreducible intentionality |

### Step 4 — Optimized statement

```
(* Sets defined for this example *)
Refactor       ⊆ CodeChange                         (* the universe of refactors under review *)
TestSuite      = the test suite for this refactor    (* scoped: this refactor's tests *)
ContractTests  ⊆ TestSuite                          (* tests that check spec-level invariants *)
acceptable_threshold : Real                          (* per-project benchmark tolerance *)

SafeToMerge ≜ { r ∈ Refactor :
                  ∀ t ∈ TestSuite      : pass(t, r)
                ∧ ∀ c ∈ ContractTests  : pass(c, r)
                ∧ benchmark_regression(r) ≤ acceptable_threshold }

safe(refactor) ≜ refactor ∈ SafeToMerge
```

**Commentary.** This sentence compiled to a Panini set definition (`SafeToMerge`) plus a Math+ALG membership predicate (`safe`). TLA+ stayed out (Step 3 ✗) because the prose contained no flow or conditional structure — if the spec extended to "merge then deploy", TLA+ would enter. NL stayed out because "safe" reduced to a finite testable conjunction.

Patterns recur — Section *Three case studies* shows this compilation process applied to three additional domains (SDLC, marketing, trading).

---

## Three case studies

The principles below applied identically to all three cases (SDLC, marketing, trading) shown in this section. Whether they apply universally beyond these cases is an open question; PSL §0.2 frames them as universal but each domain extension supplies its own parameters (see PSL §9.2 Domain_Extension_Protocol).

### Case Study 1 — SDLC (the canonical example)

**Prose request:** *"Create npm binary distribution package for gem2-lfs using esbuild-style platform-specific optionalDependencies. 5 npm packages: 1 main wrapper + 4 platform-specific binary carriers. No Go source code exposed."*

This is real (verifiable: see WP-ST-112 in the gem2-lfs repository, all 4 units COMPLETED with State: SUCCESS).

**Domain instantiation:**

```
PayoffDim(SDLC) = {correctness, latency, maintainability, deployability, observability}
NextStep(SDLC)  = {commit, test, deploy, rollback, refactor, redesign}
```

**Compilation output (parent MANDATE + 4 child MANDATEs, compositionally linked):**

```
Parent MANDATE F_WP:  "Create npm binary distribution package"   (own ℂ_F_WP)
                            │
              ─── G_ij compositional handoff ───
                            │
  Child MANDATE F_1:  Create npm directory structure and 5 package.json files
                            ↓ G_12 : B_1 → A_2
  Child MANDATE F_2:  Create Node.js wrapper and platform detection module
                            ↓ G_23 : B_2 → A_3
  Child MANDATE F_3:  Create build.sh for cross-compilation and staging
                            ↓ G_34 : B_3 → A_4
  Child MANDATE F_4:  Build, verify no source leaks, and test locally
```

Each child has its own bounded local complex space ℂ_F_i and its own A → B | P contract. Parent and children are linked through G_ij transformations (PSL §0.4 CompositionBridge), not by children tiling the parent's ℂ_F. The handoff between consecutive units is a typed transfer: the output type B_i of one unit becomes the input type A_j of the next, validated by the bridge constraint P_ij.

**Principles audit (each verdict names the test a reader can perform):**

| Principle | Verdict | Test |
|---|---|---|
| **SIMP** | ✓ | Try to decompose any unit into ≥2 sub-units that aren't trivial restatements; if the sub-WP would have all sub-units sharing the same A or producing the same B, parent SIMP holds |
| **CONS** | ✓ | Enumerate `(StateValue × StatusValue)` for the unit; check each pair has a defined next-action via /proceed-work or /verify-work routing — total iff every pair is mapped |
| **FALS** | ✓ | Run `npm pack --dry-run` on each platform package; SIMP→FALS verdict holds iff zero `.go`, `.mod`, `.sum` files appear |
| **INCV** | ✓ | Compare `install_steps_pre_WP` (manual binary download + chmod + path setup) vs `install_steps_post_WP` (`npm install -g @gem_squared/gem2-lfs`); INCV holds iff strict decrease on `deployability` dimension |
| **CTRST** | ✓ | For each unit, check `¬B` field is non-empty; e.g., Unit 4 declares `¬B`: "any `.go`/`.mod`/`.sum` file in package tarballs"; CTRST holds iff every unit's `¬B` is testable |

### Case Study 2 — Marketing Communication

**Prose request:** *"Write a dev.to article explaining why prose-based Claude Skills fail silently."*

**Domain instantiation:**

```
PayoffDim(marketing)  = {clarity, permission, optionality, status, tool-utility}
NextStep(marketing)   = {decision, experiment, commitment, claim-extension}
DomainDiscipline      = DELV (Maieutic Delivery)
```

Marketing has a DomainDiscipline that SDLC does not.

**Article CONTRACT:**

```
A: claim that prose Claude Skills fail silently + supporting examples
B: published dev.to article (1500-2500 words, headline + sub-sections, code samples)
P: target = Claude Code users; tone = candid; ≥ 3 concrete failure modes named
¬B: hype piece without examples; assertion-only delivery (DELV violation)
```

**Principles audit:**

| Principle | Verdict | Test |
|---|---|---|
| **SIMP** | ✓ | The article decomposes to one thesis (silent failure) + three named failure modes; check whether further sub-articles would have substantively different B — if not, SIMP holds |
| **CONS** | ✓ | Publication produces (STATE: published, STATUS: live); next-actions defined: engagement_signal → reply or follow-up post; rejection → revise; total over the StateValue × StatusValue grid |
| **FALS** | ✓ | The thesis "prose skills fail silently" is testable: examine N real Claude Skills repos, count instances of the three named failure modes; thesis falsified iff zero instances found |
| **INCV** | ✓ | Compare expected reach of "publish article on dev.to" vs "publish nowhere" on `clarity` and `permission` dimensions; INCV holds iff strict positive on at least one |
| **CTRST** | ✓ | `¬B` is non-empty: "hype piece without examples"; counter-form is detectable by reading the published article and counting concrete examples |

**DELV check (DomainDiscipline):** the title *"Claude Skills Fail Silently. Here Is My Solution."* is in finding form, not directive form. A directive would be *"Stop using prose skills."* The finding form invites the reader to ask themselves whether their skills fail silently before continuing. DELV holds iff the reader's first cognitive response is reflection, not acceptance — observable iff the article generates response comments asking "have I noticed this in my own work?"

### Case Study 3 — Stock-Market Prediction / Trading

**Prose:** *"Buy AAPL at market open Tuesday."*

**Domain instantiation:**

```
PayoffDim(trading)  = {expected-return, sharpe-ratio, max-drawdown, capital-efficiency, opportunity-cost}
NextStep(trading)   = {place-order, modify-order, cancel-order, close-position, hedge}
```

**Trade CONTRACT:**

```
A: signal vector (price history, volume, macro indicators, momentum)
B: order intent (size, time-in-force, limit/market) → executed buy
P: account funded; market open; no halt; signal still valid at execution
¬B: drawdown beyond stop-loss threshold; signal invalidated before execution
Fallback: stop-loss at -X%; time-based exit if profit target unmet by deadline
```

**Principles audit:**

| Principle | Verdict | Test |
|---|---|---|
| **SIMP** | ✓ | The trade is a single atomic decision with explicit signal and conditions; check whether decomposition into pre-trade/trade/post-trade would change A or B — if not, SIMP holds |
| **CONS** | ✓ | (FILLED, COMPLETED) → monitor-position; (REJECTED, ABORTED) → re-evaluate signal; routing total over the StateValue × StatusValue grid |
| **FALS** | ✓ | Refuting evidence on the holding period: AAPL closes lower; out-of-sample Sharpe negative; backtest drawdown excessive — each is testable |
| **INCV** | depends on σ | In σ = "high-conviction directional bet", expected-return justifies position size; in σ = "risk-managed allocation", may fail INCV vs holding cash — situational |
| **CTRST** | ✓ | `¬B` is the stop-loss threshold + signal-invalidation condition; both are testable in real time during execution; stop-loss IS CTRST satisfaction in operational form |

---

## Working with the lifecycle skills

The lifecycle skills realize the four-step compilation process operationally. Use them rather than reimplementing the logic by hand. The three core skills are described below; for the full skill catalog see TPMN-SKILL-STANDARD §11.

### `plan-work` — boundary-drawing

**Trigger:** a prose work request larger than one atomic action.

**What it does** (per plan-work SKILL.md):

> "Decompose work into ≤9 unit-works with CONTRACTs and clarity %. CONTRACTs before execution. 5W1H gathering → search → decompose → write WP."

**Output:** `.gem-squared/work-plan/WP-ST-{N}.md` with units in `F: A → B | P` format, Clarity %, Tags. All units start in PENDING.

**Practical tip.** The skill enforces 5W1H gathering as Step 1. From plan-work SKILL.md: "Required: WHAT must be explicit (not just a vague noun). Required: WHERE must be identifiable (target environment or file/module scope). Required (top-level only): WHY must be stated." WHERE is the most-misused dimension; users confuse it with HOW. Per the SKILL.md: "WHERE = target + location, never tech stack" — tech stack belongs in HOW.

### `proceed-work` — sovereign execution

**Trigger:** a WP exists with at least one PENDING unit, and you want to execute one unit.

**What it does** (per proceed-work SKILL.md):

> "Execute ONE unit-work — fulfill CONTRACT, record Result, verify inline, retry on FAILURE. Find PENDING unit → execute → verify → retry if FAILURE → next."

**Output:** unit STATUS = COMPLETED (or ABORTED), Result field filled, State field SUCCESS or FAILURE.

**Practical tip.** The skill is one unit per invocation. From proceed-work SKILL.md CONSTRAINT: "ONE unit-work per invocation — never batch multiple units." Sovereignty is enforced explicitly — also from CONSTRAINT: "Execution strategy is executor's blackbox — skill does not dictate how." If you find yourself wanting to dictate the AI's execution approach inside a unit, the CONTRACT is too loose; tighten P, don't reach inside F.

### `verify-work` — edge-judgment

**Trigger:** a unit completed (SINGLE mode, called inline from `proceed-work`), or all units in a WP completed (BATCH mode, end-of-WP).

**What it does** (per verify-work SKILL.md):

> "Verify results against CONTRACTs — determine STATE (SUCCESS|FAILURE) per unit. Structural drift detection between CONTRACT.B and Result. Result vs CONTRACT.B → State + log."

**Output:** STATE per unit, log file at `.gem-squared/verify-work-logs/{wp_id}.md`.

**Practical tip.** The skill is structural drift detection only. From verify-work SKILL.md CONSTRAINT: "NEVER apply subjective judgment — verify against CONTRACTs only. Verification is binary per unit: SUCCESS or FAILURE — no partial credit." If a Result is technically present (every B field exists, every P holds) but qualitatively wrong (the B fields contain unsupported claims, hallucinated content, or epistemic overclaims), `verify-work` will pass it. For epistemic verification beyond CONTRACT.B conformance, use the Truth field hook.

### The Truth field — epistemic verification hook

Every unit-contract has an optional `Truth:` field. Per PSL §5.4 TruthFieldHook, it is "the formal integration point between PSL's three-phase protocol and the TPMN-checker tool (the SAS)."

**Format:**

```
- Truth: 75% | aligned | clean | ⊢ ⊨
```

- `75%` — composite truth_score (per PSL §3 EpistemicScore: `truth_score ≜ round(epistemic_score · contract_score · 100)` with default μ=1; PSL §3 notes a calibration factor μ that can be derived from accumulated runtime data, kept at 1 in default contexts)
- `aligned` — alignment between CONTRACT and Result on intent dimensions
- `clean` — SPT verdict (no S→T, L→G, Δe→∫de violations)
- `⊢ ⊨` — EEF tags present in the Result

**The distinction between `verify-work` and the Truth field hook (`/verify-by-gem2`):**

- `/verify-work` asks: *did Result fulfill CONTRACT.B given P?* — **structural** verification (binary SUCCESS/FAILURE).
- `/verify-by-gem2` (Truth field hook) asks: *was the reasoning epistemically sound?* — **substantive** verification (graded truth_score with epistemic and contract sub-scores).

Both can pass independently. Both can fail independently. A Result can fulfill its structural CONTRACT.B (every field present, P holds) while containing unsupported claims that fail epistemic audit — exactly what happened to v1 of this manual.

**When to use the Truth field hook:**
- A unit's Result includes substantive reasoning (not just a file write)
- Stakes are high (production deployment, irreversible action)
- You want a second-opinion epistemic audit beyond `verify-work`

**When to skip:**
- The unit is mechanical (rename a file, run a build script)
- `verify-work` already provides sufficient confidence for the unit type
- Latency matters — Truth scoring takes time

---

## Patterns to watch for

Four common failure modes when compiling prose to TPMN. The first three come from PSL §1.5 Compilation_Failures. The fourth was introduced when the geometric ontology was formalized to catch the vocabulary-conflation mistake.

### Pattern 1 — Domain content smuggled into universal principles

**Symptom** (per PSL §1.5 Pattern_1_Domain_Smuggling):

> "The principle reads correctly when applied in the original domain but produces nonsense in a different domain."

**Example:** `PayoffDim` hard-coded as `{clarity, permission, optionality}` (marketing-specific) inside the INCV principle definition. Looks fine when applied to marketing claims; falls apart when applied to SDLC.

**Why it happens:** familiarity with one domain. The author writes what they know.

**Fix:** parameterize. `PayoffDim` is a function of domain, not a fixed set. If weighting varies within a domain (launch vs. sustain phase), add `situation σ` as a second parameter. PSL §9.2 has the formal protocol.

### Pattern 2 — NL leakage outside its localization

**Symptom** (per PSL §1.5 Pattern_2_NL_Leakage):

> "The operator reads more like a sentence than a formal expression."

**Example:**

```
DELV(c, L) ≜ delivery of c is question form means L will reflect on c
```

NL is doing structural work in the body of the operator.

**Fix:** confine NL to a single named predicate or comment.

```
reflects(L, c) ≜ "L generates own conclusion about c"   (* NL-localized *)

DELV(c, L) ≜ form(c) = question ⇒ reflects(L, c)
```

NL only carries the meaning of `reflects` now. The operator structure is formal.

### Pattern 3 — TLA+ overreach

**Symptom** (per PSL §1.5 Pattern_3_TLA_Plus_Overreach):

> "Sequence operators or conditional modalities applied to something that is a single static test."

**Example:** `safe(r) ≜ IF tests-pass THEN ¬breaking ELSE breaking` for a safety predicate that is actually a single conjunction.

**Fix:** if the prose says "X must be true" rather than "first X, then Y" or "if A, then B", ALG+SET alone is sufficient.

```
safe(r) ≜ tests-pass(r) ∧ ¬breaking(r)
```

### Pattern 4 — Vocabulary conflation

**Symptom:** point/line/face and STATE/STATUS/SET used interchangeably. STATE treated as a primitive (it is not — it's a relation per PSL §0.3). SET treated as identical to face without context (they are not — a SET is a bounded category WITHIN a face; a face is the containing local complex space ℂ_F). Adjectives tagged as STATE (they are STATUS — vectors per PSL §0.3 line.note: "All adjectives are STATUS, not STATE").

**Why it happens:** the two vocabularies operate at two different Kantian levels — ontological (noumenal, what beings ARE) vs. topological (phenomenal, how beings APPEAR). Per PSL §0.0 KantianAlignment.statement:

> "Ontological vocabulary names the noumenal — the being of elements in itself, beyond direct access. Topological vocabulary names the phenomenal — how being appears in relation, computable and traceable."

**Fix:** re-read PSL §0.0 KantianAlignment and §0.3 GeometricOntology. The mapping:

- point/line/face = noumenal primitives (what beings *are*)
- STATE/STATUS/SET = phenomenal relations (how beings *appear*)

If you find yourself using STATE and point as parallel terms, the levels are conflated.

---

## Workflow guidance

How to integrate TPMN into actual work.

### Starting a new project

Run `gem2-init` (or equivalent) to install the lifecycle skills and scaffolding. Create a project skill or `references/` directory for project-specific patterns. First work request: invoke `/plan-work` with the prose. The 5W1H gathering surfaces what's vague before any code is written. PSL §0.2 SIMP_Principle frames Clarity as a SIMP audit measure; the operational heuristic of `Clarity < 70%` indicating too-vague input is a project tunable, not a validated boundary — adjust per project.

### During execution

Use `/proceed-work` for each unit. **Do not batch.** Edge control = one unit, one judgment (per proceed-work SKILL.md CONSTRAINT). Read the Result before approving the next unit. Check that what was produced matches your intent (separate from CONTRACT conformance, which `verify-work` checks). If a unit FAILs verification: read the verification log. Determine if the CONTRACT was wrong (re-plan) or the execution was wrong (retry). If you find yourself wanting to dictate **how** the AI executes inside a unit, the CONTRACT is too loose. Tighten P. Don't reach inside F.

### Auditing existing work

Open the Work-Plan file. For each unit: does the CONTRACT have non-empty `¬B` declared? If not, the unit fails the CTRST test by definition (per PSL §0.2 CTRST_Principle.contract_form: "A CONTRACT without ¬B fails CTRST — the success path implies a failure path that has not been named"). Check Tags: are they in `{verb-ing}-{object}` format? If not in that format, the unit is harder to find via `/search-kg` cross-session retrieval (⊨ inferred from `/search-kg` using Tags as primary index per the lifecycle skills). Check Clarity %: anything below the project's chosen threshold is a candidate for sub-decomposition. Run `/search-kg` with the WP's primary tags. If the AI built this from scratch instead of finding prior art, that's a knowledge-graph gap to close.

### Refactoring prose into TPMN

Apply Step 1 to each paragraph: tag every meaning-bearing word as point/line/face. Group STATE assertions and STATUS observations. For each named action: write the `F: A → B | P` form. For each implicit category: write the SET definition. Audit against the five principles (per PSL §10 SOUND_Composite). The compilation patterns in this manual (Section *Worked example*, Section *Three case studies*) suggest most prose passes SIMP (it has implicit structure) and most fails CTRST (wrong-form rarely declared) — but verify against your own corpus rather than treating the pattern as universal. The output is the formal version. Compare against the prose for completeness — if anything is lost, the compilation missed it.

---

## Reader paths

Different readers benefit from different starting points.

### "I'm a developer using AI agents (Claude Code, Codex, Cursor)"

- **Start with:** this manual's *Working with the lifecycle skills* section.
- **Then read:** PSL v0.5.2 §0.2 (compilation principles, just the names), §6 (CONTRACT archetype).
- **Practice:** install lifecycle skills, plan one real WP, execute, verify. Read the WP and verification log carefully.
- **Skip until needed:** PSL §0.0 Philosophical Foundation, PSL §0.3 Geometric Ontology.

### "I'm a spec author writing CONTRACTs by hand"

- **Start with:** the *Worked example, line by line* section above.
- **Then read:** PSL v0.5.2 §1.5 (four-step process), §6 (CONTRACT archetype), §10 (SOUND composite test).
- **Practice:** take three prose claims from your existing work and compile them. Audit against the five principles.
- **Skip until needed:** PSL §1.2 Panini_Adaptation full detail (read after Step 3 becomes second nature).

### "I'm reviewing or auditing TPMN work"

- **Start with:** this manual's *Auditing existing work* sub-section.
- **Then read:** PSL v0.5.2 §10 SOUND, §1.5 Compilation_Failures (patterns 1–4).
- **Practice:** audit one existing WP. The auditing checklist applied to v1 of this very manual found 4 of 9 unit-contracts had `¬B`/CTRST violations on independent audit — that is the kind of finding to expect.
- **Skip until needed:** PSL §3 EEF and §4 SPT formal machinery (read when graded scoring is needed).

### "I'm extending TPMN to a new domain"

- **Start with:** PSL v0.5.2 §9.2 Domain_Extension_Protocol.
- **Then read:** this manual's *Three case studies* section as templates.
- **Practice:** define `PayoffDim(your-domain)`, `NextStep(your-domain)`, decide whether DomainDiscipline is needed.
- **Skip until needed:** TPMN-SKILL-STANDARD §11 (read when building domain-specific skills).

### "I'm orchestrating multiple agents or composing MANDATEs"

- **Start with:** PSL v0.5.2 §0.4 CompositionBridge (G_ij formal structure).
- **Then read:** GEM²-Core §Lemma 5 (Connect / ValidHandoff / orchestration rule).
- **Practice:** identify the typed handoff between two of your agents. What is B_i? What is A_j? What is P_ij? If P_ij is empty or uncheckable, the handoff is not a valid G_ij — tighten before composing.
- **Skip until needed:** the within-MANDATE Panini set_contract details (composition is across MANDATEs; Panini is internal to each).

### "I'm trying to understand why TPMN exists"

- **Start with:** PSL v0.5.2 §0.0 Philosophical Foundation.
- **Then read:** the dev.to articles — *Claude Skills Fail Silently. Here Is My Solution.*, *Three Wounds That Prose Skills Cannot Fix*, *Claude Skills want ALL*.
- **Practice:** examine one of your existing AI workflows. Where does silent failure happen? Where do prose instructions degrade across context?
- **Skip until needed:** PSL §0.3 GeometricOntology details (the philosophical motivation in §0.0 is sufficient for orientation).

---

## Reference index

| Concept | Location |
|---|---|
| GEM² universe | PSL §0.1 GEM²_Definition |
| ΣΔ Principle (discrete categories) | PSL §0.1 ΣΔ_Principle |
| Kantian alignment (noumenon/phenomenon) | PSL §0.0 KantianAlignment |
| GEM² as Riemann approximation | PSL §0.0 GEM²_RiemannFraming |
| Human-at-the-edge architecture | PSL §0.0 ControlAtTheEdge |
| Sovereignty of F | PSL §0.0 SovereigntyOfF |
| Geometric primitives (point/line/face) | PSL §0.3 GeometricOntology.primitives |
| Topological relations (STATE/STATUS/SET) | PSL §0.3 GeometricOntology.relations |
| Dynamic axiom (STATUS · point · THRESHOLD → STATE) | PSL §0.3 DynamicAxiom |
| Per-MANDATE Panini | PSL §0.3 PerMandatePanini |
| MANDATE as face | PSL §0.3 MandateAsFace |
| ℂ_F local complex space (locality) | PSL §0.3 GeometricOntology / Core §0–§Lemma 2 |
| GEM² Composition Bridge (G_ij) | PSL §0.4 CompositionBridge / Core §Composition Bridge |
| Five compilation principles | PSL §0.2 Compilation_Discipline |
| SIMP — Sufficient Simplicity | PSL §0.2 SIMP_Principle |
| CONS — Predefined Consequence | PSL §0.2 CONS_Principle |
| FALS — Falsifiability | PSL §0.2 FALS_Principle |
| INCV — Selection Incentive | PSL §0.2 INCV_Principle |
| CTRST — Contrast / Negative Contract | PSL §0.2 CTRST_Principle |
| Composite test SOUND | PSL §10 SOUND_Composite |
| Four-step compilation process | PSL §1.5 Compilation_Process |
| Compilation failure patterns | PSL §1.5 Compilation_Failures |
| Pattern 1 (Domain Smuggling) | PSL §1.5 Pattern_1_Domain_Smuggling |
| Pattern 2 (NL Leakage) | PSL §1.5 Pattern_2_NL_Leakage |
| Pattern 3 (TLA+ Overreach) | PSL §1.5 Pattern_3_TLA_Plus_Overreach |
| Pattern 4 (Vocabulary Conflation) | PSL §1.5 Pattern_4_Vocabulary_Conflation |
| Four-layer grammar (TLA+/Panini/Math/NL) | PSL §1 TPMN_Grammar |
| Symbol governance (Tier1 fixed) | PSL §2 SymbolGovernance |
| EEF tagging system (⊢ ⊨ ⊬ ⊥ ?) | PSL §3 EEF |
| Truth score formula | PSL §3 TruthScorePolicy |
| SPT violation registry (S→T, L→G, Δe→∫de) | PSL §4 SPT |
| Three-phase protocol (P/Inline/O) | PSL §5 TPMN_PRO |
| Truth field hook (SAS integration) | PSL §5.4 TruthFieldHook |
| CONTRACT archetype (`F: A → B \| P`) | PSL §6 CONTRACT |
| Domain Extension Protocol | PSL §9.2 Domain_Extension_Protocol |
| Tagging system (`{verb-ing}-{object}`) | LIFECYCLE-GUIDE §1 |
| Work-Plan structure | LIFECYCLE-GUIDE §2 |
| Unit-Contract definition | LIFECYCLE-GUIDE §3 |
| STATUS vs State distinction | LIFECYCLE-GUIDE §3 status_vs_state |
| `plan-work` (boundary-drawing) | SKILL-STANDARD §11 / plan-work SKILL.md |
| `proceed-work` (sovereign execution) | SKILL-STANDARD §11 / proceed-work SKILL.md |
| `verify-work` (edge-judgment) | SKILL-STANDARD §11 / verify-work SKILL.md |
| Full skill catalog | SKILL-STANDARD §11 |

---

## Closing notes

This manual will go stale. PSL evolves. Skills evolve. Specifications drift as the domain they describe extends. When this manual no longer matches PSL, rewrite it.

TPMN imposes overhead. The framework targets situations where this overhead is justified by the cost of silent failure — autonomous pipelines, multi-step workflows, agentic systems, decisions where the wrong answer is expensive. The judgment of whether your situation justifies the overhead is yours, not the framework's.

A note on what produced this manual. v1 of this manual was produced under the same TPMN three-phase discipline (plan-work → proceed-work → verify-work). Producer self-verification claimed all 9 unit-contracts SUCCESS at average 89% Clarity. Independent edge-verification via the gem2 truth filter (OpenAI provider) scored the same 9 units at average 47% truth_score, with 6 of 9 flagged Unreliable. This v2 was re-planned with the audit findings as input. The v1 → v2 process is itself a worked example of the framework's L0/L1/L2 architecture: structural authoring (L0), structural verification (L1, /verify-work), epistemic verification (L2, /verify-by-gem2). L2 caught what L0 + L1 missed.

Plan one real work-plan. Watch what 5W1H gathering surfaces about your prose. Run the units. When verification fails, read the log before fixing the code — the log is where the framework speaks.

Then ship.

---

*How to TPMN — Field Manual v0.5.2*
*Companion to TPMN-PSL v0.5.2 · 2026-05-04*