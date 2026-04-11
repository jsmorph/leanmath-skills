# Domain: Probability Theory in Mathlib

> **Sources:** Rémy Degenne, "Basic probability in Mathlib" (Lean community blog,
> 2024-10-17); Mathlib API docs for `Mathlib.Probability.*`.
> **Deep patterns:** cameronfreer's
> [measure-theory.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/measure-theory.md)
> for conditional expectation, sub-σ-algebras, and instance pollution, and
> [domain-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/domain-patterns.md)
> for the measure theory section. See [Sources and References](../SOURCES.md).

## Setup Boilerplate

Always begin probability files with:
```lean
open MeasureTheory ProbabilityTheory
open scoped ENNReal
```

## Probability Spaces

### Standard way (preferred in most cases)
```lean
variable {Ω : Type*} [MeasurableSpace Ω] {P : Measure Ω} [IsProbabilityMeasure P]
```
This allows multiple probability measures on the same space. Specify which measure
explicitly: `variance X P`, `P[X]`.

### With canonical measure (convenience)
```lean
variable {Ω : Type*} [MeasureSpace Ω] [IsProbabilityMeasure (ℙ : Measure Ω)]
```
The notation `ℙ` refers to `volume`. Use `𝔼[X]` for expectation. Note: you must
annotate `(ℙ : Measure Ω)` to fix the type.

**Important:** Lemmas written for `{P : Measure Ω}` apply to `ℙ`, but not conversely.
Mathlib favors the general `MeasurableSpace` spelling.

### `IsProbabilityMeasure` vs `ProbabilityMeasure`

| Type | Use when |
|------|----------|
| `{P : Measure Ω} [IsProbabilityMeasure P]` | Default choice. Works with all Mathlib lemmas. |
| `ProbabilityMeasure Ω` | Need the *topology* on probability measures (weak convergence / convergence in distribution). |

If you don't need weak convergence of measures, use `IsProbabilityMeasure`.

## Events and Probabilities

An event is just a `Set Ω` (ideally `MeasurableSet`). Probability is measure applied to a set:
```lean
example (P : Measure ℝ) (s : Set ℝ) : ℝ≥0∞ := P s
```

**`ℝ≥0∞` gotchas:** This type (`ENNReal`) is NOT a ring. Subtraction truncates to zero.
When a lemma about `ℝ` doesn't apply, look for `ENNReal.lemma_name_of_ne_top` variants.
Use `simp` to discharge `P s ≠ ∞` and `P s < ∞` for probability measures.

## Random Variables

A random variable is a measurable function:
```lean
variable {X : Ω → ℝ} (hX : Measurable X)
```

### Law / distribution
The law of `X` under `P` is `P.map X : Measure ℝ`. To state that `X` is Gaussian:
```lean
P.map X = gaussianReal μ v
```

### Expectation
- Bochner integral: `∫ ω, X ω ∂P` — shorthand `P[X]`, or `𝔼[X]` in a MeasureSpace
- Lebesgue integral: `∫⁻ ω, Y ω ∂P` for `Y : Ω → ℝ≥0∞` (no expectation notation)

### Integrability
`Integrable X P` states that `X` is integrable. Required by most expectation lemmas.
Key pattern:
```lean
example (hX : Integrable X P) : P[X] = ... := by ...
```

## Independence

### Two random variables
```lean
variable (hXY : IndepFun X Y P)
```

### Family of random variables
```lean
variable {X : ι → Ω → ℝ} (hX : iIndepFun (fun _ => inferInstance) X P)
```

### Two sets / family of sets
`IndepSet s t P`, `iIndepSet s P`

### Sigma-algebras
`Indep m₁ m₂ P`, `iIndep m P`

### Conditional independence
```lean
-- X, Y conditionally independent given sub-sigma-algebra m
variable (h : CondIndepFun m hm X Y P)

-- Conditionally independent given random variable Z
variable (h : CondIndepFun (mG.comap Z) hZ.comap_le X Y P)
```
Requires `StandardBorelSpace`.

## Conditioning

### Conditional probability
- `P[s|t]` = `P (s ∩ t) / P t`
- `P[|t]` = measure conditioned on event `t` (a new measure)
- `P[|X ← x]` = conditioned on `X = x` (meaningful for discrete probability)

### Conditional expectation
- `condexp m P Y` or `P[Y | m]` — conditional expectation given sub-sigma-algebra
- `P[Y | mE.comap X]` — conditional expectation given random variable `X`
- `P⟦s | m⟧` — conditional probability of set `s` given `m` (as `Ω → ℝ`)

### Conditional distribution
`condDistrib Y X P` — Markov kernel from `E` to `F` (requires `StandardBorelSpace`).

## Discrete Probability

Use `[DiscreteMeasurableSpace Ω]` — every set is measurable.
- `Measurable.of_discrete` for function measurability
- `MeasurableSet.of_discrete` for set measurability
- `PMF Ω` for probability mass functions; convert to measure via `p.toMeasure`
- Prefer `Measure` with `DiscreteMeasurableSpace` over `PMF` for library compatibility.
- Countable types with measurable singletons (like `ℕ`, `Fin n`) are automatically discrete.

## Known Distributions

Located in `Mathlib.Probability.Distributions.*`:
`Exponential`, `Gamma`, `Gaussian` (ℝ only), `Geometric`, `Pareto`, `Poisson`, `Uniform`.
Also: `Measure.dirac`, counting measure, Lebesgue measure.

```lean
-- Gaussian with mean μ, variance v
#check gaussianReal μ v  -- : Measure ℝ

-- Uniform on a finite set
#check uniformOn s  -- : Measure Ω
```

## Stochastic Processes

- Process: `X : ι → Ω → ℝ`
- Filtration: `ℱ : Filtration ι m`
- Adapted: `Adapted ℱ X`
- Martingale: `Martingale X ℱ P` (also `Submartingale`, `Supermartingale`)
- Stopping time: `IsStoppingTime ℱ τ` where `τ : Ω → ι`

**Caveat:** For `ι = ℕ`, stopping times take values in `ℕ` (cannot be infinite). This
can cause friction with informal definitions.

## Transition Kernels

`Kernel E F` — measurable function from `E` to `Measure F`.
- `IsMarkovKernel κ` — all images are probability measures
- `IsFiniteKernel κ`, `IsSFiniteKernel κ`

Kernels are used internally for independence and conditional independence definitions.

## Common Lemma Patterns

```lean
-- Expectation of sum
integral_add (hf : Integrable f P) (hg : Integrable g P)

-- Expectation of product of independent rvs
IndepFun.integral_mul_of_integrable

-- Variance
variance_def'  -- Var[X] = 𝔼[X²] - 𝔼[X]²

-- Markov inequality
ProbabilityTheory.meas_ge_le_mul_pow_snorm

-- Strong law of large numbers
ProbabilityTheory.strong_law_ae
```

## Key Imports
```lean
import Mathlib.Probability.ProbabilityMassFunction.Basic
import Mathlib.Probability.Independence.Basic
import Mathlib.Probability.ConditionalProbability
import Mathlib.Probability.Variance
import Mathlib.Probability.Distributions.Gaussian
import Mathlib.Probability.Martingale.Basic
import Mathlib.Probability.ConditionalExpectation
import Mathlib.Probability.Notation
```
