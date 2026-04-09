# Domain: Linear Algebra in Mathlib

> **Sources:** Mathlib API docs for `Mathlib.LinearAlgebra.*`, `Mathlib.Analysis.InnerProductSpace.*`;
> Mathlib overview (linear algebra coverage); Mathematics in Lean ch. 8 (Avigad & Massot).
> See `references/SOURCES.md`.

## Core Types

### Modules and vector spaces
```lean
variable [CommRing R] [AddCommGroup M] [Module R M]       -- R-module M
variable [Field K] [AddCommGroup V] [Module K V]          -- K-vector space V
variable [Module.Finite R M]                               -- finitely generated
variable [Module.Free R M]                                 -- free module
variable [FiniteDimensional K V]                           -- finite-dimensional
```

`Module` is the general typeclass. A "vector space" in Lean is just a `Module` over a `Field`.

### Linear maps and equivalences
```lean
M →ₗ[R] N              -- LinearMap: R-linear map
M →ₗ⋆[σ] N             -- semilinear map (with ring hom σ : R →+* S)
M ≃ₗ[R] N              -- LinearEquiv: R-linear isomorphism
M →L[R] N              -- ContinuousLinearMap (bounded, for normed spaces)
M ≃L[R] N              -- ContinuousLinearEquiv
```

### Submodules
```lean
Submodule R M           -- R-submodule of M
Submodule.span R s      -- span of a set
Submodule.Quotient p    -- quotient module M / p
LinearMap.range f       -- image (as a submodule)
LinearMap.ker f         -- kernel (as a submodule)
```

## Bases and Dimension

```lean
-- A basis indexed by ι
Basis ι R M             -- ι-indexed R-basis of M

-- Constructing bases
Basis.ofVectorSpace K V  -- existence (nonconstructive, needs choice)
Pi.basisFun R n          -- standard basis of R^n

-- Dimension
Module.finrank K V : ℕ   -- dimension (returns 0 if infinite-dimensional)
Module.rank R M : Cardinal  -- rank as a cardinal

-- Key lemmas
Basis.ext_elem           -- basis determines a module element
FiniteDimensional.of_finrank_pos  -- finrank > 0 → finite-dimensional
Submodule.finrank_le     -- dim of submodule ≤ dim of module
```

## Matrices

```lean
Matrix (Fin m) (Fin n) R         -- m × n matrix over R
-- Also: Matrix m n R for general index types

-- Construction
!![1, 2; 3, 4]                   -- literal matrix notation
Matrix.of f                      -- from a function (i, j) ↦ f i j
1 : Matrix n n R                 -- identity matrix

-- Operations
A * B                             -- matrix multiplication
A.det                             -- determinant
A.trace                           -- trace
Aᵀ                                -- transpose
A⁻¹                               -- inverse (returns 0 if singular)
```

### Matrix ↔ LinearMap correspondence
```lean
-- Matrix representing a linear map w.r.t. bases
LinearMap.toMatrix b₁ b₂ f      -- matrix of f in bases b₁, b₂
Matrix.toLin b₁ b₂ A            -- linear map from matrix
```

### Determinant and invertibility
```lean
Matrix.det_mul                   -- det(AB) = det(A) * det(B)
Matrix.nonsing_inv               -- the inverse matrix
Matrix.mul_nonsing_inv           -- A * A⁻¹ = 1 when det ≠ 0
Matrix.isUnit_iff_isUnit_det     -- invertible ↔ det is unit
```

## Eigenvalues and Spectral Theory

```lean
Module.End.HasEigenvalue f μ     -- f has eigenvalue μ
Module.End.eigenspace f μ        -- eigenspace for μ
Module.End.Eigenvalues f         -- the set of eigenvalues

-- Characteristic polynomial
LinearMap.charpoly f             -- characteristic polynomial
-- Cayley-Hamilton
LinearMap.aeval_self_charpoly f  -- p_f(f) = 0

-- Minimal polynomial
minpoly K f                      -- minimal polynomial
```

## Bilinear Forms and Inner Products

```lean
-- Bilinear form
LinearMap.BilinForm R M          -- alias for M →ₗ[R] M →ₗ[R] R

-- Inner product space
variable [InnerProductSpace ℝ V]
inner x y : ℝ                   -- ⟪x, y⟫ (notation: \<< and \>>)

-- Orthogonality
Submodule.IsOrtho U W           -- U ⟂ W
orthogonalComplement U          -- U^⊥
```

### Key theorems
```lean
inner_self_nonneg                -- ⟪x, x⟫ ≥ 0
real_inner_le_norm               -- Cauchy-Schwarz
```

## Tensor Products

```lean
TensorProduct R M N              -- M ⊗[R] N
TensorProduct.tmul R m n         -- m ⊗ n (notation: m ⊗ₜ[R] n)

-- Universal property
TensorProduct.lift f             -- bilinear f lifts to M ⊗ N → P
```

## Multilinear Algebra

```lean
MultilinearMap R (fun i => M i) N     -- multilinear map
AlternatingMap R M N ι                -- alternating map
ExteriorAlgebra R M                   -- exterior algebra
```

## Common Tactics

| Tactic | Use for |
|--------|---------|
| `simp [LinearMap.map_add, ...]` | Simplify linear map applications |
| `ext` | Prove linear maps equal by applying to basis/all elements |
| `ring` | Matrix/scalar arithmetic |
| `norm_num` | Concrete matrix computations |
| `decide` | Small finite-dimensional computations (SLOW for large) |
| `linarith` | Linear arithmetic on dimensions |
| `module` | (if available) Module arithmetic |

## Common Proof Patterns

### Prove two linear maps are equal
```lean
ext x   -- reduces to showing f x = g x for all x
-- or, for matrices:
ext i j -- reduces to showing A i j = B i j for all i j
```

### Dimension argument
```lean
-- Rank-nullity
LinearMap.finrank_range_add_finrank_ker f

-- Dimension of quotient
Submodule.finrank_quotient_add_finrank p
```

### Show a set is linearly independent
```lean
linearIndependent_iff.mpr       -- via the definition
LinearIndependent.of_comp       -- compose with injective map
```

### Work in coordinates
```lean
-- Pick a basis, express in coordinates
let b := Basis.ofVectorSpace K V
simp [b.repr_apply, b.coord_apply]
```

## Normed Spaces (Functional Analysis)

```lean
variable [NormedAddCommGroup E] [NormedSpace ℝ E]
-- E is a normed vector space over ℝ

variable [CompleteSpace E]    -- Banach space
variable [InnerProductSpace ℝ E] [CompleteSpace E]  -- Hilbert space
```

### Continuous linear maps
```lean
E →L[ℝ] F                    -- bounded linear map
‖f‖                           -- operator norm
ContinuousLinearMap.opNorm_le_bound  -- bound the norm
```

## Key Imports
```lean
import Mathlib.LinearAlgebra.Basic
import Mathlib.LinearAlgebra.Basis
import Mathlib.LinearAlgebra.Dimension.Finrank
import Mathlib.LinearAlgebra.Matrix.ToLin
import Mathlib.LinearAlgebra.Matrix.Determinant
import Mathlib.LinearAlgebra.Matrix.NonsingularInverse
import Mathlib.LinearAlgebra.Eigenspace.Basic
import Mathlib.LinearAlgebra.TensorProduct.Basic
import Mathlib.Analysis.InnerProductSpace.Basic
import Mathlib.Analysis.NormedSpace.Basic
```
