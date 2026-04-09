---
name: lean4-mathlib-research
description: >
  Mathematical knowledge layer for research-level Lean 4 formalization with Mathlib.
  For LLMs and LLM-driven agents. Use when the task requires knowing what Mathlib
  provides, how its API is organized, what types/lemmas/tactics to use in a specific
  mathematical domain, how to name things, or how to architect a formalization project.
  Trigger on: Lean 4, Mathlib, tactic proofs, formalization, .lean files importing
  Mathlib, proof debugging, naming conventions, Mathlib search, definition engineering,
  project planning. Even a pasted Lean error or "how do I prove X in Lean" qualifies.
---

# Lean 4 + Mathlib: Mathematical Knowledge for LLMs

## Purpose and Scope

This skill is the **mathematical knowledge layer** for LLMs and agents doing
research-level formalization in Lean 4 with Mathlib. It tells you *what Mathlib has*,
*how to find it*, *how to use it*, and *how the math maps to Lean types and tactics*
across seven mathematical domains.

**For proving workflow, sorry management, proof golfing, compiler-guided repair, and
LSP tool integration**, see [cameronfreer/lean4-skills](https://github.com/cameronfreer/lean4-skills)
(MIT licensed). That skill provides the structured prove → review → golf → checkpoint
loop, compilation error debugging, and the operational mechanics of driving Lean from
an agent. This skill provides the mathematical content that workflow operates on.

**For Mathlib PR conventions, review guidelines, and CI tooling**, see
[leanprover/skills](https://github.com/leanprover/skills) (the official Lean team
skills for mathlib-pr, mathlib-review, mathlib-build).

## Sources

This skill draws from: Mathlib's official documentation (naming, style, contributing
guidelines); Rémy Degenne's probability guide; Terence Tao's phrasebook and proof
tours; the "Growing Mathlib" paper (Baanen et al. 2026); Cameron Freer's lean4-skills,
especially [mathlib-guide.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/mathlib-guide.md),
[domain-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/domain-patterns.md),
[measure-theory.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/measure-theory.md),
and [lean-phrasebook.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/lean-phrasebook.md);
and Mathlib API documentation. Full citations with URLs are in
[Sources and References](references/SOURCES.md).

## How to Use This Skill

**Always loaded:** This file. Contains the core mathematical workflow, tactic decision
tree, math-to-Lean translation patterns, and dispatch table for deeper references.

**Load on demand:** One or two reference files per query, based on the dispatch table
below. Don't load everything.

---

## Dispatch Table

### Cross-Cutting References

| File | Load when... |
|------|-------------|
| [Search and Discovery](references/search-and-discovery.md) | Need to find a Mathlib lemma, definition, or file. Covers five search strategies, naming conventions for guessing names, Mathlib file hierarchy, Loogle/LeanSearch. |
| [Naming and Style](references/naming-and-style.md) | Naming definitions/lemmas, formatting code, preparing a Mathlib PR. Full capitalization rules, symbol→name dictionary, variable conventions, file headers, linting. |
| [Project Architecture](references/project-architecture.md) | Planning a multi-file formalization. Definition engineering, Mathlib integration, file organization, the Blueprint model, type hierarchies, contributing to Mathlib. |

### Domain Sub-Skills

Each covers: setup boilerplate, core Mathlib types, key lemma names, standard variable
conventions, important API patterns, domain-specific tactics, common pitfalls, and
curated imports.

| File | Mathematical domain |
|------|-------------------|
| [Probability](references/domains/probability.md) | Probability spaces, random variables, independence, conditioning, martingales, kernels |
| [Measure Theory and Analysis](references/domains/measure-theory-analysis.md) | Measures, integration (Lebesgue + Bochner), Lp spaces, derivatives, a.e. reasoning, filters |
| [Combinatorics](references/domains/combinatorics.md) | Finset, big operators (∑/∏), counting, graphs, set families, additive combinatorics |
| [Algebra and Number Theory](references/domains/algebra-number-theory.md) | Groups, rings, fields, ideals, localization, Galois theory, Dedekind domains |
| [Topology](references/domains/topology.md) | Topological spaces, filters, continuity, compactness, metric spaces, manifolds |
| [Linear Algebra](references/domains/linear-algebra.md) | Modules, vector spaces, matrices, eigenvalues, tensor products, inner products |
| [Category Theory](references/domains/category-theory.md) | Categories, functors, limits, adjunctions, abelian categories, sheaves |

