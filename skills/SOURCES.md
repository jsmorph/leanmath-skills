# Sources and References

This skill was synthesized from the following primary sources. When using this skill,
these are authoritative references to consult for the most current information.

---

## Official Mathlib Documentation

### Naming Conventions (Primary source for naming-and-style.md)
- **Mathlib Naming Conventions**
  https://leanprover-community.github.io/contribute/naming.html
  The canonical reference for all Lean 4 / Mathlib naming rules: capitalization,
  theorem name patterns, symbol dictionary, variable conventions, Prop-valued classes.

### Style Guide (Primary source for code formatting rules)
- **Library Style Guidelines**
  https://leanprover-community.github.io/contribute/style.html
  Official code formatting rules: line length, indentation, tactic blocks, imports,
  file headers, documentation conventions.

### Linter Documentation
- **Mathlib.Tactic.Linter.Style**
  https://leanprover-community.github.io/mathlib4_docs/Mathlib/Tactic/Linter/Style.html
  Documentation for all style linters enforced by Mathlib CI.

### Tactic Reference
- **Lean 4 Tactic Reference**
  https://lean-lang.org/doc/reference/latest/Tactic-Proofs/Tactic-Reference/
  Official Lean 4 tactic documentation (core tactics, `grind`, `simp`, etc.).

- **Mathlib Tactic List**
  https://leanprover-community.github.io/mathlib-manual/html-multi/
  Comprehensive list of Mathlib-provided tactics with documentation.

### Simp Guide
- **Simp** (Kevin Buzzard et al.)
  https://leanprover-community.github.io/extras/simp.html
  Detailed guide to the `simp` tactic: normal forms, `@[simp]` lemma design, common
  pitfalls.

### Lean 4 Naming Conventions (upstream)
- **lean4/doc/std/naming.md**
  https://github.com/leanprover/lean4/blob/master/doc/std/naming.md
  Lean core naming conventions (left/right, cancel/inj, namespaces).

### Mathlib Overview
- **Mathematics in Mathlib**
  https://leanprover-community.github.io/mathlib-overview.html
  Comprehensive list of mathematical topics formalized in Mathlib, organized by domain.

### API Documentation
- **Mathlib4 Docs**
  https://leanprover-community.github.io/mathlib4_docs/
  Auto-generated API documentation for all Mathlib declarations.

### Search Tools
- **Loogle** (type-pattern search): https://loogle.lean-lang.org/
- **LeanSearch** (natural language): https://leansearch.net/
- **Moogle** (semantic search): https://www.moogle.ai/

---

## Textbooks and Tutorials

### Mathematics in Lean (Primary pedagogical source)
- **Mathematics in Lean** (Jeremy Avigad, Patrick Massot)
  https://leanprover-community.github.io/mathematics_in_lean/
  The main resource for learning mathematical formalization in Lean 4 with Mathlib.
  Covers basics through measure theory and analysis with interactive exercises.

### Theorem Proving in Lean 4
- **Theorem Proving in Lean 4**
  https://lean-lang.org/theorem_proving_in_lean4/
  Core Lean 4 tactics and dependent type theory, independent of Mathlib.

---

## Blog Posts and Guides

### Probability in Mathlib (Primary source for domains/probability.md)
- **"Basic probability in Mathlib"** (Rémy Degenne, 2024-10-17)
  https://leanprover-community.github.io/blog/posts/basic-probability-in-mathlib/
  Official guide to probability concepts in Mathlib: `IsProbabilityMeasure` vs
  `ProbabilityMeasure`, random variables, independence, conditioning, stochastic
  processes, kernels. Written by one of Mathlib's probability maintainers.

### Tao's Lean 4 Proof Tours (Informing proof strategy and workflow sections)
- **"A slightly longer Lean 4 proof tour"** (Terence Tao, 2023-12-05)
  https://terrytao.wordpress.com/2023/12/05/a-slightly-longer-lean-4-proof-tour/
  Detailed walkthrough of formalizing an inequality proof: Finset/BigOperators usage,
  `simp`, `gcongr`, `linarith`, naming convention search strategy, blueprint model.

- **"Formalizing the proof of PFR in Lean4 using Blueprint: a short tour"**
  (Terence Tao, 2023-11-18)
  https://terrytao.wordpress.com/2023/11/18/formalizing-the-proof-of-pfr-in-lean4-using-blueprint-a-short-tour/
  The PFR formalization project: tactic workflow, blueprint tool, collaborative
  formalization at scale.

