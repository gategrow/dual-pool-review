# Dual-Pool Adversarial Review

> AI-assisted code & content review using **real people's documented philosophies**, not abstract roles. Fixed pool for depth, random pool for surprise. Manager-curated per task. **Principle-first with confidence levels — never fabricate a quote.**

**Status: Methodology + Reference Implementation** — This repo describes and demonstrates the dual-pool adversarial review methodology. It includes a reference Claude Code skill and pre-sourced persona principles. It is NOT a standalone tool.

## What This Is

This repository is three things:

1. **A methodology paper** — [`METHODOLOGY.md`](METHODOLOGY.md) describes the dual-pool adversarial review approach: why it works, how it's structured, and what problems it solves. This is the primary artifact.

2. **A reference implementation** — [`SKILL.md`](SKILL.md) is a Claude Code skill that implements the methodology. It produces structured, confidence-tagged code reviews using named personas with sourced principles. Use it as-is, adapt it, or treat it as a worked example.

3. **A sourcing backbone** — [`persona-principles.md`](persona-principles.md) documents the engineering, product, design, and management principles of 20+ named figures, each with verifiable sources and confidence levels. This is the anti-fabrication foundation — every attribution carries a confidence tag (high/moderate/low). If a persona's principle cannot be sourced, drop the persona.

### What's Missing for Tool Status

This is honest about what it is and isn't. The following would be needed to call it a tool:

1. **Standalone CLI** — The review currently runs inside Claude Code as a skill. There's no `pip install`-able package with a `dual-pool-review` command.
2. **Programmatic validation** — Confidence levels and principle sourcing are manual. A tool would verify attribution against persona-principles.md automatically.
3. **CI integration** — No GitHub Actions, pre-commit hooks, or bot accounts that run reviews automatically on PRs.
4. **Test suite** — The methodology is validated through self-review (16 issues found and fixed) and community feedback (PR #866, #867 on alirezarezvani/claude-skills), but there's no automated test suite.
5. **External validation** — One-team validation on one repo's PRs. Broader validation across different codebases and teams is needed.

## Why This Exists

AI review systems typically use abstract roles — Saboteur, New Hire, Security Auditor. Abstract roles produce generic findings. "Consider adding error handling" isn't actionable.

This system uses **named real people with sourced, citable principles**. Linus Torvalds doesn't say "check for code quality." He says "eliminate the special case entirely" (TED 2016 — confidence: high). That difference turns "fix this" into "delete this."

**v1.1 (2026-07-01): Anti-fabrication discipline.** Every attribution carries a confidence level (high/moderate/low). Cite the principle, not an invented verbatim quote. Drop a persona rather than fabricate. See [`persona-principles.md`](persona-principles.md) for every persona's pre-sourced principles + sources + confidence levels.

## Architecture

```
Task enters
  |
  v
Triage Review (v1.0, 1 round)  <-- determines depth
  |
  +-- quick/standard --> v1.0 (simple, fast)
  |
  +-- deep --> v2.3 Dual-Pool Orchestration
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
- Strengths: depth, consistency, personal relevance, pre-sourced principles
- Risk: echo chamber — needs periodic audit

### Random Pool (Divergence)
- Fresh personas via web search each session
- No preset list — manager defines search keywords
- Strengths: surprise insights, blind-spot coverage, diversity
- Risk: quality variance, principles not pre-sourced (confidence ceiling: moderate)

### Orchestration Modes
- `exploit-only`: all fixed pool (repeatable tasks)
- `explore-only`: all random pool (inspiration tasks)
- `explore->exploit`: random first, fixed verify (strategy decisions)
- `exploit->explore`: fixed baseline, random challenge (portfolio review)

## Per-Round Process

1. Randomly draw a manager from current pool
2. Manager analyzes task → decides depth + required roles (2 engineers + 1 product + optional auditor)
3. Manager recruits specific workers from the worker pool
4. Team reviews — each person applies their documented philosophy. Every finding: sourced principle + confidence level. Zero-finding burden: 3+ principles the code satisfies + how
5. Output: `[Manager] picked [A,B,C] because [reason]. Found N issues. Verdict: BLOCK/CONCERNS/CLEAN`
6. Next round: new manager + keep ≤2 members from previous round

Note: earlier versions required each reviewer to find at least one issue. Community feedback correctly identified this as counterproductive — forced findings produce exactly the generic noise this method exists to escape. The refined approach: principle-first review with symmetric burden (findings need sourced principles, non-findings need equal justification).

## Key Innovations

1. **Real people, not abstract roles** — searchable, citable, sourced philosophies
2. **Principle-first, not quote-first** — cite documented stances with confidence levels, never fabricate verbatim quotes (v1.1)
3. **Dual-pool cross-orchestration** — depth + surprise, not repetition
4. **Manager curation per task** — dynamic team, not fixed template
5. **Pool evolution** — promote (random→fixed), demote (stale→removed)
6. **Digital twin matching** — fixed pool curated to user's profile

## Validation

Tested 2026-06-27 on PR #866 (alirezarezvani/claude-skills, 18.7K stars):

- **R1 Fixed (McCord)**: 10 findings — structure, format, adoption
- **R2 Fixed (Catmull)**: 8 findings — clarity, edge cases, UX
- **R3 Random (Spolsky+DuVander)**: 3 findings — positioning, first impression, output destination

**Random pool found things both fixed-pool rounds completely missed.** Cross-pool works.

Anti-fabrication discipline (confidence levels, drop-persona rule) hardened 2026-07-01 based on alirezarezvani/claude-skills PR #867.

## Limitations

- More complex than simple review (needs triage judgment)
- Fixed pool needs periodic maintenance
- Random pool depends on web search quality
- Not all tasks need deep mode
- No standalone tooling (CLI, CI integration, automated validation)

## Files

| File | Purpose |
|------|---------|
| `README.md` | This document — methodology overview and honest positioning |
| `SKILL.md` | v2.3 skill — installable in Claude Code, principle-first with confidence levels |
| `persona-pool.md` | v2.3 fixed pool design — managers, workers, roles, evolution, anti-fabrication |
| `persona-principles.md` | Sourcing backbone — every persona's documented principles + sources + confidence levels |
| `METHODOLOGY.md` | Full methodology paper — architecture, rules, validation, risk analysis |
| `LICENSE` | MIT |

## Related

- [checkgrow](https://github.com/gategrow/checkgrow) — Full AI quality toolkit
- PR [#866](https://github.com/alirezarezvani/claude-skills/pull/866) — original skill implementation
- PR [#867](https://github.com/alirezarezvani/claude-skills/pull/867) — anti-fabrication hardening (confidence levels, principle grounding)
- PR [#2365](https://github.com/affaan-m/ECC/pull/2365) — delivery-gate

## License

MIT