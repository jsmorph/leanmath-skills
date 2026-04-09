# Project Architecture for Research Formalization

> **Sources:** Scott Armstrong, "Formalizing De Giorgi-Nash-Moser theory in Lean" (2026);
> jsmorph/armstrong-kempe-instructions gist; Terence Tao, "Formalizing the proof of PFR in
> Lean4 using Blueprint" (2023); Baanen et al., "Growing Mathlib" (2026).
> See `references/SOURCES.md` for full citations.

## Table of Contents

1. [Project Planning](#project-planning)
2. [Definition Engineering](#definition-engineering)
3. [Infrastructure and Interface Lemmas](#infrastructure-and-interface-lemmas)
4. [File and Module Organization](#file-and-module-organization)
5. [The Blueprint Model](#the-blueprint-model)
6. [Working with Mathlib's Type Hierarchy](#working-with-mathlibs-type-hierarchy)
7. [Elaboration Engineering](#elaboration-engineering)
8. [Using LLMs Effectively](#using-llms-effectively)
9. [Cleanup and Consolidation](#cleanup-and-consolidation)
10. [Domain-Specific Guidance](#domain-specific-guidance)

---

## Project Planning

### Fix the target before writing code

Start from a theorem package with fixed mathematical scope. Before writing Lean:

1. **State the top-level results precisely** — not "prove regularity theory" but
   "prove interior Hölder regularity for weak solutions of uniformly elliptic
   divergence-form equations with bounded measurable coefficients."

2. **Map the intermediate dependence chain** — which lemmas depend on which. This is
   the skeleton of the project. Example:
   ```
   Local boundedness (subsolutions)
       ↓
   Weak Harnack inequality (supersolutions)
       ↓
   Harnack inequality (solutions)
       ↓
   Interior Hölder regularity (solutions)
   ```

3. **Identify what Mathlib already provides** — search thoroughly (see
   `search-and-discovery.md`). For each concept in your chain, determine:
   - Does Mathlib have the definition? (Use it.)
   - Does Mathlib have partial results? (Build on them.)
   - Does Mathlib have nothing? (You'll need to build from scratch.)

4. **Decide the level of generality** — The endpoint determines the abstraction level
   from the start. If the target theorem crosses several kinds of objects, the library
   needs those passages in stable form early. If it uses the same reduction device
   in several places, formalize that device once.

### Choose a target that warrants library work

A serious development should leave behind reusable definitions, transport lemmas,
admissibility statements, and interfaces that later arguments can use. An isolated
theorem may be worth checking, but it tests less and leaves less behind.

---

## Definition Engineering

### Prefer Mathlib definitions

Never redefine something Mathlib already has. If Mathlib's `IsCompact` doesn't match
your paper's definition, prove they're equivalent and work with Mathlib's version.

### Design for the elaborator, not just the mathematician

A mathematically natural abstraction may:
- Elaborate slowly (deep typeclass search)
- Trigger unwanted coercions
- Make `simp` ineffective

Treat elaboration behavior as part of the design. Compile time is a constraint.

### Concrete guidance

- **Use typeclasses for algebraic structure:**
  ```lean
  variable {R : Type*} [CommRing R] [TopologicalSpace R] [TopologicalRing R]
  ```

- **Use bundled morphisms for maps:**
  ```lean
  variable (f : R →+* S)  -- RingHom, not a bare function with separate hypotheses
  ```

- **Use `Prop`-valued classes for properties:**
  ```lean
  variable [IsNoetherian R M]  -- not a term-level proof
  ```

- **Provide API immediately after definition:**
  ```lean
  def myDef : ... := ...

  @[simp] theorem myDef_apply (x : α) : myDef x = ... := rfl
  @[ext] theorem myDef_ext : ... := ...
  theorem myDef_mono : Monotone myDef := ...
  ```

- **Mark reducibility deliberately:**
  ```lean
  @[reducible] def myAlias := ExistingDef  -- unfolds freely
  -- vs.
  @[irreducible] def myOpaque := ...       -- never unfolds automatically
  ```

### Avoid `EuclideanSpace` for analysis

The Mathlib type `EuclideanSpace ℝ (Fin n)` causes severe elaboration blowups in
analysis-heavy developments. Work with `Fin n → ℝ` or `ι → ℝ` directly. This is
documented experience from the De Giorgi–Nash–Moser formalization.

---

## Infrastructure and Interface Lemmas

### The hidden layer

In advanced formalization, the main work lies between definitions and headline
theorems. Paper proofs hide this layer inside phrases like "standard setup," "after
localization," or "by a routine reduction." In Lean, this becomes:

- Restriction maps and their properties
- Witnesses and approximation lemmas
- Compatibility statements across formal settings
- Transport results between representations

**Design this layer so that later theorem statements read naturally.** If every proof
fights the same coercion problem or missing admissibility lemma, the defect is in the
architecture.

### Interface lemmas

Many of the most valuable lemmas let the main argument move cleanly among
representations:

```lean
-- Moving between pointwise and a.e. statements
theorem ae_of_pointwise : (∀ x, P x) → ∀ᵐ x ∂μ, P x := ...

-- Moving between local and global
theorem local_to_global : (∀ x ∈ s, P x) → P_global s := ...

-- Moving between coordinate descriptions
theorem coord_change : P_in_coords₁ ↔ P_in_coords₂ := ...
```

If a boundary is crossed constantly, formalize the crossing once and reuse everywhere.

### Formalize hidden work explicitly

Paper proofs suppress:
- **Truncations and cutoffs** — prove they are admissible as test functions
- **Regularized powers** — control their weak gradients explicitly
- **Standard reductions** (unit-ball reduction, rescaling, extension) — implement
  through explicit operators, not verbal assertions
- **Quantitative iterations** — De Giorgi iteration, Moser iteration, oscillation
  decay: exponents, radii, cutoffs, and inequalities must line up exactly. The hidden
  compatibility conditions become named lemmas.

---

## File and Module Organization

### Principles

1. **One focused topic per file.** A file about "Sobolev spaces" should not also
   contain PDE regularity theory.

2. **Target ≤ 1000 lines per file.** Split at ~1000 lines; the Mathlib linter warns
   around 1500.

3. **Organize by the elaborator's needs**, not by paper exposition order. Split files
   where the elaborator needs relief. Package intermediate results where they
   stabilize interfaces and cut search space.

4. **Keep imports narrow.** Each file imports only what it needs. This enables
   parallelism in compilation.

### Recommended project structure

```
MyProject/
├── lakefile.lean
├── lean-toolchain
├── MyProject.lean                    -- root import file
├── MyProject/
│   ├── Defs/                         -- Core definitions
│   │   ├── WeakSolution.lean
│   │   ├── EllipticOperator.lean
│   │   └── SobolevSpace.lean
│   ├── Infrastructure/               -- Interface and transport lemmas
│   │   ├── Admissibility.lean
│   │   ├── Truncation.lean
│   │   └── Rescaling.lean
│   ├── Estimates/                    -- Quantitative results
│   │   ├── EnergyEstimate.lean
│   │   ├── DeGiorgiIteration.lean
│   │   └── MoserIteration.lean
│   ├── Main/                         -- Headline theorems
│   │   ├── LocalBoundedness.lean
│   │   ├── WeakHarnack.lean
│   │   ├── HarnackInequality.lean
│   │   └── HolderRegularity.lean
│   └── Auxiliary/                    -- Helper lemmas not fitting elsewhere
│       ├── MeasureEstimates.lean
│       └── FunctionalInequalities.lean
```

### lakefile.lean setup

```lean
import Lake
open Lake DSL

package myProject where
  leanOptions := #[
    ⟨`autoImplicit, false⟩  -- Require explicit variable declarations
  ]

@[default_target]
lean_lib MyProject where
  srcDir := "MyProject"

require mathlib from git
  "https://github.com/leanprover-community/mathlib4" @ "main"
```

### Getting Mathlib cache

After `lake update`:
```bash
lake exe cache get    -- Download precompiled Mathlib oleans
lake build            -- Build your project only
```

---

## The Blueprint Model

For large projects, use Patrick Massot's Blueprint tool to maintain a parallel
human-readable description linked to the Lean formalization.

### What a blueprint provides

- A **dependency graph** of lemmas and definitions
- **LaTeX descriptions** of each node (human-readable proof sketch)
- **Status tracking** (stated / partially proved / fully proved)
- **Links** between LaTeX nodes and Lean declarations

### When to use a blueprint

Use a blueprint when:
- The project involves more than ~20 interconnected lemmas
- Multiple people are contributing
- You need to track progress across a long development
- You want to communicate the proof structure to mathematicians who don't read Lean

### Blueprint workflow

1. Write the proof in LaTeX as an "informal blueprint" — more explicit than a paper
   proof, but without Lean syntax.
2. Break the proof into atomic claims (each becomes a blueprint node).
3. Map dependencies between claims.
4. Formalize each claim as a Lean declaration.
5. Link Lean declarations to blueprint nodes.
6. The blueprint website updates automatically to show progress.

### Setup

See https://github.com/leanprover-community/leanblueprint for the tool.

---

## Working with Mathlib's Type Hierarchy

### Algebraic hierarchy

Mathlib builds algebraic structures via typeclasses with inheritance:
```
Monoid → Group → CommGroup
    ↘ CommMonoid ↗
         ↓
Semiring → Ring → CommRing → Field
     ↓
OrderedSemiring → OrderedRing → LinearOrderedField
```

**Always use the weakest structure that suffices.** A lemma about `CommMonoid` is more
reusable than one about `CommRing`.

### Morphism hierarchy

```
OneHom → MonoidHom → RingHom → AlgHom
     ↘ MulHom ↗
```

Use the most specific morphism type that applies. Lean's coercion system will handle
upward coercions automatically.

### Topological/metric hierarchy

```
TopologicalSpace → UniformSpace → PseudoMetricSpace → MetricSpace
        ↓
T1Space → T2Space (Hausdorff)
        ↓
NormalSpace → CompactSpace
```

### Analysis hierarchy

```
NormedAddCommGroup → InnerProductSpace
        ↓
NormedSpace → CompleteSpace (Banach)
```

---

## Elaboration Engineering

### Keep notes on elaboration fixes

When you discover a workaround for an elaboration problem, document it in a markdown
file in your project. The same failures recur, and forgetting the fix wastes time.

### Common elaboration issues and fixes

**Typeclass resolution timeout:**
```lean
-- Provide the instance explicitly
@[instance] local instance : Foo α := inferInstance
-- or pass it as an argument
have : Foo α := inferInstance
```

**Unification failure with coercions:**
```lean
-- Be explicit about the coercion
show (↑n : ℤ) = ...
-- or use norm_cast / push_cast
```

**Slow `simp`:**
```lean
-- Profile it
set_option profiler true in
-- Replace with simp only
simp only [specific_lemma_1, specific_lemma_2]
```

**Large proof terms:**
```lean
-- Break into helper lemmas
private theorem step1 : ... := by ...
private theorem step2 : ... := by ...
theorem main : ... := step1.trans step2
```

### `autoImplicit false`

Set `autoImplicit := false` in your lakefile. This requires all variables to be
declared explicitly, preventing mysterious universe errors and accidental free
variables.

---

## Using LLMs Effectively

### What LLMs are good at

- Writing boilerplate (API lemmas, `simp` lemmas, monotonicity proofs)
- Translating informal proof sketches into tactic sequences
- Trying many proof strategies quickly
- Discovering Mathlib lemma names by approximate description
- Refactoring and code cleanup

### What humans must control

- **Target selection** — which theorems to formalize
- **Proof architecture** — the dependency chain and abstraction levels
- **Critical representation choices** — which Mathlib structures to use
- **Interface design** — what the library's public API should look like
- **Mathematical correctness** — the LLM can produce plausible-looking nonsense

### Effective LLM workflow

1. **Write detailed proof blueprints** for the LLM to implement. The more precise
   the mathematical specification, the better the Lean output.

2. **Have the LLM surface blocked interfaces** — ask it to write down where it gets
   stuck and what lemmas are missing.

3. **Have the LLM document elaboration repairs** — when it finds a workaround for a
   compilation issue, make it write that down in markdown for reuse.

4. **Use the LLM's speed to expose uncertainty** rather than conceal it. A model can
   move quickly through local proof search, but it does not replace mathematical
   judgment about what the library should contain.

### The Armstrong-Kempe model

In the De Giorgi–Nash–Moser formalization (~56,000 lines in ~2 weeks):
- No human touched Lean files directly
- Humans supplied detailed proof blueprints
- Humans pushed models through difficult points
- Models documented elaboration-fixing tricks in markdown for reuse
- The result was sorry-free and axiom-free

This model works when the human has complete mathematical understanding and the
formalization is bottlenecked by Lean syntax / Mathlib API knowledge rather than
mathematical insight.

---

## Cleanup and Consolidation

### Plan cleanup from the start

The first successful compile marks when library repair becomes visible. Budget
significant time for:

1. **Merge duplicate lemmas** — large developments accumulate variants
2. **Delete vestigial code** — lemmas that were needed during development but not in
   the final proof
3. **Repair file boundaries** — reorganize files by topic, not by chronological
   development order
4. **Fix naming** — align with Mathlib conventions
5. **Silence linter warnings** — `#lint` should be clean
6. **Add documentation** — module docstrings and declaration docstrings

### Diagnose structural problems during cleanup

When one part of the library accumulates wrappers, duplicate statements, or massive
files, the problem usually lies in the underlying organization. Cleanup should shorten
later proofs and stabilize later extensions.

### Checklist before considering a file done

- [ ] All `sorry`s resolved
- [ ] `#lint` produces no warnings
- [ ] Every public definition has a docstring
- [ ] Every file has a module docstring
- [ ] `simp` calls are all `simp only [...]`
- [ ] No search tactics (`exact?`, `apply?`) remain
- [ ] Imports are minimal (no unused imports)
- [ ] Lines ≤ 100 characters
- [ ] File ≤ 1500 lines (preferably ≤ 1000)
- [ ] Naming follows Mathlib conventions
- [ ] `set_option maxHeartbeats` is scoped (not global)

---

## Domain-Specific Guidance

### Analysis / PDE

- Avoid `EuclideanSpace`; use `ι → ℝ` directly
- Sobolev spaces: check `Mathlib.Analysis.InnerProductSpace` and
  `Mathlib.MeasureTheory` for existing infrastructure
- For weak formulations, you need explicit admissibility lemmas for test functions
- Iterations (De Giorgi, Moser) require named lemmas for all exponent/radius/cutoff
  compatibility conditions
- `norm_num`, `positivity`, and `linarith` are your workhorses for quantitative bounds

### Algebra / Number Theory

- Use bundled morphisms (`RingHom`, `AlgHom`) not bare functions
- Localization, completion, and tensor products are well-developed in Mathlib
- For new algebraic structures, follow the typeclass hierarchy pattern precisely
- `ring`, `group`, `abel` close most algebraic identities

### Topology / Geometry

- `fun_prop` handles most continuity/differentiability goals
- For manifolds, see `Mathlib.Geometry.Manifold`
- Compact spaces: prefer `IsCompact s` (property of a set) over `CompactSpace α`
  (property of the whole type) unless the entire space is compact

### Measure Theory / Probability

- `IsProbabilityMeasure` vs `ProbabilityMeasure`: the former is a typeclass
  (property), the latter is a bundled type
- `filter_upwards` is essential for a.e. reasoning
- Conditional expectation: `MeasureTheory.condexp`
- Independence: `ProbabilityTheory.IndepFun`

### Category Theory

- Heavily bundled: functors, natural transformations, limits are all structures
- `aesop_cat` is the standard automation tactic
- Commutative diagrams: `simp` with category-specific lemmas, or `slice_lhs`/`slice_rhs`
