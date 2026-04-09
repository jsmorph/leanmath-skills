# Domain: Measure Theory and Analysis in Mathlib

> **Sources:** Mathlib API docs for `Mathlib.MeasureTheory.*` and `Mathlib.Analysis.*`;
> Mathematics in Lean ch. 10-11 (Avigad & Massot); Armstrong & Kempe De Giorgi–Nash–Moser
> formalization (avoid `EuclideanSpace` lesson). See `references/SOURCES.md`.

## Setup

```lean
open MeasureTheory Measure Filter Topology
open scoped ENNReal NNReal
```

## Measures

### Core types
- `MeasurableSpace α` — sigma-algebra on `α`
- `Measure α` — a measure on the measurable space
- `MeasureSpace α` — measurable space with canonical measure `volume`

### Important measure classes
| Class | Meaning |
|-------|---------|
| `IsFiniteMeasure μ` | `μ Set.univ < ∞` |
| `IsProbabilityMeasure μ` | `μ Set.univ = 1` |
| `SigmaFinite μ` | Countable cover by finite-measure sets |
| `IsLocallyFiniteMeasure μ` | Finite on compact sets |
| `Measure.IsAddLeftInvariant μ` | Haar-like left invariance |

### Constructing measures
```lean
#check Measure.dirac a          -- point mass
#check Measure.count             -- counting measure
#check volume                    -- Lebesgue measure on ℝ (in MeasureSpace ℝ)
#check Measure.restrict μ s     -- restrict μ to set s
#check Measure.map f μ          -- pushforward
#check Measure.comap f μ        -- pullback (less commonly used)
```

### Comparing measures
```lean
-- Two measures agree on all measurable sets
Measure.ext (h : ∀ s, MeasurableSet s → μ s = ν s) : μ = ν

-- Absolute continuity
Measure.AbsolutelyContinuous μ ν  -- notation: μ ≪ ν
-- meaning: ∀ s, ν s = 0 → μ s = 0
```

## Measurability

### Tactic: `measurability`
The `measurability` tactic proves measurability goals automatically by composing
`@[measurability]`-tagged lemmas. Use it as first attempt:
```lean
example : Measurable (fun x : ℝ => x ^ 2 + 3 * x) := by measurability
```

### `fun_prop` (more general)
`fun_prop` proves measurability AND continuity AND differentiability:
```lean
example : Measurable (fun x : ℝ => Real.exp (x ^ 2)) := by fun_prop
```

### Key measurability lemmas
```lean
Measurable.add, Measurable.mul, Measurable.neg, Measurable.inv
Measurable.comp, Measurable.prod_mk
Continuous.measurable  -- continuous → measurable (in Borel spaces)
MeasurableSet.inter, MeasurableSet.union, MeasurableSet.compl
measurableSet_Icc, measurableSet_Ioo  -- intervals are measurable
```

## Integration

### Two integral types

| Integral | Type | Notation | Use for |
|----------|------|----------|---------|
| Lebesgue | `∫⁻ x, f x ∂μ : ℝ≥0∞` | `lintegral` | `f : α → ℝ≥0∞`, always defined |
| Bochner | `∫ x, f x ∂μ : E` | `integral` | `f : α → E` where `E` is a Banach space |

Bochner integral returns `0` for non-integrable functions (by convention).

### Integrability
```lean
Integrable f μ  -- f is Bochner-integrable w.r.t. μ
-- Equivalent to: AEStronglyMeasurable f μ ∧ HasFiniteIntegral f μ
```

### Key integral lemmas
```lean
-- Linearity
integral_add (hf : Integrable f μ) (hg : Integrable g μ)
integral_smul (c : ℝ) (f : α → E)

-- Monotonicity
integral_mono (hf : Integrable f μ) (hg : Integrable g μ) (h : f ≤ᵐ[μ] g)

-- Monotone convergence (for ℝ≥0∞)
lintegral_iSup (hf : ∀ n, Measurable (f n)) (h_mono : Monotone f)

-- Dominated convergence
tendsto_integral_of_dominated_convergence

-- Triangle inequality
norm_integral_le_integral_norm

-- Integral over a set
set_integral_mono, integral_union

-- Fubini-Tonelli
lintegral_lintegral  -- for ℝ≥0∞ (always valid for σ-finite)
integral_prod        -- for Bochner integral
```

## Almost Everywhere (a.e.) Reasoning

### The `ae` filter
`μ.ae` is the "almost everywhere" filter. A property holds a.e. when the set where
it fails has measure zero.

