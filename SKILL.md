---
name: lean4-mathlib-research
description: >
  Instructions for research-level mathematics formalization in Lean 4 with Mathlib.
  Use this skill whenever the user is working on serious mathematical formalization:
  writing Lean 4 proofs, defining mathematical structures, searching Mathlib for lemmas,
  building proof infrastructure, planning formalization architecture, or translating
  paper proofs into Lean. Also trigger when the user mentions Lean 4, Mathlib, tactic
  proofs, theorem proving, formalization, or asks for help with any .lean file that
  imports Mathlib. This includes: proof debugging, tactic selection, naming conventions,
  elaboration troubleshooting, Mathlib search strategies, blueprint design, definition
  engineering, and large-scale formalization project planning. Even if the user just
  pastes a Lean error message or asks "how do I prove X in Lean", use this skill.
---

# Research Mathematics Formalization in Lean 4 with Mathlib

## Introduction

This skill provides comprehensive guidance for formalizing research-level mathematics
in Lean 4 on top of Mathlib, the largest unified library of formalized mathematics
(2+ million lines, 100,000+ theorems as of 2026). It is designed for mathematicians,
formalization engineers, and AI systems working at the frontier — where the proofs are
long, the infrastructure is heavy, and the interfaces between mathematical domains are
nontrivial.

The guidance here is drawn from primary sources in the Lean formalization community:
the official Mathlib documentation for naming, style, and tactics; Rémy Degenne's
probability guide; Scott Armstrong and Julia Kempe's lessons from formalizing De Giorgi–
Nash–Moser theory (~56,000 lines in ~2 weeks); Terence Tao's Lean 4 proof tours and
the PFR project; Cameron Freer's lean4-skills Mathlib guide; and several research
papers on Mathlib maintenance and domain-specific formalization. Full citations are in
`references/SOURCES.md`.

The skill is organized in three tiers:

1. **This file (SKILL.md):** Always loaded. Contains the core workflow, tactic quick
   reference, common imports, and dispatch rules for consulting deeper references.
2. **Cross-cutting references** (`references/*.md`): Loaded on demand for search
   strategies, naming conventions, tactic details, or project architecture.
3. **Domain sub-skills** (`references/domains/*.md`): Loaded on demand when working
   in a specific mathematical field.

---

## Skill Map

### Cross-Cutting References

Read these as needed — do NOT load all of them for every query.

**`references/search-and-discovery.md`** (~365 lines)
When: User needs to find a Mathlib lemma, definition, or file.
Contents: The "search before you prove" philosophy. Five complementary search
strategies: in-proof tactics (`exact?`, `apply?`, `rw?`, `simp?`), command-line
grep/find on the Mathlib source tree, Mathlib naming convention patterns for guessing
lemma names, the Mathlib file hierarchy organized by mathematical domain, Loogle
type-pattern search, and LeanSearch natural language search. Verification workflow
with `#check` / `#print`. What to do when Mathlib doesn't have it.
Sources: cameronfreer/lean4-skills `mathlib-guide.md`; Mathlib naming conventions.

**`references/naming-and-style.md`** (~370 lines)
When: User is naming definitions/lemmas, formatting code, or preparing a Mathlib PR.
Contents: Capitalization rules (snake_case for proofs, UpperCamelCase for types,
lowerCamelCase for terms). Theorem naming patterns: `conclusion_of_hypothesis`,
axiomatic names, dot notation, left/right conventions, abbreviations. Complete
symbol-to-name dictionary (logic, sets, algebra, lattices). Variable conventions.
`Is*` prefix rules for Prop-valued classes. Structural lemma patterns (ext, inj, rec).
Code formatting: 100-char lines, 2-space indent, `<|` not `$`, `fun` not `λ`.
File organization: headers, imports, sections. Documentation conventions. Linting rules
and `@[simp]` normal forms.
Sources: Mathlib naming conventions; Lean 4 naming conventions; Library style guidelines.

