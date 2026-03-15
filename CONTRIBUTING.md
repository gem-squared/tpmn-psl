# Contributing to TPMN-PSL

TPMN-PSL is an open specification. Contributions are welcome in three forms:
domain extensions, base spec corrections, and tooling.

---

## 1. Domain Extensions (Primary Contribution Path)

The base spec defines the notation and protocol. Domain experts define the rules
for their field. This is where the spec becomes useful in practice.

**Target domains currently open:**
- Medical / Clinical
- Legal / Regulatory
- Finance / Investment
- Research / Academic
- SDLC / Software Engineering
- Marketing / Product Claims
- And any domain where AI makes claims that carry real consequences

**What makes a good domain extension:**
- Tier2 glyphs that map to real epistemic distinctions your field already uses
- P/O checks that catch errors practitioners in your domain actually make
- SPT violations grounded in documented failure modes, not intuition
- CONTRACT archetypes derived from real workflows, not hypothetical ones

**To submit a domain extension:**

1. Fork the repository
2. Copy the template: `extensions/template/tpmn-domain-spec-0.1.5-p.md`
3. Create: `extensions/[domain]/tpmn-[domain]-spec-0.1.0.md`
4. Fill every `[placeholder]` with domain-grounded content
5. Open a pull request with a brief rationale for each addition

**Extension rules (from §9 of the spec):**
- Declare `EXTENDS TPMN_PSL (* v0.1.5-p *)` in the module header
- Tier1 glyphs `⊢ ⊨ ⊬ ⊥ ?` MUST NOT be redefined
- New Tier2 glyphs must be defined before use
- P0–P5 and O1–O8 must be preserved; additional checks may be added
- EEF_Record structure must be preserved; fields may be added, not removed

---

## 2. Base Spec Corrections

The spec is stable at v0.1.5-p but not finalized at v1.0.0.
Corrections are welcome for:
- Logical inconsistencies within the spec
- Notation errors (TLA+, math, grammar)
- Glossary gaps or imprecisions
- Philosophical mapping errors (§7)

**Not in scope for base spec PRs:**
- Implementation details of any specific checker tool
- Platform-specific actor pipelines
- Training or fine-tuning methodology

**To submit a correction:**
1. Open an issue describing the inconsistency with specific section references
2. Include a proposed fix in TPMN notation where possible
3. PRs for corrections must include a changelog entry

---

## 3. Tooling and Implementations

If you have built a tool that implements TPMN-PSL (checker, linter, IDE plugin,
CI integration), open an issue to add it to the Implementations section of the README.

**To qualify for listing:**
- Implements at least P-phase validation or O-phase verification
- References TPMN-PSL version explicitly
- Is publicly accessible (open source or documented API)

---

## Review Process

All PRs are reviewed against three criteria:
1. **Spec conformance** — does the contribution respect §9 Extension Protocol?
2. **Epistemic grounding** — are claims in the contribution itself ⊢ or ⊨ tagged correctly?
3. **Domain authority** — for domain extensions, is the contributor or reviewer a domain practitioner?

PRs that introduce `⊬` claims without basis statements will be returned for revision.

---

## Code of Conduct

Contributions are evaluated on technical merit. All discussion should reference
the spec text, not abstract opinion. Disagreements about notation choices should
be resolved by reference to §1 Grammar rules.

---

## Questions

Open a GitHub Discussion. Do not open issues for general questions about TPMN concepts.

---

*TPMN-PSL v0.1.5-p · CC-BY 4.0 · Inseok Seo · 2026*