```lean
-- "P holds for μ-almost every x"
∀ᵐ x ∂μ, P x     -- notation for Filter.Eventually P μ.ae
```

### `filter_upwards` — the essential tactic
```lean
-- Combine multiple a.e. hypotheses
example (h₁ : ∀ᵐ x ∂μ, f x ≤ g x) (h₂ : ∀ᵐ x ∂μ, g x ≤ h x) :
    ∀ᵐ x ∂μ, f x ≤ h x := by
  filter_upwards [h₁, h₂] with x hfg hgh
  exact le_trans hfg hgh
```

### `ae_of_all` — pointwise → a.e.
```lean
example (h : ∀ x, f x ≤ g x) : ∀ᵐ x ∂μ, f x ≤ g x :=
  ae_of_all μ h
```

## Lp Spaces

```lean
-- f is in Lp
Memℒp f p μ  -- f ∈ L^p(μ)

-- The Lp space as a type
Lp E p μ  -- Banach space of L^p functions

-- Norm
snorm f p μ  -- the L^p seminorm (in ℝ≥0∞)
```

## Derivatives and Calculus

```lean
-- Fréchet derivative
HasFDerivAt f f' x       -- f has derivative f' at x
DifferentiableAt ℝ f x   -- f is differentiable at x
fderiv ℝ f x             -- the derivative (a linear map)

-- Scalar derivative (for f : ℝ → E)
HasDerivAt f f' x
deriv f x

-- Within a set
HasFDerivWithinAt f f' s x
DifferentiableOn ℝ f s
fderivWithin ℝ f s x

-- Fundamental theorem of calculus
intervalIntegral.integral_hasDerivAt_right
intervalIntegral.integral_eq_sub_of_hasDerivAt
```

## Topology and Continuity in Analysis

### Filters
Mathlib uses filters extensively. Key filters:
```lean
𝓝 x        -- neighborhood filter at x
𝓝[s] x     -- neighborhood filter within set s
atTop       -- filter at infinity for ordered types
ae μ        -- almost everywhere filter
```

### Continuity
```lean
Continuous f                -- globally continuous
ContinuousAt f x           -- continuous at x
ContinuousOn f s           -- continuous on set s
ContinuousWithinAt f s x   -- continuous within s at x
```

### Tactic: `fun_prop`
Proves continuity, measurability, differentiability of composed expressions:
```lean
example : Continuous (fun x : ℝ => Real.exp (Real.sin x + x ^ 2)) := by fun_prop
```

## Norms and Distances

```lean
‖x‖           -- norm (notation for NNNorm or Norm)
dist x y      -- distance
edist x y     -- extended distance (ℝ≥0∞)
```

### Key lemma patterns
```lean
norm_add_le x y          -- triangle inequality
dist_comm x y            -- symmetry
norm_nonneg x            -- ‖x‖ ≥ 0
```

## Common Proof Patterns

### Integral inequality via a.e. bound
```lean
example (hf : Integrable f μ) (hg : Integrable g μ) (h : ∀ᵐ x ∂μ, f x ≤ g x) :
    ∫ x, f x ∂μ ≤ ∫ x, g x ∂μ :=
  integral_mono hf hg h
```

### Showing a set has measure zero
```lean
-- Via absolute continuity
Measure.AbsolutelyContinuous.ae_eq

-- Via countable union
measure_iUnion_null_iff

-- Via density / Lebesgue differentiation
Measure.ae_tendsto_measure_inter_div
```

### Epsilon-delta with filters
```lean
-- ContinuousAt via filter
rw [Metric.continuousAt_iff]
intro ε hε
...
```

## Avoid `EuclideanSpace`

For analysis-heavy work, `EuclideanSpace ℝ (Fin n)` causes severe elaboration problems.
Use `Fin n → ℝ` or `ι → ℝ` directly. This is documented experience from the
De Giorgi–Nash–Moser formalization.

## Key Imports
```lean
import Mathlib.MeasureTheory.Measure.MeasureSpace
import Mathlib.MeasureTheory.Measure.Lebesgue.Basic
import Mathlib.MeasureTheory.Integral.Bochner
import Mathlib.MeasureTheory.Integral.Lebesgue
import Mathlib.MeasureTheory.Function.AEEqFun
import Mathlib.MeasureTheory.Function.LpSpace
import Mathlib.Analysis.Calculus.Deriv.Basic
import Mathlib.Analysis.Calculus.FDeriv.Basic
import Mathlib.Analysis.NormedSpace.Basic
import Mathlib.Analysis.SpecialFunctions.Integrals
import Mathlib.Topology.MetricSpace.Basic
```
