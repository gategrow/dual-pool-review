# 双池交叉审查方法论 (Dual-Pool Adversarial Review)

> AI-assisted code & content review using **real people's philosophies**, not abstract roles. Fixed pool for depth, random pool for surprise. Manager-curated per task.

## Why This Exists

Existing AI review systems use abstract roles (Saboteur, New Hire, Security Auditor). Problem: abstract roles produce generic findings — "consider adding error handling" — not actionable insights.

This system uses **named real people with searchable, citable philosophies**. Linus Torvalds isn't "an engineer who cares about code quality." He's "someone who believes special cases should be eliminated, not handled." That difference turns "fix this" into "delete this."

## Architecture

```
Task enters
  |
  v
Triage Review (v1.0, 1 round)  <-- determines depth
  |
  +-- quick/standard --> v1.0 (simple, fast)
  |
  +-- deep --> v2.1 Dual-Pool Orchestration
                  |
        +---------+---------+
        v                   v
   Fixed Pool           Random Pool
   (digital-twin       (web-searched
    matched)            fresh each time)
   stability            surprise
        |                   |
        +---------+---------+
                  v
        Cross-pool rounds
        explore<-->exploit
```

## The Two Pools

### Fixed Pool (Convergence)
- Matched to the user's digital twin (expertise, personality, goals)
- 2 managers + 9 workers across 5 roles
- Strengths: depth, consistency, personal relevance
- Risk: echo chamber — needs periodic audit
- Best for: personal projects, career decisions, portfolio review

### Random Pool (Divergence)
- Fresh personas via web search each session
- No preset list — manager defines search keywords
- Strengths: surprise insights, blind-spot coverage, diversity
- Risk: quality variance
- Best for: generic tasks, exploration, breaking fixed-pool staleness

### Orchestration Modes
- `exploit-only`: all fixed pool (repeatable tasks)
- `explore-only`: all random pool (inspiration tasks)
- `explore->exploit`: random first, fixed verify (strategy decisions)
- `exploit->explore`: fixed baseline, random challenge (portfolio review)

## Per-Round Process

1. Randomly draw a manager from current pool
2. Manager analyzes task -> decides depth + required roles (2 engineers + 1 product/designer + optional auditor)
3. Manager recruits specific workers from the worker pool
4. Team reviews (each must find >=1 issue; zero findings = invalid round)
5. Output: `[Manager] picked [A,B,C] because [reason]. Found N issues. Verdict: BLOCK/CONCERNS/CLEAN`
6. Next round: new manager + keep <=2 members from previous round

## Key Innovations

1. **Real people, not abstract roles** — searchable, citable philosophies
2. **Dual-pool cross-orchestration** — depth + surprise, not repetition
3. **Manager curation per task** — dynamic team, not fixed template
4. **Pool evolution** — promote (random->fixed), demote (stale->removed)
5. **Digital twin matching** — fixed pool curated to user's profile

## Comparison

| | alirezarezvani adversarial-reviewer | gaurav-yadav adversarial-ai-review | Dual-Pool System |
|---|---|---|---|
| Reviewers | Abstract roles (Saboteur) | Domain-specialized agents | **Real people + searchable philosophy** |
| Team formation | Fixed 3-template | 22 agent pairs | **Manager-curated per task** |
| Cross-round strategy | Rotate roles | Same agent set | **Swap pool + manager + workers** |
| Personalization | None | None | **Digital twin matching** |
| Evolution | Static | Static | **Promote/demote/audit** |

## Validation

Tested 2026-06-27 on PR #866 (alirezarezvani/claude-skills, 18.7K stars):

- **R1 Fixed (McCord)**: 10 findings — structure, format, adoption
- **R2 Fixed (Catmull)**: 8 findings — clarity, edge cases, UX
- **R3 Random (Spolsky+DuVander)**: 3 findings — positioning, first impression, output destination

**Random pool found things both fixed-pool rounds completely missed.** Cross-pool works.

## When to Use

- Code review (pre-merge hardening)
- Design doc review
- Portfolio/resume review
- Strategy decision stress-testing
- Learning methodology design
- Any scenario where "AI might be too agreeable"

## Limitations

- More complex than simple review (needs triage judgment)
- Fixed pool needs periodic maintenance
- Random pool depends on web search quality
- Not all tasks need deep mode

## Files

| File | Purpose |
|------|---------|
| `README.md` | This document — methodology overview |
| `SKILL.md` | v1.0 skill — installable in Claude Code |
| `persona-pool.md` | v2.1 fixed pool design — managers, workers, roles, evolution |

## Related

- PR [#866](https://github.com/alirezarezvani/claude-skills/pull/866) — skill implementation on alirezarezvani/claude-skills (18.7K stars)
- PR [#2365](https://github.com/affaan-m/ECC/pull/2365) — delivery-gate tool on ECC

## License

MIT — free to use, modify, distribute. Attribution appreciated.
