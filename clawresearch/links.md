# leanmath candidate links

Format:
- [priority] title — url
  - Why it may matter
  - Category: paper | blog | forum | repo | tool | workshop
  - Added: 2026-04-11

## Seed links

- [high] Searching for Theorems in Mathlib — https://leanprover-community.github.io/blog/posts/searching-for-theorems-in-mathlib/
  - Directly relevant to discovery workflow. Likely useful for `search-and-discovery.md`, onboarding, and practical theorem-finding guidance.
  - Category: blog
  - Added: 2026-04-11

- [high] Formalizing Class Field Theory — https://leanprover-community.github.io/blog/posts/cmi-class-field-theory-workshop/
  - Good signal for active frontier work and how the community structures collaborative formalization projects, blueprints, APIs, and parallelizable theorem work.
  - Category: blog
  - Added: 2026-04-11

- [high] A formalization of the Gelfond-Schneider theorem — https://arxiv.org/abs/2603.24823
  - Recent substantial Lean 4 formalization in transcendental number theory. Likely useful as a case study for advanced-domain coverage and repo/source mining.
  - Category: paper
  - Added: 2026-04-11

- [high] Synthetic Differential Geometry in Lean — https://arxiv.org/abs/2603.17457
  - Recent paper showing constructive mathematics and nontrivial new proof engineering in Lean. Good candidate for domain coverage and style/architecture lessons.
  - Category: paper
  - Added: 2026-04-11

- [medium] Theorems about abelian categories — https://leanprover-community.github.io/blog/posts/abelian-categories/
  - Points to concrete mathlib additions and may surface patterns for domain-specific skill notes.
  - Category: blog
  - Added: 2026-04-11

- [medium] Lean community blog index — https://leanprover-community.github.io/blog/
  - Stable source to monitor for new mathlib and project reports.
  - Category: blog
  - Added: 2026-04-11

- [medium] Posts about New in mathlib — https://leanprover-community.github.io/blog/categories/cat_new-in-mathlib/
  - High-value recurring feed for concrete additions worth folding into the skill repo.
  - Category: blog
  - Added: 2026-04-11

- [medium] FormalProofBench: Can Models Write Graduate Level Math Proofs That Are Formally Verified? — https://arxiv.org/html/2603.26996
  - Relevant if leanmath-skills should track AI/formalization benchmarks, datasets, and repo pointers such as LeanDojo v2, Lean Workbook, and SorryDB.
  - Category: paper
  - Added: 2026-04-11

- [medium] Construction-Verification: A Benchmark for Applied Mathematics in Lean 4 — https://arxiv.org/abs/2602.01291
  - Useful if the project wants applied-math formalization patterns, benchmark tasks, and failure modes of proof-oriented models.
  - Category: paper
  - Added: 2026-04-11

- [medium] lean-lsp-mcp — https://github.com/oOo0oOo/lean-lsp-mcp
  - Tooling lead for agentic interaction with Lean. Could matter for `tools.md` or workflow guidance.
  - Category: repo
  - Added: 2026-04-11

- [high] Basic probability in Mathlib — https://leanprover-community.github.io/blog/posts/basic-probability-in-mathlib/
  - Strong practical commentary for exactly the kind of domain-specific skill material we want: how probability concepts are actually expressed in Mathlib, when to use `IsProbabilityMeasure` vs `ProbabilityMeasure`, and how to work with canonical probability spaces and notation.
  - Category: blog
  - Added: 2026-04-11

- [high] The Radon-Nikodym theorem in Lean — https://leanprover-community.github.io/blog/posts/the-radon-nikodym-theorem-in-lean/
  - High-value measure-theory case study with implementation details, file pointers, and design choices (for example using structures for Jordan decompositions). Good model for advanced-domain notes and proof-engineering guidance.
  - Category: blog
  - Added: 2026-04-11

- [high] Statistical Learning Theory in Lean 4: Empirical Processes from Scratch — https://arxiv.org/abs/2602.02285
  - Not pure probability in the classical sense, but a serious Lean 4 development built on concentration, expectations, and empirical process machinery. Useful as a modern case study in probability-heavy formalization and human-AI collaborative proof work.
  - Category: paper
  - Added: 2026-04-11

