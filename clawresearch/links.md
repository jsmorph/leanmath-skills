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

## 2026-04-12 additions

- [high] The Sphere Packing Project | Post 1 - The Story — https://leanprover-community.github.io/blog/posts/SpherePacking-1/
  - Strong large-scale formalization case study with unusually concrete project-architecture details: blueprinting, repository strategy, synchronous “packathons”, public Zulip coordination, and explicit AI/autoformalization interaction. Also directly references `lean4-skills`, which makes it unusually relevant to skill authoring.
  - Category: blog
  - Added: 2026-04-12

- [high] Tradeoffs of defining types as subobjects — https://leanprover-community.github.io/blog/posts/tradeoff-of-defining-types-as-subobjects/
  - High-value API/design note for mathlib-facing authoring. Gives a crisp comparison of subobject vs coerced-subobject vs custom-structure designs, with practical consequences for dot notation, projections, instance transfer, and refactors like `ProbabilityTheory.Kernel`.
  - Category: blog
  - Added: 2026-04-12

- [medium] Simons Foundation Lean Workshop — https://leanprover-community.github.io/blog/posts/simons-lean-workshop/
  - Good high-signal workshop report with concrete lecture links and project notes across analysis, topology, algebra, tactic writing, blueprints, and substantial collaborative formalization efforts. Useful as a source of downstream leads rather than a single skill note.
  - Category: workshop
  - Added: 2026-04-12

- [medium] Fantastic Simprocs and How to Write Them — https://leanprover-community.github.io/blog/posts/simprocs-tutorial/
  - Not domain math, but very practical for proof automation and maintenance-oriented skill writing. Includes worked examples, `simproc` / `dsimproc` patterns, and tradeoffs against ordinary simp lemmas.
  - Category: blog
  - Added: 2026-04-12

## 2026-04-13 additions

- [high] Lean Formalization of Generalization Error Bound by Rademacher Complexity — https://arxiv.org/html/2503.19605v3
  - Strong probability-and-analysis case study built explicitly on Mathlib 4 probability. The abstract and intro point to formalized symmetrization, topological assumptions on hypothesis classes, and a concrete repo (`auto-res/lean-rademacher`), which makes it a good lead for probability skill coverage and mature measure-theoretic proof patterns.
  - Category: paper
  - Added: 2026-04-13

- [medium] The correspondence between affine group schemes and Hopf algebras — https://leanprover-community.github.io/blog/posts/affine-group-schemes-hopf-algebra/
  - Strong algebraic-geometry project report tied to the Toric project. More mathematical than implementation-focused, but still useful as a mature formalization case study and a pointer to concrete declarations, repo docs, and contributor-oriented project structure.
  - Category: blog
  - Added: 2026-04-13

- [medium] Simprocs for the Working Mathematician — https://leanprover-community.github.io/blog/posts/simprocs-for-the-working-mathematician/
  - Companion to the existing simproc tutorial entry, but worth tracking separately because it explains when simprocs beat ordinary simp lemmas, with concrete examples like `existsAndEq`, `Nat.reduceDvd`, `Finset.Icc_ofNat_ofNat`, and `↓reduceIte`. Good material for workflow and automation notes used by math-facing skill docs.
  - Category: blog
  - Added: 2026-04-13

- [medium] Simp, made simple. — https://leanprover-community.github.io/blog/posts/simp-made-simple/
  - Deeper internals writeup on `simp` itself: preprocedures vs postprocedures, `Step`, `Result`, and `SimpM`. Not domain-specific mathematics, but strong maintenance and proof-engineering context for anyone writing robust Lean automation around mathlib workflows.
  - Category: blog
  - Added: 2026-04-13

## 2026-04-14 additions

- [high] Formalizing the Classical Isoperimetric Inequality in the Two-Dimensional Case — https://arxiv.org/abs/2603.14663
  - Strong analysis case study with unusually concrete formalization challenges: Fourier-series foundations, Parseval, term-by-term differentiation, interchange of infinite sums and integrals, and indexing friction inside Mathlib. Good candidate for analysis-oriented skill notes and a mature worked example.
  - Category: paper
  - Added: 2026-04-14

