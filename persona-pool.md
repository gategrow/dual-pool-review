# Dual-Pool Persona Review System v2.2 · 人物审查双池系统

> **TL;DR:** Two pools, two thinking modes. Fixed pool = convergence (known experts, deep). Random pool = divergence (fresh discovery, blind-spot breaking). Cross-orchestrated for adversarial review quality.

## Two Thinking Modes · 双池的两种思维模式

| Pool 池 | Mode 思维模式 | Strengths 优势 | Risk 风险 |
|---------|-------------|---------------|----------|
| **Fixed 固定池** | **Convergence 收敛** — known best, deep mining | Stable, reliable, gets deeper each round | Echo chamber, plateauing |
| **Random 随机池** | **Divergence 发散** — unknown possibilities, break blind spots | Surprise insights, breaks echo chamber | Quality variance, may go off-topic |

## Round Flow · 流程（每轮）

1. Classify task type → select pool/orchestration mode
2. Manager pool randomly draws 1 (exclude last round's manager)
3. Manager analyzes task → determines depth + roles + recruits workers
4. Team review (≥1 finding per person)
5. Output: [Manager] chose [A,B,C] because [reason]. Found N issues. Verdict.

## Orchestration Modes · 编排模式

| Mode | When 适用 | Orchestration 编排 |
|------|----------|------|
| **exploit-only** | Repetitive tasks | All rounds: fixed pool |
| **explore-only** | Creative/inspiration tasks | All rounds: random pool |
| **explore→exploit** | Strategic decisions | R1: random → R2+: fixed |
| **exploit→explore** | Portfolio/capstone review | R1: fixed → R2+: random |

## Fixed Pool · 固定池

### Managers · 管理员

| Manager | Background | Best For |
|--------|-----------|---------|
| Patty McCord | Netflix former CTO | Concrete deliverable tasks |
| Ed Catmull | Pixar co-founder | Creative/strategy tasks |

### Workers · 工人

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

## Pool Evolution · 池子进化

- **Promotion 晋升:** Random pool worker selected 2 consecutive times + high quality → fixed pool
- **Demotion 淘汰:** Fixed pool worker 5 consecutive rounds with zero findings → removed
- **Audit 审计:** Every 10 deep tasks, review fixed pool health

## License
MIT