- [high] Markov kernels in Mathlib’s probability library — https://arxiv.org/abs/2510.04070
  - Looks especially relevant for probability-focused skill coverage: kernels, conditional distributions, conditional independence, sub-Gaussian variables, entropy, and KL divergence. More architectural than a single theorem formalization.
  - Category: paper
  - Added: 2026-04-11

- [high] Formalization of Brownian motion in Lean — https://arxiv.org/abs/2511.20118
  - Strong downstream probability lead. Brownian motion forces substantial measure-theoretic and stochastic-process infrastructure, which makes it a good signal for what probability-domain skill docs may need to explain.
  - Category: paper
  - Added: 2026-04-11

- [medium] This month in Mathlib (May 2024) — https://leanprover-community.github.io/blog/posts/month-in-mathlib/2024/month-in-mathlib-may-2024/
  - Good recurring source for domain-specific additions. This issue includes additive combinatorics and graph-theory signals such as dissociated sets and Hamiltonian paths/cycles, which can feed combinatorics-oriented skill notes.
  - Category: blog
  - Added: 2026-04-11

- [medium] This month in mathlib (Jul 2022) — https://leanprover-community.github.io/blog/posts/month-in-mathlib/2022/month-in-mathlib-jul-2022/
  - Older but still useful combinatorics lead list: Ruzsa covering lemma, Behrend construction, and Roth-number lower bounds. Useful more as a map of formalized topics than as direct workflow guidance.
  - Category: blog
  - Added: 2026-04-11

- [medium] This month in mathlib (Nov 2021) — https://leanprover-community.github.io/blog/posts/month-in-mathlib/2021/month-in-mathlib-nov-2021/
  - Another combinatorics lead source, including Hindman’s theorem and set-family machinery. Likely useful for identifying mathlib areas worth deeper repo/source inspection.
  - Category: blog
  - Added: 2026-04-11

- [high] Introducing Mathlib Changelog — https://leanprover-community.github.io/blog/posts/mathlib-changelog/
  - Very practical workflow artifact for skill-writing: helps track renamed/removed lemmas and understand version drift in fast-moving mathlib. Likely useful for maintenance-oriented guidance and “why old code broke” notes.
  - Category: blog
  - Added: 2026-04-11

- [medium] Backstage with Yaël Dillies — https://leanprover-community.github.io/blog/posts/backstage-with-dillies/
  - Not a theorem guide, but unusually good qualitative context on how substantial combinatorics formalization work got done, including branch-based collaboration around Sperner’s lemma and later Roth/Szemerédi-related work.
  - Category: blog
  - Added: 2026-04-11

- [medium] This month in mathlib (Oct and Nov 2022) — https://leanprover-community.github.io/blog/posts/month-in-mathlib/2022/month-in-mathlib-oct-and-nov-2022/
  - High-density measure-theory lead source: Vitali families, Lebesgue density theorem, Lebesgue differentiation theorem, plus adjacent analysis material. Useful as a map of mature measure-theory coverage in mathlib.
  - Category: blog
  - Added: 2026-04-11

- [medium] This month in mathlib (Aug 2022) — https://leanprover-community.github.io/blog/posts/month-in-mathlib/2022/month-in-mathlib-aug-2022/
  - Useful probability lead source: portmanteau implications, Doob upcrossing estimate, a.e. martingale convergence, and L¹ martingale convergence. Good signal that the probability library has deeper practical reach than just introductory notation.
  - Category: blog
  - Added: 2026-04-11

- [medium] 2021 — The Bottom Line — https://leanprover-community.github.io/blog/posts/2021-the-bottom-line/
  - Broad retrospective rather than a domain guide, but helpful for situating when measure theory/analysis became strong enough to support probability work in mathlib. Useful background context, not a primary instructional source.
  - Category: blog
  - Added: 2026-04-11

## Monitor searches

- site:leanprover-community.github.io/blog Lean mathlib formalization
- site:arxiv.org Lean 4 formalization mathematics
- site:github.com Lean mathlib theorem proving tool Lean 4
- site:leanprover.zulipchat.com Lean formalization mathlib