- [medium] Pursuit of Truth and Beauty in Lean 4: Formally Verified Theory of Grammars, Optimization, Matroids — https://arxiv.org/abs/2602.12891
  - Broad thesis rather than a single-domain paper, but it looks useful for matroid and optimization coverage because it explicitly documents code artifacts and emphasizes readable, believable definitions. Worth keeping as a source of reusable design commentary and downstream repo leads.
  - Category: paper
  - Added: 2026-04-14

- [medium] RepoProver: Research code base for Automatic Textbook Formalization — https://github.com/facebookresearch/repoprover
  - Not domain math by itself, but unusually concrete workflow infrastructure for large Lean textbook formalization, with a real algebraic-combinatorics case study, chapter manifests, issue files, merge-queue discipline, and role separation across sketch/prove/review agents. Likely useful for workflow notes adjacent to domain-specific skill authoring.
  - Category: repo
  - Added: 2026-04-14

## 2026-04-15 additions

- [high] teorth/analysis: A Lean companion to Analysis I — https://github.com/teorth/analysis
  - Unusually practical analysis-facing repository because it explicitly documents where textbook-style mathematics must bend to current Lean/Mathlib conventions: 0-based sequence indexing, total-function design instead of partial functions, gradual migration from custom textbook definitions to Mathlib definitions, and generated docs for cross-navigation. Very likely useful for skill notes on analysis workflow, notation friction, and “why the Lean version looks different from the book”.
  - Category: repo
  - Added: 2026-04-15

- [high] A formal proof of the Ramanujan--Nagell theorem in Lean 4 — https://arxiv.org/abs/2604.09808
  - Fresh April 2026 formalization with exactly the kind of commentary we want from a mature case study: proof architecture, dependency graph / blueprint, gap analysis between textbook and formal proof, and reusable algebraic-number-theory infrastructure for quadratic integer rings. Not in the top target domains, but strong enough to keep.
  - Category: paper
  - Added: 2026-04-15

## 2026-04-16 additions

- [high] YaelDillies/cam-combi — https://github.com/YaelDillies/cam-combi
  - Exceptionally strong combinatorics lead: a living Lean 4 repo organized around Cambridge graph theory, extremal/probabilistic combinatorics, Ramsey theory, additive combinatorics, and growth-in-groups courses, with explicit upstreaming structure, theory-development folders, archived alternative proofs, and concrete active targets like Erdős–Rényi random graphs and the van den Berg–Kesten–Reimer inequality. Exactly the sort of domain map and proof-pattern reservoir that can feed combinatorics-focused skill notes.
  - Category: repo
  - Added: 2026-04-16

- [medium] A formalization of Borel determinacy in Lean — https://arxiv.org/abs/2502.03432
  - Not one of the top target domains, but still a substantial mature formalization in descriptive set theory / logic with publication in Annals of Formalized Mathematics. Worth keeping as a signal for topology-adjacent infinite-game and Borel-set infrastructure, and as a case study in following a classical proof closely inside Lean 4.
  - Category: paper
  - Added: 2026-04-16

## 2026-04-17 additions

- [high] UW Math AI Lab — https://github.com/uw-math-ai
  - Strong discovery hub rather than a single artifact, but a very good one: the org page exposes active Lean formalization projects in target domains, including random graphs, central limit theorem work, geometric measure theory, and point-set topology, plus concrete mathlib PR links and theorem-search tooling. Worth monitoring because it is unusually dense with domain-specific downstream leads.
  - Category: repo
  - Added: 2026-04-17

- [high] uw-math-ai/FormalizingGMT — https://github.com/uw-math-ai/FormalizingGMT
  - Especially strong analysis / measure-theory lead. The repo is explicit about upstreaming mathlib-ready GMT foundations, formalizing Falconer/Evans material, current proof status, and linked mathlib PRs (`diameter` of Euclidean balls, accumulation-point / no-atoms lemmas). Good candidate for later skill notes on geometric-measure-theory conventions, measure-theoretic infrastructure, and how a project decomposes formalization into upstreamable pieces.
  - Category: repo
  - Added: 2026-04-17

- [medium] uw-math-ai/central_limit_theorem — https://github.com/uw-math-ai/central_limit_theorem
  - Early-looking repo, but still a worthwhile probability lead because it is plainly scoped to a Lean 4 CLT formalization and includes a `howto.md` alongside the project skeleton. Worth checking later for proof architecture and probability-library usage once the repo fills out.
  - Category: repo
  - Added: 2026-04-17

