---
name: "named-persona-adversarial-review"
description: "Code review with real engineers' philosophies, not abstract roles. Catches what automated bots and generic reviewers miss."
---

# Named-Persona Adversarial Review

> **TL;DR:** Abstract roles find abstract problems. Named people with searchable, citable philosophies find problems you would actually fix. This upgrades your review beyond what bots and generic reviewers can provide.

**Triggers:** "review this PR with real engineers" | "named persona review"

## Example Output

```
CRITICAL [Torvalds]: Special-case error handling at auth.ts:47.
  "Eliminate the special case and the error disappears entirely."
WARNING [Thompson]: parseConfig() does 3 unrelated things. Split.
NOTE [Jobs]: Error message "EACCES:13" means nothing to users.
Verdict: CONCERNS -- fix CRITICAL before merge.
```

## Problem

Generic adversarial review produces generic findings. This grounds each persona in real, searchable philosophy -- what Linus Torvalds actually said about good taste, not what an AI thinks a "security auditor" might say.

**Before/after:** `adversarial-reviewer` -> "Consider adding error handling here." Named-persona -> "Linus would ask: why is this even a special case? Eliminate the special case and the error handling disappears."

**Cost:** 1 round ~ 8-12 min. Comparable to waiting for CI.

## Quick Start

**Starter:** Ken Thompson + Linus Torvalds + Steve Jobs. Works today.

```
1. Search "[Name] engineering philosophy" -- extract 3-5 criteria from actual quotes
2. Role-play all 3 -- MUST find >=1 issue each
3. Deduplicate -- 2+ hits -> severity upgrade
4. Output: structured report + post to PR as comment (or save to file)
5. Feynman check: "Would they actually say this?"
```

## Persona Pools

**Product** (pick 1 per round -- mandatory):
| Persona | Known For | Best For |
|---------|-----------|----------|
| Steve Jobs | Design is how it works | UX, onboarding |
| Marty Cagan | Problem not features | PRDs, feature specs |
| Intercom PM | First 30 seconds | Docs, READMEs, quick starts |

**Engineers** (pick 2 per round):
| Persona | Known For | Best For | Blind Spot |
|---------|-----------|----------|------------|
| Ken Thompson | Do one thing well | Architecture, API | UX, documentation |
| Linus Torvalds | Eliminate special cases | Logic, data structures | User empathy, DX |
| John Carmack | Performance as moral craft | Algorithms, critical paths | Simplicity, minimalism |
| Greg Brockman | Find the boundary conditions | Complex systems, integration | Aesthetics, process |
| Kent Beck | Simplicity, feedback, courage | Process, team practices | Performance, security |

**Routing:**
- Code -> Torvalds + Carmack + Jobs
- Architecture -> Thompson + Brockman + Cagan
- Documentation -> Thompson + Beck + Intercom PM
- Performance -> Carmack + Torvalds + Jobs

## The Process

### Step 0: Read Twice
What changed (pass 1). Why + trade-offs (pass 2). Multi-file -> trace one end-to-end path.

### Step 1: Search
`"[Name] engineering philosophy code review principles"`. Extract from quotes. Never improvise.

### Step 2: Review (3 independent)
Each gets Mindset (from search), Priorities (3-5 criteria), Finding (>=1 issue with philosopher's reasoning).

### Step 3: Synthesize & Post
Merge duplicates. Cross-persona -> severity upgrade. Post as PR comment or save to file.

## Feynman Honesty Check

1. Would [Name] actually say this?
2. Did I cite real philosophy, or write generic advice?
3. All NOTE-level? -> You're not really switching perspectives. Switch at least 2 personas and re-review.

## When to Use

- You want review quality beyond what automated bots can provide
- Self-authored PR needs pre-submit hardening
- `adversarial-reviewer` findings feel generic
- Auth, data, architecture, public API changes

## Exit Condition

- CLEAN on 2 consecutive rounds -> done
- CLEAN on round 1 for low-impact PRs -> done
- BLOCK/CONCERNS -> fix and re-review

## Cross-References

- **Extends:** `adversarial-reviewer` (alirezarezvani/claude-skills)
- **Advanced:** For curated persona pools with manager curation, see `persona-pool.md` and `dual-pool-review` methodology.
