---
name: "named-persona-adversarial-review"
description: "Code review with real engineers' documented principles, not abstract roles. Principle-first (with confidence levels), not quote-first. Catches what automated bots and generic reviewers miss."
version: 2.3.0
---

# Named-Persona Adversarial Review

> **TL;DR:** Abstract roles find abstract problems. Named people with sourced, citable principles find problems you would actually fix. This upgrades your review beyond what bots and generic reviewers can provide.

**Triggers:** "review this PR with real engineers" | "named persona review"

## Example Output

```
CRITICAL [Torvalds]: Special-case error handling at auth.ts:47.
  "Good taste" principle: refactor so the special case disappears, not branches around it.
  (confidence: high — TED 2016)
WARNING [Thompson]: parseConfig() does 3 unrelated things.
  Unix "do one thing well" principle. (confidence: high — Unix philosophy)
NOTE [Jobs]: Error message "EACCES:13" means nothing to users.
  "Start with customer experience" principle. (confidence: high — WWDC 1997)
Verdict: CONCERNS — fix CRITICAL before merge.
```

## Attribution Discipline (read first — this is load-bearing)

This method puts real people's *principles* to work. That power is also its failure mode: **language models fabricate quotes.** To stay honest:

1. **Cite the principle, not an invented verbatim quote.** Prefer paraphrasing the persona's sourced, documented stance — not wrapping words they may never have said in quotation marks.
2. **Every attribution carries a confidence level** — `high` (sourced, listed in [`persona-principles.md`](persona-principles.md)), `moderate` (widely attributed, source not pinned, paraphrase only), `low`/`unknown` (inferred — usable as an attention-directing lens only, must be labeled, never present as a quote).
3. **If you cannot anchor a persona's lens to a real source, drop that persona.** One confident-but-wrong attribution to a living engineer is worse than one fewer reviewer. Never fabricate a quote to meet the "≥1 finding" quota.
4. **Findings must stand on technical merit.** The persona is an *attention-directing lens*, not the authority that makes the finding true. A real bug caught "through Carmack's lens" is a bug because it's a bug, not because Carmack said so.

Sourced principles + sources + confidence levels for every persona live in [`persona-principles.md`](persona-principles.md).

## Problem

Generic adversarial review produces generic findings. This grounds each persona in real, sourced philosophy — what Linus Torvalds actually demonstrated about good taste (TED 2016), not what an AI thinks a "security auditor" might say.

**Before/after:** `adversarial-reviewer` → "Consider adding error handling here." Named-persona → "Torvalds' good-taste principle: eliminate the special case so the error handling disappears entirely."

**Cost:** 1 round ~ 8-12 min. Comparable to waiting for CI.

## Quick Start

**Starter:** Ken Thompson + Linus Torvalds + Steve Jobs. Works today.

```
1. Pull each persona's sourced principles from [`persona-principles.md`](persona-principles.md) first. Search only for personas not yet covered there.
2. Role-play all 3 — each applies their documented principles. At least 1 finding expected; zero-finding rounds valid per symmetric burden (cite 3+ principles the code satisfies)
3. Deduplicate — 2+ hits → severity upgrade
4. Output: structured report with confidence-tagged findings + post to PR as comment (or save to file)
5. Feynman check: "Is this principle actually sourced, or did I fabricate it?"
```

## Persona Pools

> **Note:** The personas below form the **v1.0 "starter kit"** — simple, pick-by-role, always-ready. For the **v2.3 advanced dual-pool architecture** (fixed pool + random pool, manager curation, diversity enforcement, pool evolution, anti-fabrication discipline), see [`persona-pool.md`](persona-pool.md). The two persona sets are intentionally different — SKILL.md is the quick-start entry point, persona-pool.md is the full production system. Use SKILL.md's table when you want 3 named engineers fast; use persona-pool.md when you want a curated review with convergence + divergence.

> **Sourcing:** Every persona's documented principles + sources + confidence levels are in [`persona-principles.md`](persona-principles.md). Pull principles from there BEFORE reviewing — don't guess what a persona would say.