**`references/tactics-and-automation.md`** (~440 lines)
When: User needs tactic advice, proof strategy, or is stuck on a goal.
Contents: Development vs. production proof philosophy. Complete tactic reference:
introduction/elimination, rewriting (`rw` vs `simp_rw` vs `conv`), case analysis,
induction, calc blocks. Decision procedures: `ring`, `omega`, `linarith`, `nlinarith`,
`field_simp`, `norm_num`, `positivity`, `decide`, `norm_cast`. Domain-specific
automation: `fun_prop`, `gcongr`, `measurability`, `continuity`, `aesop`, `grind`.
Search tactics (`exact?`, `apply?`, `rw?`, `hint`). Proof strategy patterns:
forward vs backward reasoning, have/suffices decomposition, epsilon-delta with
filters, measure theory patterns with `filter_upwards`. Performance: profiling,
`simp only`, typeclass instance provision, `set_option maxHeartbeats`. Common pitfalls:
missing tactic imports, typeclass resolution failures, `rw` under binders, definitional
equality surprises, universe issues, coercion chains.
Sources: Lean 4 tactic reference; Mathlib tactic list; Buzzard's simp guide; Tao's
proof tours; Mathematics in Lean.

**`references/project-architecture.md`** (~500 lines)
When: User is planning a formalization, designing definitions, or managing a multi-file
project.
Contents: Project planning: fixing the target, mapping the dependency chain, identifying
what Mathlib provides, choosing the right level of generality. Definition engineering:
prefer Mathlib definitions, design for the elaborator, typeclasses vs bundled morphisms
vs Prop-valued classes, provide API lemmas immediately, mark reducibility deliberately,
avoid `EuclideanSpace`. Infrastructure and interface lemmas: the hidden layer between
definitions and headline theorems, formalizing truncations/cutoffs/reductions
explicitly, treating quantitative iterations as exact mathematics. File organization:
one topic per file, ~1000-line target, import graph discipline, recommended project
structure with `lakefile.lean` setup. The Blueprint model for large projects.
Mathlib's type hierarchies (algebraic, topological, analytic). Elaboration engineering:
documenting fixes, common issues, `autoImplicit false`. Using LLMs effectively: what
they're good at, what humans must control, the Armstrong-Kempe workflow model.
Cleanup and consolidation: checklist, diagnosing structural problems.
Sources: Armstrong & Kempe (De Giorgi–Nash–Moser); Tao (PFR Blueprint); Baanen et al.
("Growing Mathlib").

### Domain Sub-Skills

Each covers: setup boilerplate, core types, key tactics, important lemma names, common
proof patterns, domain-specific gotchas, and curated import blocks.

**`references/domains/probability.md`** (~190 lines)
Scope: Probability spaces, random variables, independence, conditioning, martingales.
Key topics: `IsProbabilityMeasure` vs `ProbabilityMeasure` (and when to use which),
the `ℙ` / `𝔼` / `P[X]` notation system, `ℝ≥0∞` arithmetic gotchas, random variables
as measurable functions, law/distribution via `Measure.map`, the full independence
hierarchy (`IndepFun` / `iIndepFun` / `IndepSet` / `Indep` and conditional variants),
conditional probability (`P[s|t]`, `P[|t]`, `P[|X ← x]`), conditional expectation
(`condexp`), discrete probability (`DiscreteMeasurableSpace`, `PMF`), known
distributions (Gaussian, Poisson, etc.), stochastic processes and filtrations,
martingales and stopping times, transition kernels (`Kernel`, `IsMarkovKernel`).
Sources: Rémy Degenne, "Basic probability in Mathlib" (2024); Brownian motion paper.

