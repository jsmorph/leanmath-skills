---
name: lean4-mathlib-research
description: >
  Entry point for a curated Lean 4 + Mathlib knowledge base. Use when deciding
  whether this repository is relevant to a task, and to route to the right
  deeper reference under skills/.
---

# Lean 4 + Mathlib Research Skill

## Scope

This file is the entry point for the repository.  It helps an LLM decide
whether the deeper material applies to the task and, if so, which file to load
next.  The repository fits Lean 4 and Mathlib work where the hard part is
library navigation, theorem search, tactic selection, naming, or formalization
design.

The material is strongest when the task depends on existing Mathlib practice:
which typeclass to use, which bundled structure to pick, which theorem names are
plausible, which imports to start from, or which tactics tend to close a goal
shape.  It also helps with research-level mathematical domains that already have
substantial Mathlib support, including probability, measure theory, algebra,
topology, linear algebra, combinatorics, and category theory.  Outside Lean 4
and Mathlib formalization, most of the repository adds little.

This repository is a synthesized knowledge layer.  It helps with recall,
routing, and search, but final answers still depend on the current Mathlib
codebase and the local project context.  Confirm names and statements with
source inspection, `#check`, API docs, and the tools collected in
[Tool Index](skills/tools.md).

When the task turns on compiler-guided repair, proof golfing, sorry management,
PR review, or CI routines, pair this material with upstream workflow packs.
[cameronfreer/lean4-skills](https://github.com/cameronfreer/lean4-skills)
covers the operational loop for agent-driven Lean work.  [leanprover/skills](https://github.com/leanprover/skills)
covers the official Lean-team workflows around Mathlib.

## Navigation

Start here, then load one or two deeper files.  In most cases,
[Root Reference](skills/ROOT.md) or [Tool Index](skills/tools.md) is the first
stop.  Domain files are narrower and matter once the mathematical area is
clear.

### Core References

| File | Use when | Contents |
|------|----------|----------|
| [Root Reference](skills/ROOT.md) | Need the main mathematical workflow for Lean 4 and Mathlib | Dispatch table, tactic order, search strategy, import patterns, and high-level guidance on definitions and APIs |
| [Tool Index](skills/tools.md) | Need to choose a search service, automation tactic, project tool, or external workflow resource | Consolidated list of tools and services mentioned across the repository |
| [Search and Discovery](skills/search-and-discovery.md) | Need to find an existing theorem, definition, namespace, or source file | Search order, name-guessing, local source inspection, public search services, and escalation to Zulip |
| [Tactics and Automation](skills/tactics-and-automation.md) | Need to choose tactics by goal shape or by mathematical domain | Practical tactic guidance, automation boundaries, and common tactic combinations |
| [Math-to-Lean Phrasebook](skills/math-to-lean.md) | Need to translate mathematical prose into Lean declarations or proof steps | Common mathematical phrases, Lean encodings, and proof-language patterns |
| [Naming and Style](skills/naming-and-style.md) | Need to name declarations, structure files, or prepare code for upstream style expectations | Naming conventions, capitalization rules, notation spellings, and style constraints |
| [Project Architecture](skills/project-architecture.md) | Need to plan a multi-file formalization or shape a reusable local API | File layout, definition engineering, blueprint use, and performance considerations |
| [Sources and References](skills/SOURCES.md) | Need provenance or direct upstream citations | Source list for the material synthesized in this repository |

### Domain References

These files are the main value of the repository once the subject area is
known.  Each one narrows the search space by collecting the standard types,
common imports, familiar lemma names, and domain-specific tactics for one part
of Mathlib.  Load the single closest file first, then widen only if the task
crosses domains.

| File | Use when | Contents |
|------|----------|----------|
| [Probability](skills/domains/probability.md) | The task involves probability spaces, random variables, independence, conditioning, martingales, or kernels | Standard probability types, import patterns, and common API shapes |
| [Measure Theory and Analysis](skills/domains/measure-theory-analysis.md) | The task involves measures, integration, a.e. reasoning, derivatives, filters, or analytic estimates | Measure-theoretic and analytic patterns, including automation and typeclass issues |
| [Combinatorics](skills/domains/combinatorics.md) | The task involves `Finset`, big operators, counting, graphs, or additive combinatorics | Finite combinatorial data structures, summation patterns, and counting lemmas |
| [Algebra and Number Theory](skills/domains/algebra-number-theory.md) | The task involves groups, rings, ideals, fields, localization, or Galois theory | Standard algebraic structures, bundled morphisms, and common theorem patterns |
| [Topology](skills/domains/topology.md) | The task involves topological spaces, filters, continuity, compactness, metric spaces, or manifolds | Topological APIs, continuity tooling, and filter-oriented reasoning |
| [Linear Algebra](skills/domains/linear-algebra.md) | The task involves modules, vector spaces, matrices, eigenvalues, tensor products, or inner-product spaces | Linear-algebraic structures, matrix APIs, and common tactics for finite-dimensional arguments |
| [Category Theory](skills/domains/category-theory.md) | The task involves categories, functors, limits, adjunctions, abelian categories, or sheaves | Category-theoretic tactics, rewriting tools, and common structural patterns |

### Support Files

These files do not carry mathematical guidance directly, but they help an agent
judge provenance, project intent, and pending gaps.  They are useful when the
task involves editing the repository itself or evaluating how much trust to put
in a particular synthesis.  They matter less when the job is only to solve a
Lean problem quickly.

| File | Use when | Contents |
|------|----------|----------|
| [Project README](README.md) | Need the short repository-level description and current framing | Project overview and positioning |
| [TODO](TODO.md) | Need to see which external sources have been identified but not yet integrated | Pending source list |
| [Development Notes](devnotes.md) | Need background on recent edits, rationale, or outstanding documentation work | Development journal with change notes and local decisions |
