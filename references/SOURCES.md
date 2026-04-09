# Sources and References

## Primary Sources

### cameronfreer/lean4-skills (workflow + deep references)
- **Repository:** https://github.com/cameronfreer/lean4-skills
  MIT-licensed Lean 4 workflow pack for AI coding agents. It provides broad coverage
  for LLM-driven Lean 4 work. Our skill complements theirs: they handle proving
  workflow; we handle mathematical content knowledge.
- **Key files we draw from or reference:**
  - [lean-phrasebook.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/lean-phrasebook.md) — math→Lean translations, inspired by Tao's Lean Phrasebook
  - [mathlib-guide.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/mathlib-guide.md) — Mathlib search strategies and import patterns
  - [domain-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/domain-patterns.md) — domain-specific proof patterns
  - [measure-theory.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/measure-theory.md) — deep measure theory and conditional expectation patterns
  - [tactics-reference.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/tactics-reference.md) — comprehensive tactic documentation
  - [compilation-errors.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/compilation-errors.md) — error-by-error debugging
  - [instance-pollution.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/instance-pollution.md) — typeclass conflict patterns
  - [mathlib-style.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/mathlib-style.md) — Mathlib code style
  - [proof-golfing.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/proof-golfing.md) — proof optimization
  - [performance-optimization.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/performance-optimization.md) — build speed

### leanprover/skills (official Lean team skills)
- **Repository:** https://github.com/leanprover/skills
  Official skills from the Lean team: `mathlib-pr`, `mathlib-review`, `mathlib-build`,
  `lean-mwe`, `lean-bisect`, `lean-pr`, `nightly-testing`.

### Official Mathlib Documentation
- **Naming conventions:** https://leanprover-community.github.io/contribute/naming.html
- **Style guide:** https://leanprover-community.github.io/contribute/style.html
- **Contributing guide:** https://leanprover-community.github.io/contribute/
- **API docs:** https://leanprover-community.github.io/mathlib4_docs/
- **Mathlib overview:** https://leanprover-community.github.io/mathlib-overview.html
- **Linter docs:** https://leanprover-community.github.io/mathlib4_docs/Mathlib/Tactic/Linter/Style.html
- **Simp guide:** https://leanprover-community.github.io/extras/simp.html

### Lean 4 Documentation
- **Tactic reference:** https://lean-lang.org/doc/reference/latest/Tactic-Proofs/Tactic-Reference/
- **Naming conventions:** https://github.com/leanprover/lean4/blob/master/doc/std/naming.md
- **Grind tactic:** https://lean-lang.org/doc/reference/latest/The--grind--tactic/

### Search Tools
- **Loogle** (type-pattern): https://loogle.lean-lang.org/
- **LeanSearch** (natural language): https://leansearch.net/
- **Moogle** (semantic): https://www.moogle.ai/

## Textbooks

- **Mathematics in Lean** (Jeremy Avigad, Patrick Massot)
  https://leanprover-community.github.io/mathematics_in_lean/
- **Theorem Proving in Lean 4**
  https://lean-lang.org/theorem_proving_in_lean4/

## Blog Posts

- **"Basic probability in Mathlib"** (Rémy Degenne, 2024-10-17)
  https://leanprover-community.github.io/blog/posts/basic-probability-in-mathlib/
  Primary source for [Probability](domains/probability.md).

- **"A slightly longer Lean 4 proof tour"** (Terence Tao, 2023-12-05)
  https://terrytao.wordpress.com/2023/12/05/a-slightly-longer-lean-4-proof-tour/

- **"Formalizing the proof of PFR in Lean4 using Blueprint"** (Terence Tao, 2023-11-18)
  https://terrytao.wordpress.com/2023/11/18/formalizing-the-proof-of-pfr-in-lean4-using-blueprint-a-short-tour/

- **Tao's Lean Phrasebook** (spreadsheet)
  https://docs.google.com/spreadsheets/d/1Gsn5al4hlpNc_xKoXdU6XGmMyLiX4q-LFesFVsMlANo/
  Basis for cameronfreer's
  [lean-phrasebook.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/lean-phrasebook.md)
  and our [Math-to-Lean Phrasebook](math-to-lean.md).

## Papers

- **"Growing Mathlib"** (Baanen, Ballard, Commelin, Chen, Rothgang, Testa, 2026)
  https://arxiv.org/html/2508.21593v1

- **"Dedekind domains and class groups"** (Baanen, Dahmen, Narayanan, Nuccio, 2022)
  https://link.springer.com/article/10.1007/s10817-022-09644-0

- **"Formalization of Brownian motion in Lean"** (Degenne, Ledvinka, Marion, Pfaffelhuber)
  https://arxiv.org/pdf/2511.20118

## Community

- **Lean Zulip:** https://leanprover.zulipchat.com/ (`#mathlib` stream)
- **Lean community pages:** https://leanprover-community.github.io/
- **Blueprint tool:** https://github.com/leanprover-community/leanblueprint

## Version Note

Compiled April 2026. Mathlib evolves rapidly. When in doubt:
1. Check current docs: https://leanprover-community.github.io/mathlib4_docs/
2. Search Zulip for recent discussions
3. `lake update && lake exe cache get` for latest Mathlib