- [high] uw-math-ai/math-ai-docs — https://github.com/uw-math-ai/math-ai-docs
  - Practical workflow commentary with unusually concrete advice for Lean formalization projects: use LeanSearch / LeanExplore / Mathlib Index first, ask on Zulip, prototype in Lean4Web, keep a single shared repo, upstream to mathlib in pieces, and structure weekly planning explicitly. Not domain math per se, but very relevant to skill authoring around theorem discovery, project hygiene, and mathlib contribution workflow.
  - Category: repo
  - Added: 2026-04-17

## 2026-04-18 additions

- [high] A Prime-Generated Formalization of Nagata’s Factoriality Theorem in Lean 4 — https://arxiv.org/abs/2604.05238
  - Strong algebra lead with better-than-usual proof-engineering value: the paper is explicit about reusable localization / `IsLocalization` transfer lemmas, packaging the theorem at both concrete and abstract levels, and how the formalization forced a correction from a too-weak “prime-or-unit” hypothesis to the right prime-generated statement. Good candidate for algebra-oriented skill notes on localization APIs, theorem packaging, and how formalization sharpens hypotheses.
  - Category: paper
  - Added: 2026-04-18

- [medium] Bridging Lean and the LMFDB — https://multramate.github.io/lean-lmfdb/
  - Upcoming 2026 workshop, but worth tracking because it is unusually explicit about tutorial topics that should surface practical Lean number-theory navigation material: number fields, elliptic curves, modular forms, and collaborative formalization of LMFDB definitions. More a source of downstream notes/talks than a standalone skill doc, but a good watchlist item for algebra / number-theory API guidance.
  - Category: workshop
  - Added: 2026-04-18

- [medium] Techniques and Tools for the Formalization of Analysis — https://icerm.brown.edu/program/topical_workshop/tw-26-ttfa
  - The public page is thin right now, but the event itself is exactly on target: a 2026 analysis-focused Lean workshop that may later produce slides, talk pages, or project notes worth mining for proof patterns and domain conventions in analysis. Best treated as an event-source lead rather than as immediate instructional content.
  - Category: workshop
  - Added: 2026-04-18

## 2026-04-19 additions

- [medium] uw-math-ai/central_limit_theorem — https://github.com/uw-math-ai/central_limit_theorem
  - Still an early repo, but it has crossed from vague org-level mention into a concrete project artifact with a dedicated Lean 4 repository, a `howto.md`, and a minimal theorem/file layout. Worth tracking because CLT is a major missing probability milestone, and even a sparse project repo can later become a strong source for probability-library conventions, dependency choices, and proof decomposition once the formalization matures.
  - Category: repo
  - Added: 2026-04-19

- [medium] Lean Together 2026 — https://leanprover-community.github.io/lt2026/
  - Not domain-specific by itself, but now worth watching because the 2026 event page points to recorded talks, and Lean Together often surfaces fresh mathlib workflow, project, and infrastructure material before it is rewritten as blog posts. Best treated as a discovery hub for later targeted follow-up rather than immediate guidance.
  - Category: workshop
  - Added: 2026-04-19

## 2026-04-20 additions

- [high] MAT740-Topology-in-Lean-HS25 — https://github.com/MariusFurter/MAT740-Topology-in-Lean-HS25
  - Strong topology-facing teaching repo with a very practical angle: it rebuilds core point-set topology in Lean 4 while explicitly forbidding `Mathlib.Topology`, which makes it a good source for “what the definitions really look like”, proof patterns around open sets / continuity, and topology-specific onboarding material that is closer to skill authoring than a polished paper would be.
  - Category: repo
  - Added: 2026-04-20

- [medium] Announcing the ∞-Cosmos Project — https://leanprover-community.github.io/blog/posts/infinity-cosmos-announcement/
  - Not in the top target domains, but still a solid adjacent lead: it explains a concrete strategy for building higher-category theory on top of existing mathlib coverage, highlights the choice of an axiomatic interface over direct quasi-category encodings, and points to a blueprint plus project overview. Worth keeping as an example of large-project architecture and “formalize through the right abstraction layer” design.
  - Category: blog
  - Added: 2026-04-20

## 2026-04-21 additions