**`references/domains/measure-theory-analysis.md`** (~265 lines)
Scope: Measures, integration, Lp spaces, derivatives, norms, a.e. reasoning.
Key topics: Measure classes (`IsFiniteMeasure`, `SigmaFinite`, etc.), measure
construction (Dirac, counting, Lebesgue, restrict, map), two integral types (Lebesgue
`∫⁻` vs Bochner `∫`), integrability, key theorems (monotone convergence, dominated
convergence, Fubini-Tonelli), the `ae` filter and `filter_upwards` tactic, Lp spaces
(`Memℒp`, `snorm`), Fréchet and scalar derivatives, `fun_prop` for function properties,
filters as the foundation for limits, norms and distances, and the "avoid
`EuclideanSpace`" lesson from Armstrong-Kempe.
Sources: Mathlib API docs; Mathematics in Lean; Armstrong-Kempe.

**`references/domains/combinatorics.md`** (~245 lines)
Scope: Finset, big operators (∑/∏), counting, graphs, set families.
Key topics: `Finset` construction and operations, `Fintype` for finite types,
`open BigOperators` for ∑/∏ notation, essential sum/product lemmas (splitting,
comparing, telescoping, reindexing via `sum_bij`), cardinality lemmas, binomial
coefficients, `SimpleGraph` for graph theory, set family results (Sperner, Kruskal-
Katona), additive combinatorics from the PFR project, proof patterns (double counting,
pigeonhole, Finset induction), `Decidable` instance requirements, and the `ℕ`
subtraction truncation gotcha.
Sources: Mathlib API docs; Tao's proof tour (Finset walkthrough); Mathlib overview.

**`references/domains/algebra-number-theory.md`** (~190 lines)
Scope: Groups, rings, fields, ideals, localization, Galois theory, Dedekind domains.
Key topics: The algebraic typeclass hierarchy (`Semigroup` → `Field`), bundled
morphisms (`→*`, `→+*`, `→ₐ`), bundled subobjects (`Subgroup`, `Ideal`,
`IntermediateField`), `algebraMap` for algebra towers, localization (`IsLocalization`),
quotient rings, polynomials (`R[X]`, `MvPolynomial`), field extensions and Galois
theory, Dedekind domains and class groups, valuations and local fields, arithmetic
functions and `ZMod`, the `ring`/`group`/`abel`/`field_simp` tactics.
Sources: Mathlib API docs; Baanen et al. (Dedekind domains paper);
Auslander-Buchsbaum-Serre formalization; Mathematics in Lean.

**`references/domains/topology.md`** (~240 lines)
Scope: Topological spaces, filters, continuity, compactness, metric spaces, manifolds.
Key topics: Filter-based foundations (`𝓝`, `atTop`, `Filter.Tendsto`), the four levels
of continuity (`Continuous`, `ContinuousAt`, `ContinuousOn`, `ContinuousWithinAt`),
`fun_prop` as first-choice tactic, open/closed/compact sets and their key lemmas,
metric spaces (balls, Lipschitz/Hölder maps), connectedness, topological algebra
(`TopologicalGroup`, `TopologicalRing`), completions, product/subspace/quotient
topologies, manifolds (`SmoothManifoldWithCorners`), common patterns for compactness
arguments and neighborhood reasoning.
Sources: Mathlib API docs; Mathlib topology overview; Mathematics in Lean.

**`references/domains/linear-algebra.md`** (~220 lines)
Scope: Modules, vector spaces, matrices, bases, eigenvalues, tensor products, norms.
Key topics: `Module` typeclass, linear maps (`→ₗ[R]`) and continuous linear maps
(`→L[R]`), submodules, bases and dimension (`Module.finrank`, `Module.rank`), matrix
type and operations (determinant, inverse, `toLin` correspondence), eigenvalues and
Cayley-Hamilton, bilinear forms and inner product spaces, tensor products, multilinear
and exterior algebra, normed/Banach/Hilbert spaces, `ext` for equality of linear maps,
rank-nullity and dimension arguments.
Sources: Mathlib API docs; Mathlib overview; Mathematics in Lean.

