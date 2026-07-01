# Persona Principles — sourced, with confidence levels

> **Rule:** Cite the principle, not an invented verbatim quote. If you cannot reach at least *moderate* confidence for a persona on the point you're making, drop that persona rather than fabricate.

Each attribution carries a confidence level:
- **high** — the persona has a verifiable record of saying/doing/writing this principle; a source is listed below
- **moderate** — widely attributed to the persona and consistent with their body of work, but the exact source is not pinned. Paraphrase only — do **not** wrap in quotation marks as if verbatim
- **low / unknown** — inferred from general reputation. May be used as an *attention-directing lens* only, must be labeled, and must never be presented as a quote

---

## Engineers

### Linus Torvalds
- **"Good taste": eliminate the special case.** In his 2016 TED talk he walked through a linked-list deletion example — after refactoring, the conditional branch disappears entirely. The special case is *gone*, not handled. Use for scrutinizing branch logic and data structures.
  *(confidence: high — TED, "The mind behind Linux," Feb 2016)*
- **"Never break userspace."** A long-standing, repeatedly stated kernel rule: any change that breaks existing userspace programs is a regression, no exceptions. Use for reviewing backward compatibility and public APIs.
  *(confidence: high — documented across LKML; e.g. the 2012 "we do not break userspace" thread)*

### Ken Thompson
- **Trust boundaries — "You can't trust code that you did not totally create yourself."** The core argument of his 1984 Turing Award lecture *Reflections on Trusting Trust* (the compiler backdoor). Use for scrutinizing supply chain, third-party code, and input you didn't write.
  *(confidence: high — CACM, Aug 1984)*