**Product** (pick 1 per round — mandatory):
| Persona | Known For | Best For |
|---------|-----------|----------|
| Steve Jobs | Design is how it works | UX, onboarding |
| Marty Cagan | Problem not features | PRDs, feature specs |
| Des Traynor (Intercom) | First 30 seconds | Docs, READMEs, quick starts |

**Engineers** (pick 2 per round):
| Persona | Known For | Best For | Blind Spot |
|---------|-----------|----------|------------|
| Ken Thompson | Do one thing well | Architecture, API | UX, documentation |
| Linus Torvalds | Eliminate special cases | Logic, data structures | User empathy, DX |
| John Carmack | Performance as craft | Algorithms, critical paths | Simplicity, minimalism |
| Greg Brockman | Find the boundary conditions | Complex systems, integration | Aesthetics, process |
| Kent Beck | Simplicity, feedback, courage | Process, team practices | Performance, security |

**Routing:**
- Code → Torvalds + Carmack + Jobs
- Architecture → Thompson + Brockman + Cagan
- Documentation → Thompson + Beck + Traynor
- Performance → Carmack + Torvalds + Jobs

> **Full catalog:** The routing table above covers the v1.0 starter kit. See [`persona-principles.md`](persona-principles.md) for the full 20+ persona catalog with pre-sourced principles and confidence levels, and [`persona-pool.md`](persona-pool.md) for the v2.3 dual-pool system with 9 additional workers (Hickey, Norman, Schell, Wardley, Few, Tam, Abramov, Sierra) plus managers (McCord, Catmull).

## The Process

### Step 0: Read Twice
What changed (pass 1). Why + trade-offs (pass 2). Multi-file → trace one end-to-end path.

### Step 1: Ground the Principles First
Pull each persona's documented principles from [`persona-principles.md`](persona-principles.md) (or search `"[Name] engineering philosophy principles"` and extract only verifiable stances). Do this **before** reading the code — so you are *applying* principles, not rationalizing pre-formed opinions.

### Step 2: Review (3 independent)
Each gets Mindset (one sentence from their principles), Priorities (3-5 check criteria), Finding (each issue mapped to a sourced principle + confidence level; zero findings valid if ≥3 principles the code satisfies are cited).

### Step 3: Synthesize & Post
Merge duplicates. Cross-persona → severity upgrade. Post as PR comment or save to file.

## Feynman Honesty Check

1. Is this principle actually *sourced*, or did I fabricate it?
2. Does my finding carry a confidence level? If not, why?
3. All NOTE-level? → You're not really switching perspectives. Switch at least 2 personas and re-review.

## When to Use

- You want review quality beyond what automated bots can provide
- Self-authored PR needs pre-submit hardening
- `adversarial-reviewer` findings feel generic
- Auth, data, architecture, public API changes

## Exit Condition

- CLEAN on 2 consecutive rounds → done
- CLEAN on round 1 for low-impact PRs → done
- BLOCK/CONCERNS → fix and re-review

## Cross-References

- **Sourcing backbone:** [`persona-principles.md`](persona-principles.md) — every persona's documented principles + sources + confidence levels
- **Extends:** `adversarial-reviewer` (alirezarezvani/claude-skills)
- **Upstream:** alirezarezvani/claude-skills PR #867 — anti-fabrication hardening (confidence levels, principle grounding, zero-fabrication)
- **v1.0 Quick-Start:** The persona tables on this page (Thompson, Torvalds, Carmack, Brockman, Beck; Jobs, Cagan, Traynor). Pick 3, run, done.
- **v2.3 Advanced:** [`persona-pool.md`](persona-pool.md) — completely different persona set (Hickey, Carmack, Norman, Schell, Wardley, Few, Tam, Abramov, Sierra; McCord, Catmull) with dual-pool architecture, manager curation, diversity enforcement, anti-fabrication discipline, and pool evolution rules. See also [`dual-pool-review` methodology](https://github.com/gategrow/dual-pool-review).