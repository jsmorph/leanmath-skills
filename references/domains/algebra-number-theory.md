# Domain: Algebra and Number Theory in Mathlib

> **Sources:** Mathlib API docs; Baanen et al. (Dedekind domains); Mathematics in Lean.
> **Extended:** cameronfreer's
> [domain-patterns.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/domain-patterns.md)
> for the algebra section. See [Sources and References](../SOURCES.md).

## The Algebraic Hierarchy

Mathlib builds algebra via typeclasses with carefully designed inheritance:

```
Semigroup → Monoid → Group → CommGroup
    ↘ CommSemigroup → CommMonoid ↗
Semiring → Ring → CommRing → Field
    ↘ CommSemiring ↗       ↘ IntegralDomain ↗
OrderedSemiring → OrderedRing → LinearOrderedField
```

**Always use the weakest typeclass that suffices.** A lemma about `CommMonoid` is
reusable for groups, rings, and fields. A lemma about `Field` is not.

## Core Algebraic Types

### Groups
```lean
variable [Group G]              -- multiplicative group
variable [AddCommGroup A]       -- additive abelian group
```
- `Subgroup G`, `QuotientGroup.Quotient N` (for `N : Subgroup G` with `[N.Normal]`)
- `MonoidHom` (`G →* H`), `MulEquiv` (`G ≃* H`)

### Rings
```lean
variable [CommRing R]
variable [Ring R] [IsDomain R]   -- integral domain
```
- `Ideal R` — ideals are bundled; `Ideal.span`, `Ideal.Quotient`
- `RingHom` (`R →+* S`), `RingEquiv` (`R ≃+* S`)
- `Polynomial R` (`R[X]`) — univariate polynomials
- `MvPolynomial σ R` — multivariate polynomials

### Fields and extensions
```lean
variable [Field K]
variable [Field K] [Field L] [Algebra K L]   -- field extension
```
- `IntermediateField K L` — subfields of L containing K
- `IsAlgClosed K`, `algebraicClosure K`
- `IsSplittingField`, `IsGalois`

## Morphisms: Always Bundled

Mathlib uses bundled morphisms. Never use a bare function + separate proof of
homomorphism properties.

| Type | Notation | Meaning |
|------|----------|---------|
| `MonoidHom` | `G →* H` | Monoid homomorphism |
| `AddMonoidHom` | `A →+ B` | Additive monoid homomorphism |
| `RingHom` | `R →+* S` | Ring homomorphism |
| `AlgHom` | `A →ₐ[R] B` | R-algebra homomorphism |
| `LinearMap` | `M →ₗ[R] N` | R-linear map |
| `MulEquiv` | `G ≃* H` | Multiplicative isomorphism |
| `RingEquiv` | `R ≃+* S` | Ring isomorphism |
| `AlgEquiv` | `A ≃ₐ[R] B` | Algebra isomorphism |

Coercions go upward automatically: `RingHom` coerces to `MonoidHom`, etc.

## Subobjects: Bundled

| Type | Meaning |
|------|---------|
| `Subgroup G` | Subgroup (bundled carrier + closure proofs) |
| `Subring R` | Subring |
| `Ideal R` | Ideal (special case of `Submodule R R`) |
| `Subalgebra R A` | Subalgebra |
| `IntermediateField K L` | Intermediate field extension |

All support `⊥` (trivial), `⊤` (whole), `⊔` (join/generated), `⊓` (meet/intersection).

## Key Design Patterns

### `algebraMap` for ring maps between algebra towers
```lean
-- The canonical map R → S when [Algebra R S]
algebraMap R S : R →+* S
```

### Localization
```lean
-- Localization at a submonoid
variable (S : Submonoid R) [IsLocalization S Sₘ]

-- Localization at a prime
variable (p : Ideal R) [p.IsPrime]
-- Use IsLocalization.AtPrime
```

### Quotient rings
```lean
-- Quotient by an ideal
variable (I : Ideal R)
Ideal.Quotient.mk I : R →+* R ⧸ I    -- the projection
Ideal.Quotient.lift I f hf            -- universal property
```

## Tactics for Algebra

| Tactic | Solves |
|--------|--------|
| `ring` | Commutative (semi)ring equalities |
| `noncomm_ring` | Non-commutative ring equalities |
| `group` | Multiplicative group equalities |
| `abel` | Additive abelian group equalities |
| `field_simp` | Clear denominators in fields |
| `norm_num` | Numerical computations |

### Common pattern: field equations
```lean
example (a b : ℚ) (hb : b ≠ 0) : a / b * b = a := by
  field_simp
```

## Number Theory

### Arithmetic functions and divisibility
```lean
Nat.Prime p                    -- p is prime
Nat.gcd a b, Nat.lcm a b
Nat.Coprime a b                -- gcd = 1
Int.emod, Int.ediv             -- Euclidean division
ZMod n                         -- ℤ/nℤ
```

### Dedekind domains and class groups
```lean
IsDedekindDomain R             -- Noetherian, integrally closed, Krull dim ≤ 1
ClassGroup R                   -- the ideal class group
NumberField K                  -- finite extension of ℚ
```
Mathlib has: finiteness of class number, Dirichlet unit theorem, class number formula.

### Valuations and local fields
```lean
Valuation R Γ₀                -- valuation
DiscreteValuation.Integers     -- valuation ring
```

### Galois theory
```lean
IsGalois K L                   -- L/K is Galois
IntermediateField.fixingSubgroup
IntermediateField.fixedField
-- The Galois correspondence is formalized
```

### Quadratic reciprocity, Hensel's lemma
Available in `Mathlib.NumberTheory.*`.

## Common Proof Patterns

### Working with ideals
```lean
-- Show two ideals are equal
Ideal.ext (h : ∀ x, x ∈ I ↔ x ∈ J)

-- Ideal membership
Ideal.mem_span_singleton       -- x ∈ Ideal.span {a} ↔ a ∣ x
Ideal.Quotient.eq_zero_iff_mem -- x̄ = 0 ↔ x ∈ I
```

### Polynomial arithmetic
```lean
open Polynomial in
example : (X + C 1) * (X - C 1) = X ^ 2 - C 1 := by ring
```

## Key Imports
```lean
import Mathlib.Algebra.Group.Basic
import Mathlib.Algebra.Ring.Basic
import Mathlib.Algebra.Field.Basic
import Mathlib.RingTheory.Ideal.Basic
import Mathlib.RingTheory.Ideal.Quotient.Basic
import Mathlib.RingTheory.Localization.Basic
import Mathlib.RingTheory.DedekindDomain.Basic
import Mathlib.FieldTheory.Galois.Basic
import Mathlib.NumberTheory.NumberField.Basic
import Mathlib.Data.Polynomial.Basic
import Mathlib.Data.ZMod.Basic
```