### Also see (in cameronfreer/lean4-skills)

| Their file | Use for |
|-----------|---------|
| [lean-phrasebook.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/lean-phrasebook.md) | Math English → Lean translations, inspired by Tao's phrasebook |
| [compilation-errors.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/compilation-errors.md) | Error-by-error debugging, including type mismatch and unknown identifier failures |
| [measure-theory.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/measure-theory.md) | Deep measure theory: sub-σ-algebras, instance pollution, condexp |
| [instance-pollution.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/instance-pollution.md) | Typeclass conflicts critical for measure theory work |
| [tactics-reference.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/tactics-reference.md) | Comprehensive tactic catalog with decision trees |
| [calc-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/calc-patterns.md) | Calculational proof patterns and simp interaction |
| [proof-golfing.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/proof-golfing.md) | Optimizing compiled proofs |
| [domain-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/domain-patterns.md) | Patterns for measure theory, geometry, algebra, and number theory |

---

## Core Mathematical Workflow

### 1. Search Mathlib Before Proving

Mathlib has 100,000+ theorems. **Always search before writing tactics.**

**Search order for an LLM:**
```
1. Guess the name from conventions.  See [Naming and Style](references/naming-and-style.md).
   - "continuous preimage of compact is compact" → Continuous.isCompact_preimage
   - "sum over range telescopes" → Finset.sum_range_sub
2. Use exact?, apply?, rw? if you have a goal state
3. Grep the Mathlib source tree for keywords
4. Check the Mathlib file hierarchy by domain
5. Use Loogle for type-pattern search: Continuous ?f → IsCompact ?s → IsCompact (?f ⁻¹' ?s)
6. Use LeanSearch for natural language: "continuous function preserves compact sets"
```

### 2. Use the Right Mathlib Types

**Always prefer Mathlib's definitions.** Never redefine compactness, measurability,
continuity, etc. If Mathlib's version differs from your paper, prove the equivalence
and use Mathlib's.

**Standard patterns:**
- Algebraic structure → typeclasses: `[CommRing R]`, `[TopologicalSpace X]`
- Maps → bundled morphisms: `f : R →+* S` (not `f : R → S` with separate proofs)
- Properties → Prop-valued classes: `[IsNoetherian R M]`, `[IsProbabilityMeasure μ]`
- Subobjects → bundled: `Subgroup G`, `Ideal R`, `Submodule R M`

**Use the weakest typeclass that suffices.** A lemma about `CommMonoid` serves groups,
rings, and fields.

### 3. Provide API With Every Definition

```lean
def myDef : ... := ...
@[simp] theorem myDef_apply (x : α) : myDef x = ... := rfl
@[ext] theorem myDef_ext : ... := ...
```

A definition without `@[simp]` / `@[ext]` lemmas is unusable by automation.

### 4. Formalize What Papers Leave Implicit

Paper proofs say "by a routine argument" or "by standard reductions." In Lean, every
such step becomes a named lemma: truncations, cutoffs, admissibility of test functions,
rescalings, change-of-variables estimates, quantitative iteration compatibility.

---

## Math-to-Lean Quick Translation

Inspired by Tao's Lean Phrasebook.  For the expanded version, see
[lean-phrasebook.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/lean-phrasebook.md).

### Stating results
| Math | Lean |
|------|------|
| Let R be a commutative ring | `variable [CommRing R]` |
| Let f : X → Y be continuous | `variable (hf : Continuous f)` |
| Let μ be a probability measure on Ω | `variable {μ : Measure Ω} [IsProbabilityMeasure μ]` |
| Let H be a normal subgroup of G | `variable (H : Subgroup G) [H.Normal]` |
| For all ε > 0, there exists δ > 0 | `∀ ε > 0, ∃ δ > 0, ...` |

### Forward reasoning (building up)
| Math phrase | Lean tactic |
|------------|-------------|
| "Observe that A holds because..." | `have h : A := by ...` |
| "Applying f to h gives B" | `have hB : B := f h` |
| "This follows from h" | `exact h` |
| "Replace h with its consequence" | `replace h := f h` |

