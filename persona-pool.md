# Dual-Pool Persona Review System v2.3

> **TL;DR:** Two pools, two thinking modes. Fixed pool = convergence (known experts, deep). Random pool = divergence (fresh discovery, blind-spot breaking). Cross-orchestrated for adversarial review quality. **v2.3: anti-fabrication discipline** — cite principles not invented quotes, every attribution with confidence level.

## Two Thinking Modes

| Pool | Mode | Strengths | Risk |
|---------|-------------|---------------|----------|
| **Fixed** | **Convergence** — known best, deep mining | Stable, reliable, gets deeper each round | Echo chamber, plateauing |
| **Random** | **Divergence** — unknown possibilities, break blind spots | Surprise insights, breaks echo chamber | Quality variance, may go off-topic |

## Round Flow

1. Classify task type → select pool/orchestration mode
2. Manager pool randomly draws 1 (exclude last round's manager)
3. Manager analyzes task → determines depth + roles + recruits workers
4. Team review — each finding mapped to a sourced principle + confidence level. Zero-finding rounds are valid per symmetric burden (cite ≥3 principles the code satisfies + explain how; see METHODOLOGY.md)
5. Output: [Manager] chose [A,B,C] because [reason]. Found N issues. Verdict.

## Orchestration Modes

| Mode | When | Orchestration |
|------|----------|------|
| **exploit-only** | Repetitive tasks | All rounds: fixed pool |
| **explore-only** | Creative/inspiration tasks | All rounds: random pool |
| **explore→exploit** | Strategic decisions | R1: random → R2+: fixed |
| **exploit→explore** | Portfolio/capstone review | R1: fixed → R2+: random |

## Fixed Pool

> **Sourcing:** Every fixed-pool persona's documented principles + sources + confidence levels are in [`persona-principles.md`](persona-principles.md). Pull principles from there BEFORE reviewing — don't guess what a persona would say.

### Managers

| Manager | Background | Best For |
|--------|-----------|---------|
| Patty McCord | Netflix former CTO | Concrete deliverable tasks |
| Ed Catmull | Pixar co-founder | Creative/strategy tasks |

### Workers

| Worker | Core Framework | Best Match |
|--------|---------------|------------|
| Rich Hickey | Simple vs Easy | Chaos → order |
| John Carmack | First principles | Games × engineering |
| Don Norman | HCI / affordance | HCI goals |
| Jesse Schell | 100+ lenses | 126-game perspective |
| Simon Wardley | Map first, then decide | Full picture before details |
| Stephen Few | Functional density > decoration | Heavy data visualization |
| Keith Tam | Chinese typography standards | Chinese print/documents |
| Dan Abramov | Mental model first | Adopt templates → internalize |
| Kathy Sierra | Reduce cognitive load | Learning materials |

## Random Pool

### Random Pool Output Spec

> Random pool workers have no predefined style. The skeleton below enforces a minimum bar (no drifting); everything else is free-form (preserves divergence value).

**Unified skeleton (all random pool workers):**
```
[LEVEL] [confidence] location — finding → reason → fix
```
- LEVEL: CRITICAL/HIGH/MEDIUM/LOW
- **confidence: high/moderate/low** (v2.3 — sourced principle confidence. Random pool workers default to `moderate` ceiling unless the principle also appears in [`persona-principles.md`](persona-principles.md))
- location: file path + line number or UI location, must be specific and locatable
- finding: one-sentence problem description, no preamble
- reason: why it's a problem (paraphrase the persona's **documented, verifiable stance** — not a fabricated quote, a paraphrased position with confidence tag)
- fix: concrete, actionable change

**Free dimensions (persona-dependent):**
- Argumentation style (data-driven/logical deduction/analogy/counter-example)
- Terminology (use the persona's domain language)
- Principle paraphrase (cite the persona's known writing/talk/stance, with confidence level, **without** fabricating quotation marks)
- Severity judgment (per the persona's value system)

**Sample review output (random pool, template only):**
> [HIGH] [moderate] `src/auth.ts:34` — token refresh fires on every request but no concurrent-duplicate check. Per Sandi Metz's "less knowledge, more action" stance (*Practical Object-Oriented Design* — objects should minimize knowledge of other objects), this implicit side-effect should be an explicit scheduling layer. Extract `TokenScheduler` singleton; request layer reads only.

> Note: principle citations must be paraphrases (not fabricated quote marks) with confidence tags. No citation = round invalid; manager should reject and re-run. Random pool workers default to `moderate` ceiling (insufficient preset grounding), unless the same principle also appears in [`persona-principles.md`](persona-principles.md).

## Mandatory Rules

1. Each person reviews through their documented principles. Zero findings is valid IF ≥3 principles the code satisfies are cited with explanation. Per symmetric burden — both findings and non-findings carry equal verification cost (see METHODOLOGY.md §Symmetric Burden).
2. 2+ people independently finding the same issue → severity promotion (+1 level)
3. User may inspect process or veto manager's picks at any time
4. Manager misdiagnoses task → round void, next round with new manager + fresh diagnosis
5. **Anti-fabrication discipline (v2.3):** Cite principles not invented quotes. Every attribution carries a confidence level (high/moderate/low). Drop a persona rather than fabricate. Fixed pool → [`persona-principles.md`](persona-principles.md) provides preset grounding. Random pool → search results extract only verifiable stances; label `confidence: low` when source is unconfirmed.

## Pool Evolution

- **Promotion:** Random pool worker selected 2 consecutive times + high quality → fixed pool
- **Demotion:** Fixed pool worker 5 consecutive rounds with zero findings → removed
- **Audit:** Every 10 deep tasks, review fixed pool health

## License
MIT