**`references/domains/category-theory.md`** (~220 lines)
Scope: Categories, functors, natural transformations, limits, adjunctions, abelian
categories, sheaves.
Key topics: Diagrammatic-order composition convention (`f ≫ g` means f-then-g),
functors (`⥤`) and natural transformations, `aesop_cat` as primary automation tactic,
limits and colimits (products, equalizers, pullbacks and their duals), preservation
and reflection of limits, adjunctions and the Yoneda embedding, abelian categories
(kernels, cokernels, exact sequences, homological complexes), concrete categories
(`GroupCat`, `RingCat`, etc.), monoidal categories, Grothendieck topologies and
sheaves, the `reassoc` trick and `slice_lhs`/`slice_rhs` for diagram chasing.
Sources: Mathlib API docs; Mathlib category theory overview; Lean community blog.

### Citations

**`references/SOURCES.md`** (~190 lines)
Full bibliography with URLs: official Mathlib documentation, textbooks (Mathematics in
Lean, Theorem Proving in Lean 4), blog posts (Degenne, Tao, Armstrong), community
guides (cameronfreer, Vilin97), research papers (Growing Mathlib, Dedekind domains,
Brownian motion, Auslander-Buchsbaum-Serre), community resources (Zulip, Loogle,
LeanSearch, Moogle).

---

## Core Workflow

Every formalization task follows the same fundamental loop:

### 1. Understand the Mathematics First

Before writing any Lean, state the mathematical content precisely. Identify the exact
hypotheses and conclusion, the mathematical domain, and the right level of generality.
Lean and Mathlib reward generality — a result about `CommMonoid` is more reusable than
one about `ℤ` — but over-generalization can cause elaboration problems.

### 2. Search Mathlib Before Proving

Mathlib has 100,000+ theorems. **Always search before proving.** See
`references/search-and-discovery.md`. Quick version:
```
1. Guess the name from naming conventions
2. Use exact?, apply?, rw? in a test example
3. Use grep / find on .lake/packages/mathlib
4. Check the Mathlib file hierarchy by domain
5. Use Loogle (type-pattern) or LeanSearch (natural language)
```

### 3. Engineer Definitions for the Prover

- Prefer Mathlib's existing definitions over your own.
- Use typeclasses for structure, bundled morphisms for maps, `Prop`-valued classes for
  properties. Follow `Is*` naming for noun-based property classes.
- Avoid `EuclideanSpace` for analysis — use `ι → ℝ` directly.
- Provide API lemmas (`@[simp]`, `@[ext]`, coercions) alongside every definition.
- Mark `@[reducible]` / `@[irreducible]` deliberately.

### 4. Write Proofs in the Structure the Prover Needs

- Name intermediate results as separate lemmas, not sprawling `have` chains.
- Build interface lemmas for domain crossings (pointwise ↔ a.e., local ↔ global).
- Formalize "routine" hidden work (truncations, cutoffs, reductions) explicitly.
- Treat quantitative bookkeeping (iterations, exponent cascades) as named mathematics.

### 5. Manage Elaboration and Compilation

- Split files at ~1000 lines. Keep imports narrow.
- Use `simp only [...]` not bare `simp`. Use `simp?` to discover lemmas.
- Profile slow proofs with `set_option profiler true`.
- Scope `set_option maxHeartbeats` to single declarations.

### 6. Iterate with Compiler Feedback

```
1. State theorem with sorry → check statement elaborates
2. Write tactic proof, reading goal state after each step
3. If stuck: exact?/apply?/rw? → decompose → search Mathlib → reformulate
4. Clean up: simp only, remove unused imports, fix names, add docstrings
```

### 7. Plan for Library Quality

Follow Mathlib conventions even for private projects: naming, `@[simp]`/`@[ext]`/
`@[fun_prop]` tagging, docstrings, `#lint` clean.

---

## Tactic Quick Reference