- [high] b-mehta/epfl-comb — https://github.com/b-mehta/epfl-comb
  - Strong combinatorics teaching repo with unusually reusable skill-authoring value: chapter-organized Lean files, exercises, and onboarding material adapted from Mathematics in Lean and the Lean for the Curious Mathematician workshop. More pedagogical than `cam-combi`, which is exactly why it looks useful for combinatorics-oriented notes on proof patterns, exercise design, and newcomer-facing mathlib navigation.
  - Category: repo
  - Added: 2026-04-21

- [medium] drisspg/lean_ua — https://github.com/drisspg/lean_ua
  - Analysis-facing Lean 4 repo formalizing large parts of Abbott’s *Understanding Analysis*, including sequences and series, basic topology of `ℝ`, continuity, derivatives, and the Riemann integral. Likely useful as a second teaching-style analysis source alongside `teorth/analysis`, especially for comparing textbook organization against current Lean/mathlib idioms.
  - Category: repo
  - Added: 2026-04-21

## 2026-04-22 additions

- [high] Formalization of De Giorgi--Nash--Moser Theory in Lean — https://arxiv.org/abs/2604.05984
  - Very strong analysis/PDE formalization lead: formalizes local boundedness, weak and Moser Harnack inequalities, and interior Hölder regularity for elliptic equations, while explicitly adding substantial Sobolev / weak-solution infrastructure in Lean. This is exactly the kind of mature case study that can inform skill notes on analysis proof architecture, dependency layering, and mathlib navigation for hard analysis.
  - Category: paper
  - Added: 2026-04-22

## 2026-04-23 additions

- [high] mrdouglasny/OSforGFF — https://github.com/mrdouglasny/OSforGFF
  - Exceptionally strong analysis/probability-adjacent repo: a 32k-line Lean 4 formalization of the Gaussian free field with zero axioms/sorries, explicit architecture docs, layered dependency structure, and reusable infrastructure for Fourier analysis, Schwartz-space integration, positive-definite kernels, and measure-theoretic probability on distributions. Strong candidate for deeper mining because it exposes both domain APIs and project-architecture decisions.
  - Category: repo
  - Added: 2026-04-23

- [medium] Introduction to Real Analysis — https://alexkontorovich.github.io/2025F311H/
  - Practical analysis-teaching artifact with public lecture notes tied to a Lean game-based course. The topic list is unusually broad for an openly browsable course page: limits, Cauchy sequences, completion of metric spaces, series, continuity, derivatives, compactness, Riemann sums, and limit/integral interchange, along with concrete tactic topics. Useful as a source of textbook-to-Lean examples and possible downstream repo/note leads.
  - Category: blog
  - Added: 2026-04-23

- [medium] Undergraduate mathematics in mathlib — https://leanprover-community.github.io/undergrad.html
  - Not a narrative writeup, but a high-value navigation artifact maintained by the community. It maps undergraduate topics directly to current mathlib declarations and fills a different niche from theorem search posts: domain-to-library coverage lookup. Likely useful for skill authoring around discovery, “is this already in mathlib?”, and topic-specific onboarding.
  - Category: tool
  - Added: 2026-04-23

## 2026-04-24 additions

- [high] scottnarmstrong/DeGiorgi — https://github.com/scottnarmstrong/DeGiorgi
  - Strong companion artifact to the De Giorgi--Nash--Moser paper: the repo is explicit about theorem entry points, namespace layout, root imports, and a machine-generated `DeGiorgi_Lean_to_Tex.tex` reading companion. Especially useful for skill authoring because it exposes how a large PDE formalization is packaged for navigation and reuse, not just what the paper claims abstractly.
  - Category: repo
  - Added: 2026-04-24

- [medium] 2-Coloring Cycles in One Round — https://arxiv.org/abs/2603.04235
  - Good combinatorics/discrete-math case study even though it comes from distributed computing: the paper states the underlying probabilistic/measurability model cleanly and ties it to a Lean 4 formalization of both bounds. Worth tracking for proof-pattern value around finite combinatorial objects, probability on local random algorithms, and decomposition through De Bruijn-graph arguments.
  - Category: paper
  - Added: 2026-04-24

- [medium] suomela/2-coloring-1-round — https://github.com/suomela/2-coloring-1-round
  - Useful repo-level complement to the paper above: it highlights a small pair of entry files (`Definitions.lean`, `MainResults.lean`), documents an axiom-audit path, and makes the large 17k-line development more navigable. That packaging detail makes it more relevant to skill authoring than a bare theorem statement would be.
  - Category: repo
  - Added: 2026-04-24