- **Do one thing well.** The Unix philosophy: small, composable tools (McIlroy's formulation; Thompson co-created Unix and embodies this philosophy). Use for scrutinizing functions/modules that do too many things.
  *(confidence: high for the Unix philosophy; moderate as a *direct* Thompson quote — it is McIlroy's phrasing)*

### John Carmack
- **Measure first, then optimize; optimization is craft, not guessing.** Pervades his .plan files, QuakeCon talks, and interviews — profile real hot paths, don't speculate. Use for scrutinizing unsupported performance claims.
  *(confidence: high as a documented stance; moderate on any specific verbatim wording)*
- **Code is slow because you haven't traced a real execution path — surface-level review has the same failure mode.** Consistent with his measurement-first approach: profile the hot path before changing anything. Use for scrutinizing performance reviews that lack profiling data or execution-path analysis.
  *(confidence: moderate — consistent with his documented approach across .plan files, QuakeCon talks, and interviews)*

### Kent Beck
- **Simple design + "Make it work, make it right, make it fast" (in that order).** From *Extreme Programming Explained* (1999) and the XP simple-design rules (passes tests, reveals intent, no duplication, fewest elements). Use for scrutinizing premature complexity and testability.
  *(confidence: high — *XP Explained*, Addison-Wesley, 1999)*
- **Build the mental model before the API.** Often attributed to Beck's teaching approach. Use for scrutinizing whether the conceptual model is clear before implementation details.
  *(confidence: moderate — consistent with XP's "reveals intent" principle; not a pinned Beck quote)*

### Fred Brooks
- **Essential vs. accidental complexity.** From *No Silver Bullet* (1986) and *The Mythical Man-Month* (1975): some complexity is inherent to the problem; some is self-inflicted by tools/design. Use for scrutinizing whether complexity in a diff is essential or accidental.
  *(confidence: high — IEEE Computer, 1987; MMM, 1975)*

### Rich Hickey
- **Simple vs. Easy — simple (objective, one braid) vs. easy (subjective, familiar).** From "Simple Made Easy" (Strange Loop 2011). Use for scrutinizing design decisions that trade simplicity for ease.
  *(confidence: high — Strange Loop 2011 keynote, transcribed)*
- **Programming is not about writing code — it's about understanding.** A consistent emphasis on understanding the problem domain before coding. Use for scrutinizing implementations that lack domain modeling.
  *(confidence: moderate — consistent with his talks/writing; specific wording may vary)*

### Greg Brockman
- **Systems thinking, boundary conditions first.** OpenAI co-founder era emphasis on system-level thinking — define boundaries and failure modes before implementation. Use for scrutinizing complex system integration and edge cases.
  *(confidence: moderate — consistent with OpenAI technical blog posts and talks; no single canonical source)*
- **Find the system's boundary conditions and the code writes itself.** Use for scrutinizing large PRs that lack boundary definitions.
  *(confidence: low — inferred from general approach; label as inference, not quote)*

### Google SRE (collective, not individual)
- **Reliability first — every release equals a page.** From *Site Reliability Engineering* (O'Reilly, 2016). Use for scrutinizing error handling, monitoring coverage, and release risk.
  *(confidence: high — *SRE Book*, O'Reilly, 2016, multiple chapters)*
- **Error budgets: 100% reliability is the wrong target.** Use for scrutinizing over-engineered reliability guarantees.
  *(confidence: high — SRE Book, Ch. 3 "Embracing Risk")*
- **Note: Google SRE is a team/methodology, not an individual. In named-persona review, label as "SRE (methodology)" — do not attribute to a person.**

### Dan Abramov
- **One hook, one data source — let the caller's mental model map 1:1 to the data flow.** From React documentation and Just JavaScript teaching style. Use for scrutinizing hook/component design coupling.
  *(confidence: moderate — consistent with React docs and his writing; no single canonical quote)*

### Simon Wardley
- **"Map first, then decide."** The core method of Wardley Mapping: understand a component's evolution stage (genesis→custom→product→commodity) before deciding what to do. Use for scrutinizing technology choices and build-vs-buy decisions.
  *(confidence: high — *Wardley Mapping* (online book), multiple chapters; also "Crossing the River by Feeling the Stones" 2019)*

---

## Product

### Steve Jobs
- **"Start with the customer experience and work backward to the technology."** Stated on stage at WWDC 1997. Also: "Design is not just what it looks like — design is how it works" (NYT Magazine, 2003). Use for scrutinizing error surfaces, onboarding, and complexity the user is forced to absorb.
  *(confidence: high — WWDC 1997; NYT Magazine, Nov 30, 2003)*
- **Simplicity as intuition — first impressions determine adoption.** A consistent product philosophy. Use for scrutinizing first-use experience.
  *(confidence: high as documented philosophy; moderate on any single verbatim formulation)*

### Marty Cagan
- **"Fall in love with the problem, not the solution."** Core theme of *Inspired* (2008/2017) and *Empowered* (2020), SVPG. Use for scrutinizing scope creep, feature-first thinking, and goal misalignment.
  *(confidence: high — SVPG / *Inspired*)*
- **User value > engineering implementation.** Use for scrutinizing engineer-self-gratification features in PRDs/feature specs.
  *(confidence: high — consistent with SVPG product framework)*

### Des Traynor (Intercom)
- **First experience determines adoption; onboarding and messaging ARE the product.** Pervades Intercom's writing on onboarding and his talks. Use for scrutinizing READMEs, quick-starts, and the first 30 seconds.
  *(confidence: high as Intercom's documented position; moderate on exact attribution to Traynor personally)*

### Don Norman
- **Affordance, signifier, conceptual model.** *The Design of Everyday Things* (1988/2013). Use for scrutinizing whether UI elements communicate the right mental model to users.
  *(confidence: high — *The Design of Everyday Things*, multiple editions)*
- **"Good design is actually harder to notice — because it serves your needs without drawing attention."** Use for scrutinizing interface friction and unnecessary cognitive load.
  *(confidence: high — *The Design of Everyday Things*, Ch. 1)*

### Jesse Schell
- **100+ lenses for multi-perspective examination.** *The Art of Game Design: A Book of Lenses* (2008). Use for scrutinizing whether creative/experience products have been considered from multiple angles.
  *(confidence: high — *The Art of Game Design*, 2008; 100+ documented lenses)*
- **Players learn rules by playing, not by reading.** Use for scrutinizing tutorials, onboarding, and interactive learning materials.
  *(confidence: moderate — consistent with *The Art of Game Design*; specific wording may vary)*

### Kathy Sierra
- **Reduce cognitive load — users need to feel "I can do this" before they're willing to face "I need to learn this."** Core theme of the *Head First* series and *Badass: Making Users Awesome* (2015). Use for scrutinizing learning material entry barriers.
  *(confidence: high — *Badass*, O'Reilly, 2015; also *Head First* series design principles)*
- **Don't make users feel stupid.** Use for scrutinizing API docs, tutorials, CLI error messages, and architectural choices.
  *(confidence: moderate — consistent across her work; specific formulation may vary)*

---

## Information / Visual Design

### Stephen Few
- **"Functional density > decoration."** *Information Dashboard Design* (2006) and *Show Me the Numbers* (2004). Maximize data-ink ratio. Use for scrutinizing dashboards, reports, and print materials.
  *(confidence: high — *Information Dashboard Design*, O'Reilly, 2006)*
- **Use color to encode data dimensions, not to decorate.** Every visual element should carry information. Use for scrutinizing purely decorative use of color.
  *(confidence: high — consistent across both major books)*

### Keith Tam
- **Chinese typography requires 1.5-2× the line spacing of Latin text (stroke density is 3-5× higher).** Use for scrutinizing Chinese print materials (resumes, reports, certificates).
  *(confidence: moderate — consistent with documented Chinese typography standards; Tam is a recognized authority in Chinese typography at University of Reading)*
- **Type size hierarchy, weight contrast, and line spacing are the three pillars of Chinese typography.** Use for scrutinizing visual hierarchy in Chinese documents.
  *(confidence: moderate — consistent with his published work and teaching)*

---

## Managers (Fixed Pool)

### Patty McCord
- **"Zero sugarcoating + results-driven + unafraid to reorganize."** "How Netflix Reinvented HR" (HBR, 2014) and *Powerful* (2018). Use for scrutinizing whether there are concrete deliverables vs. process theater.
  *(confidence: high — HBR, Jan-Feb 2014; also *Powerful*, 2018)*

### Ed Catmull
- **Braintrust — multi-perspective review of creative work.** The core mechanism from *Creativity, Inc.* (2014): a group of experienced peers gives honest feedback but has no decision-making authority. Use for scrutinizing team composition for creative/strategy/portfolio reviews.
  *(confidence: high — *Creativity, Inc.*, Random House, 2014, Ch. 5 "Honesty and Candor")*

---

## Theory Basis (why multiple named lenses work)

- **Edward de Bono, *Six Thinking Hats* (1985)** — Deliberately switching perspectives surfaces problems a single stance misses. Named personas are "hats" with substance. (confidence: high)
- **Daniel Kahneman, *Thinking, Fast and Slow* (2011)** — Forcing explicit, effortful (System 2) review counters rapid, confirmation-biased intuitive judgment. Grounding + integrity check are System-2 forcing mechanisms. (confidence: high)
- **Richard Feynman, *Cargo Cult Science* (Caltech commencement, 1974)** — "You must not fool yourself — and you are the easiest person to fool." The integrity check operationalizes this principle. (confidence: high)

---

## How to use this file during a review

1. Select personas per the routing table
2. Pull their principles above **before** reading the code — so you are *applying* principles, not rationalizing pre-formed opinions
3. Every finding must name the principle + confidence level. If your point is not in this file and cannot be verified to at least *moderate* via search → either find another persona whose documented principles cover the point, or report the finding on pure technical merit without a name attached
4. You may supplement-search for a persona (e.g. "Linus Torvalds code review 2025 2026"), but newly discovered principles must be labeled confidence *low* until a verifiable source is found

## Related Files

- [`persona-pool.md`](persona-pool.md) — v2.3 dual-pool architecture (fixed + random pools, managers, evolution rules)
- [`SKILL.md`](SKILL.md) — installable Claude Code skill with routing table and quick start
- [`METHODOLOGY.md`](METHODOLOGY.md) — full methodology paper with architecture, validation, and risk analysis