---

## Research-Scale Formalization Guides

### Armstrong-Kempe Instructions (Primary source for project-architecture.md)
- **"Some math formalization guidelines based on Armstrong and Kempe"**
  (compiled by jsmorph / GPT 5.4 from Armstrong's blog post)
  https://gist.github.com/jsmorph/62ae62f136ef0b55692a5936740839a8
  Extracted instructions from the De Giorgi–Nash–Moser formalization. Covers: fixing
  the target, building infrastructure, engineering for Lean, using LLMs under
  mathematical control, cleanup and consolidation.

- **"Formalizing De Giorgi-Nash-Moser theory in Lean"** (Scott Armstrong, 2026-04)
  https://www.scottnarmstrong.com/2026/04/formalizing-de-giorgi-nash-moser-theory-in-lean/
  The original blog post describing the ~56,000-line sorry-free formalization of
  elliptic PDE regularity theory. Key lessons: avoid `EuclideanSpace`, formalize
  hidden work explicitly, treat iterations as exact quantitative objects, document
  elaboration fixes.

### cameronfreer/lean4-skills Mathlib Guide (Primary source for search-and-discovery.md)
- **mathlib-guide.md** (Cameron Freer et al.)
  https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/mathlib-guide.md
  Comprehensive guide to finding and using Mathlib lemmas: search strategies
  (keyword, type-based, Loogle, naming conventions, file organization), import
  patterns by domain, verification workflow, when Mathlib doesn't have it.

### Vilin97 Mathlib Conventions
- **conventions.md** (Vasily Ilin)
  https://github.com/Vilin97/mathlib-conventions/blob/main/conventions.md
  Community-contributed conventions document for Mathlib usage.

---

## Papers

### Growing Mathlib (Informing linting, maintenance, and style sections)
- **"Growing Mathlib: maintenance of a large scale mathematical library"**
  (Anne Baanen, Matthew Ballard, Johan Commelin, Bryan Chen, Michael Rothgang,
  Damiano Testa, 2026)
  https://arxiv.org/html/2508.21593v1
  Describes Mathlib's deprecation system, linters, import structure management,
  compilation speed optimization, and review processes.

### Dedekind Domains (Informing algebra-number-theory.md)
- **"A formalization of Dedekind domains and class groups of global fields"**
  (Anne Baanen, Sander Dahmen, Ashvni Narayanan, Filippo A. E. Nuccio, 2022)
  https://link.springer.com/article/10.1007/s10817-022-09644-0
  Design patterns for algebraic number theory in Mathlib: bundled subobjects,
  localization, fractional ideals, class groups.

### Brownian Motion Formalization (Informing probability and measure theory sections)
- **"Formalization of Brownian motion in Lean"**
  (Rémy Degenne, David Ledvinka, Etienne Marion, Peter Pfaffelhuber)
  https://arxiv.org/pdf/2511.20118
  Practical lessons from formalizing stochastic processes: working with natural number
  exponents instead of integer exponents, Mathlib support for sums over ℕ, localized
  theorems.

### Auslander-Buchsbaum-Serre (Informing algebra patterns)
- **"Formalization of Auslander–Buchsbaum–Serre criterion in Lean4"** (2025)
  https://arxiv.org/html/2510.24818v1
  Homological algebra in Mathlib: regular sequences, depth, localization, flat base
  change.

---

## Community Resources

- **Lean Zulip Chat**: https://leanprover.zulipchat.com/
  Primary discussion forum. The `#mathlib` stream is the canonical place to ask
  "Is there a lemma for X?"

- **Lean Community Pages**: https://leanprover-community.github.io/
  Hub for all community documentation, project listings, event calendar.

- **Lean Projects**: https://leanprover-community.github.io/lean_projects.html
  Index of formalization projects built on Mathlib.

---

## Version Note

This skill was compiled in April 2026. Mathlib evolves rapidly — definitions get
renamed, files get reorganized, new tactics appear. When in doubt:
1. Check the current Mathlib4 docs at https://leanprover-community.github.io/mathlib4_docs/
2. Search Lean Zulip for recent discussions
3. Run `lake update && lake exe cache get` to get the latest Mathlib
