# Domain: Topology in Mathlib

> **Sources:** Mathlib API docs; Mathlib topology overview; Mathematics in Lean.
> **Extended:** cameronfreer's
> [domain-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/domain-patterns.md)
> for the analysis and topology section. See [Sources and References](../SOURCES.md).

## The Topological Hierarchy

```
TopologicalSpace → UniformSpace → PseudoMetricSpace → MetricSpace
        ↓                                                    ↓
  T0Space → T1Space → T2Space (Hausdorff)            EMetricSpace
        ↓                                   
  RegularSpace → NormalSpace
        ↓
  CompactSpace
```

## Filters: The Foundation

Mathlib's topology is built on **filters**, not epsilon-delta. Understanding filters
is essential for working with limits, continuity, and convergence.

### Key filters
```lean
𝓝 x           -- neighborhood filter at x
𝓝[s] x        -- nhdsWithin: neighborhoods within set s
atTop          -- filter at +∞ for ordered types
atBot          -- filter at -∞
cofinite       -- sets whose complement is finite
Filter.map f l -- image filter
```

### Filter operations
```lean
Filter.Tendsto f l₁ l₂   -- f tends to l₂ along l₁ (generalized limit)
Filter.Eventually p l     -- p holds eventually along l (∀ᶠ x in l, p x)
Filter.Frequently p l     -- p holds frequently along l (∃ᶠ x in l, p x)
```

### Limits via filters
```lean
-- "f(x) → y as x → a"
Filter.Tendsto f (𝓝 a) (𝓝 y)

-- "f(x) → y as x → +∞"
Filter.Tendsto f atTop (𝓝 y)

-- "f(x) → +∞ as x → a"
Filter.Tendsto f (𝓝 a) atTop

-- "f(x) → y as x → a within s"
Filter.Tendsto f (𝓝[s] a) (𝓝 y)
```

## Translating Textbook Topology into Lean

Recent topology teaching repos are useful mainly because they expose the translation layer between textbook point-set topology and current Lean 4 / Mathlib practice.

### What they are good for

- understanding `TopologicalSpace` from first principles
- learning how continuity, open sets, and induced constructions are encoded
- seeing small exercise-sized proofs before dropping into full Mathlib abstraction

### How to use them safely

- Prefer recent Lean 4 repos over older topology tutorials.
- Use them for onboarding and translation patterns, not as the final authority on current Mathlib APIs.
- When a pedagogical repo rebuilds topology without `Mathlib.Topology`, treat that as a learning aid. Before giving advice, map the local definitions back to current Mathlib structures.

## Continuity

### Levels of continuity
```lean
Continuous f                  -- globally continuous
ContinuousAt f x              -- continuous at a point
ContinuousOn f s              -- continuous on a set
ContinuousWithinAt f s x      -- continuous within s at x
```

### Tactic: `fun_prop`
First choice for proving continuity of composed expressions:
```lean
example : Continuous (fun x : ℝ => Real.exp (x ^ 2 + Real.sin x)) := by fun_prop
```

### Tactic: `continuity`
Older tactic, superseded by `fun_prop` but still works:
```lean
example : Continuous (fun p : ℝ × ℝ => p.1 + p.2) := by continuity
```

### Manual continuity proofs
```lean
-- Composition
Continuous.comp hg hf          -- g continuous, f continuous → g ∘ f continuous

-- Product
Continuous.prod_mk hf hg       -- (f, g) continuous from hf, hg

-- Standard functions
continuous_id, continuous_const, continuous_fst, continuous_snd
continuous_add, continuous_mul, continuous_neg, continuous_inv₀
```

## Open, Closed, Compact Sets

```lean
IsOpen s                       -- s is open
IsClosed s                     -- s is closed
IsCompact s                    -- s is compact
IsClopen s                     -- s is both open and closed

-- For the whole space
CompactSpace α                 -- α is compact
```

### Key lemmas
```lean
IsCompact.image hs hf          -- image of compact under continuous is compact
IsCompact.isClosed hs          -- compact → closed (in Hausdorff spaces)
isCompact_iff_finite_subcover  -- characterization
IsClosed.isCompact             -- closed subset of compact is compact (needs CompactSpace)
```