See `references/tactics-and-automation.md` for full detail.

| Situation | First-choice tactic(s) |
|-----------|----------------------|
| Ring/field equation | `ring`, `field_simp` then `ring` |
| Linear arithmetic (ℕ, ℤ, ℚ, ℝ) | `linarith`, `omega` (ℕ/ℤ) |
| Simplification | `simp only [...]`, `simp_rw [...]` |
| Find the exact lemma | `exact?`, `apply?` |
| Rewrite search | `rw?` |
| Continuity / measurability | `fun_prop`, `measurability` |
| Positivity / nonnegativity | `positivity` |
| Case split | `rcases`, `obtain`, `by_cases` |
| Inequality chaining | `calc`, `gcongr` |
| Extensionality | `ext` |
| Coercions | `norm_cast`, `push_cast` |
| Finishing moves | `exact`, `assumption`, `omega`, `linarith`, `tauto` |
| Nonlinear arithmetic | `nlinarith`, `polyrith` |
| Decision procedures | `decide`, `norm_num` |
| General automation | `aesop`, `grind` |
| Category theory | `aesop_cat`, `simp`, `slice_lhs`/`slice_rhs` |
| Groups / abelian groups | `group`, `abel` |

---

## Common Import Groups

```lean
-- Analysis / Calculus
import Mathlib.Analysis.Calculus.Deriv.Basic
import Mathlib.Analysis.SpecialFunctions.Exp
import Mathlib.Topology.MetricSpace.Basic

-- Measure Theory
import Mathlib.MeasureTheory.Measure.MeasureSpace
import Mathlib.MeasureTheory.Integral.Lebesgue
import Mathlib.MeasureTheory.Function.ConditionalExpectation

-- Probability
import Mathlib.Probability.ProbabilityMassFunction.Basic
import Mathlib.Probability.Independence.Basic
import Mathlib.Probability.ConditionalProbability

-- Algebra
import Mathlib.Algebra.Ring.Basic
import Mathlib.Algebra.Field.Basic
import Mathlib.RingTheory.Ideal.Basic

-- Topology
import Mathlib.Topology.Basic
import Mathlib.Topology.Compactness.IsCompact
import Mathlib.Topology.ContinuousFunction.Basic

-- Linear Algebra
import Mathlib.LinearAlgebra.Basic
import Mathlib.LinearAlgebra.Matrix.Determinant
import Mathlib.LinearAlgebra.Dimension.Finrank

-- Category Theory
import Mathlib.CategoryTheory.Category.Basic
import Mathlib.CategoryTheory.Functor.Basic
import Mathlib.CategoryTheory.Limits.Shapes.Products

-- Combinatorics
import Mathlib.Data.Finset.Basic
import Mathlib.Algebra.BigOperators.Group.Finset
import Mathlib.Combinatorics.SimpleGraph.Basic

-- Commonly needed tactics
import Mathlib.Tactic.Ring
import Mathlib.Tactic.Linarith
import Mathlib.Tactic.FieldSimp
import Mathlib.Tactic.Positivity
import Mathlib.Tactic.FunProp
import Mathlib.Tactic.NormNum
import Mathlib.Tactic.GCongr
```

---

## When Responding to Users

1. **Error message:** Diagnose it. Common causes: missing import, wrong universe,
   typeclass not found, elaboration timeout, `simp` failure. Give the fix.

2. **"How do I prove X?":** Search Mathlib first (suggest the likely lemma name). If
   not there, sketch the strategy and provide working Lean code with imports.

3. **Planning a formalization:** Design the definition hierarchy, identify Mathlib
   coverage, map the dependency chain. Load `references/project-architecture.md`.

4. **Writing a Mathlib PR:** Check naming, style, imports, linting, documentation.
   Load `references/naming-and-style.md`.

5. **Working in a specific domain:** Load the appropriate `references/domains/*.md`.

6. **Always provide complete, compilable code** with imports when possible.