### Backward reasoning (reducing the goal)
| Math phrase | Lean tactic |
|------------|-------------|
| "It suffices to show A" | `suffices h : A by ...` |
| "Apply lemma L" | `apply L` or `exact L _ _` |
| "By the definition of X" | `unfold X` or `simp only [X]` |
| "By cases on h" | `rcases h with ⟨a, b⟩ \| c` |
| "By contradiction" | `by_contra h` |

### Equational / inequality reasoning
| Math phrase | Lean |
|------------|------|
| "a = b = c" chain | `calc a _ = b := by ... _ = c := by ...` |
| "a ≤ b ≤ c" chain | `calc a _ ≤ b := by ... _ ≤ c := by ...` |
| "by monotonicity" | `gcongr` |
| "by the triangle inequality" | `norm_add_le` or `dist_triangle` |

---

## Tactic Decision Tree

When you have a goal, try in this order:

**Atomic closers (try first):**
`rfl` → `exact h` → `assumption` → `contradiction`

**Arithmetic / algebraic:**
`ring` (ring eq) → `field_simp; ring` (field eq) → `omega` (ℕ/ℤ linear) →
`linarith` (ordered field linear) → `nlinarith` (nonlinear) → `norm_num` (numerical) →
`positivity` (0 < x or 0 ≤ x)

**Search (discovery, not production):**
`exact?` → `apply?` → `rw?` → `simp?`

**Structural:**
`ext` (extensionality) → `congr` / `gcongr` (congruence) → `constructor` (split ∧/↔) →
`rcases` / `obtain` (decompose) → `induction ... with` → `by_cases h : P`

**Simplification:**
`simp only [...]` (always pin lemmas) → `simp_rw [...]` (rewrites under binders) →
`norm_cast` / `push_cast` (coercions)

**Domain automation:**
`fun_prop` (continuity/measurability/differentiability) → `measurability` →
`continuity` → `aesop` → `grind` → `aesop_cat` (category theory)

**Inequality chains:**
`calc` with `gcongr`, `linarith`, `positivity` in each step

**After proof compiles — clean up:**
Replace `simp` with `simp only [...]` (use `simp?` to find lemmas).
Replace `exact?` / `apply?` with the lemma they found.

---

## Common Import Groups

```lean
-- Measure Theory & Probability
import Mathlib.MeasureTheory.Measure.MeasureSpace
import Mathlib.MeasureTheory.Integral.Lebesgue
import Mathlib.Probability.Independence.Basic

-- Analysis & Calculus
import Mathlib.Analysis.Calculus.Deriv.Basic
import Mathlib.Analysis.SpecialFunctions.Exp
import Mathlib.Topology.MetricSpace.Basic

-- Algebra & Number Theory
import Mathlib.Algebra.Ring.Basic
import Mathlib.RingTheory.Ideal.Basic
import Mathlib.FieldTheory.Galois.Basic

-- Combinatorics
import Mathlib.Data.Finset.Basic
import Mathlib.Algebra.BigOperators.Group.Finset

-- Linear Algebra
import Mathlib.LinearAlgebra.Basic
import Mathlib.LinearAlgebra.Matrix.Determinant

-- Category Theory
import Mathlib.CategoryTheory.Category.Basic
import Mathlib.CategoryTheory.Limits.Shapes.Products

-- Topology
import Mathlib.Topology.Basic
import Mathlib.Topology.Compactness.IsCompact

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

## When Responding

1. **Always provide complete, compilable code** with `import` statements.

2. **Search Mathlib first.** Before writing any tactic proof, suggest the likely
   existing lemma name. Use naming conventions to guess.

3. **For error messages:** Diagnose the cause (missing import, typeclass not found,
   universe mismatch, `simp` failure). Give the fix. For deep debugging, see
   [compilation-errors.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/compilation-errors.md).

4. **For "how do I prove X":** State the likely Mathlib lemma. If not in Mathlib,
   give the proof strategy and working tactic code.

5. **For project planning:** Load [Project Architecture](references/project-architecture.md). Help design
   the definition hierarchy and dependency chain.

6. **For domain-specific work:** Load the relevant file under
   [domain references](references/domains/).