## Metric Spaces

```lean
variable [MetricSpace X]

dist x y : ℝ                   -- distance
Metric.ball x r                -- open ball {y | dist x y < r}
Metric.closedBall x r          -- closed ball
Metric.sphere x r              -- sphere
```

### Characterizations via metrics
```lean
Metric.continuousAt_iff        -- ∀ ε > 0, ∃ δ > 0, dist y x < δ → dist (f y) (f x) < ε
Metric.isOpen_iff              -- open ↔ every point has an open ball inside
Metric.isCompact_iff_isClosed_bounded  -- compact ↔ closed + bounded (in proper spaces)
```

### Lipschitz and Hölder continuity
```lean
LipschitzWith K f              -- dist (f x) (f y) ≤ K * dist x y
HolderWith C r f               -- dist (f x) (f y) ≤ C * dist x y ^ r
```

## Connectedness

```lean
IsConnected s                  -- s is connected
IsPathConnected s              -- s is path-connected
ConnectedSpace α               -- α is connected
```

## Topological Algebra

Mathlib has rich support for algebraic structures with compatible topologies:

```lean
TopologicalGroup G             -- group with continuous multiplication and inverse
TopologicalRing R              -- ring with continuous operations
TopologicalAddGroup A          -- additive group with continuous addition and negation
ContinuousSMul R M             -- continuous scalar multiplication
```

### Completions
```lean
UniformSpace.Completion α      -- completion of a uniform space
-- For groups/rings: automatically inherits algebraic structure
```

## Constructions

### Product topology
```lean
-- Automatic on α × β when both have TopologicalSpace
continuous_fst : Continuous (Prod.fst : α × β → α)
continuous_snd : Continuous (Prod.snd : α × β → β)
Continuous.prod_mk hf hg      -- (f, g) is continuous
```

### Subspace topology
```lean
-- Automatic on subtypes {x : α // p x}
continuous_subtype_val         -- inclusion is continuous
IsOpen.isOpenMap_subtype_val   -- open embedding
```

### Quotient topology
```lean
-- QuotientMap, IsOpenQuotientMap
Quotient.continuousLift        -- lift continuous function through quotient
```

## Common Proof Patterns

### Showing a set is open/closed
```lean
-- Open: usually via IsOpen.preimage or IsOpen.inter
example (hf : Continuous f) (hs : IsOpen s) : IsOpen (f ⁻¹' s) :=
  hs.preimage hf

-- Closed: via IsClosed.preimage or complement of open
example (hf : Continuous f) (hs : IsClosed s) : IsClosed (f ⁻¹' s) :=
  hs.preimage hf
```

### Compactness arguments
```lean
-- Extract finite subcover
IsCompact.elim_finite_subcover

-- Continuous image of compact
IsCompact.image hs hf

-- Compact + Hausdorff → closed
IsCompact.isClosed

-- Maximum on compact set
IsCompact.exists_isMaxOn hs hne hf
```

### Working with neighborhoods
```lean
-- "Eventually" in neighborhoods
example (h : ∀ᶠ x in 𝓝 a, P x) : ... := by
  rw [Filter.Eventually, Metric.mem_nhds_iff] at h
  obtain ⟨ε, hε, hball⟩ := h
  ...
```

## Manifolds and Geometry

For smooth manifolds, see `Mathlib.Geometry.Manifold.*`:
```lean
SmoothManifoldWithCorners I M   -- smooth manifold with model I
ContMDiff I I' n f              -- f is C^n between manifolds
Tangent I M                     -- tangent bundle
```

## Key Imports
```lean
import Mathlib.Topology.Basic
import Mathlib.Topology.Constructions
import Mathlib.Topology.ContinuousFunction.Basic
import Mathlib.Topology.Compactness.IsCompact
import Mathlib.Topology.MetricSpace.Basic
import Mathlib.Topology.MetricSpace.Lipschitz
import Mathlib.Topology.Algebra.Group.Basic
import Mathlib.Topology.Algebra.Ring.Basic
import Mathlib.Topology.UniformSpace.Basic
import Mathlib.Topology.Connected.Basic
import Mathlib.Topology.Order.Basic
```
