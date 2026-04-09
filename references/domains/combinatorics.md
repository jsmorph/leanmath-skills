# Domain: Combinatorics in Mathlib

> **Sources:** Mathlib API docs; Tao's proof tour (Finset/BigOperators walkthrough);
> Mathlib overview. **Extended:** cameronfreer `domain-patterns.md` (number theory
> and combinatorics section). See `references/SOURCES.md`.

## Setup

```lean
open Finset BigOperators  -- essential for ∑ and ∏ notation
```

## Core Types for Finite Objects

### `Finset α` — finite sets (the workhorse)
A `Finset α` is a finite subset of `α`, implemented as a duplicate-free `Multiset`.
This is the primary type for combinatorics in Mathlib.

```lean
-- Construction
Finset.range n           -- {0, 1, ..., n-1}
Finset.Icc a b           -- {a, a+1, ..., b} (for ordered types)
Finset.filter p s        -- {x ∈ s | p x}
Finset.image f s         -- {f x | x ∈ s}
Finset.univ              -- all elements (requires [Fintype α])
{a, b, c}               -- literal finite set (requires [DecidableEq α])
s ∪ t, s ∩ t, s \ t     -- set operations
s ×ˢ t                   -- Cartesian product
s.powerset               -- power set
```

### `Fintype α` — types with finitely many elements
```lean
variable [Fintype α]     -- α has finitely many elements
Fintype.card α           -- |α|
Finset.univ : Finset α   -- the universal finset
```

### `Set α` with `Set.Finite`
Sometimes you work with `Set α` and prove finiteness separately.
```lean
variable (s : Set α) (hs : s.Finite)
hs.toFinset  -- convert to Finset
```

### `Multiset α` — finite multisets (bags)
Like `Finset` but allows duplicates. Rarely used directly in combinatorics.

## Big Operators (∑ and ∏)

### Notation (requires `open BigOperators`)
```lean
∑ x ∈ s, f x              -- sum over Finset s
∏ x ∈ s, f x              -- product over Finset s
∑ x, f x                  -- sum over all x (requires Fintype)
∏ x, f x                  -- product over all x (requires Fintype)
∑ x ∈ s with p x, f x     -- sum with filter
∑ ⟨x, y⟩ ∈ s ×ˢ t, f x y -- sum over product
```

Without `open BigOperators`, you must write `Finset.sum s f` (ugly).

### Essential sum/product lemmas

```lean
-- Splitting and combining
Finset.sum_union_inter           -- sum over union + intersection
Finset.sum_filter                -- sum with predicate filter
Finset.sum_bUnion                -- sum over disjoint union
Finset.sum_product               -- ∑ in s ×ˢ t = ∑ in s, ∑ in t
Finset.sum_comm                  -- swap summation order

-- Comparing sums
Finset.sum_le_sum                -- pointwise ≤ → sum ≤
Finset.sum_nonneg                -- pointwise ≥ 0 → sum ≥ 0
Finset.sum_pos                   -- pointwise > 0, nonempty → sum > 0

-- Special values
Finset.sum_const                 -- ∑ x ∈ s, c = |s| • c
Finset.sum_const_nat             -- for natural number sums
Finset.card_eq_sum_ones          -- |s| = ∑ x ∈ s, 1

-- Telescoping
Finset.sum_range_sub             -- ∑ i in range n, (f (i+1) - f i) = f n - f 0

-- Manipulation
Finset.sum_congr                 -- change f under equal finsets
Finset.sum_bij                   -- reindex via bijection
Finset.sum_nbij                  -- reindex without surjectivity proof
Finset.sum_ite                   -- split by condition
```

### Tactic tips for sums
- `simp` often handles simple sum identities (`sum_const`, `sum_range_succ`, etc.)
- `ring` works inside sum arguments after `simp_rw`
- `gcongr` works for sum inequalities: `∑ f ≤ ∑ g` from `∀ x, f x ≤ g x`
- `omega` for goals about `Finset.card` or `Finset.range`

## Cardinality

```lean
Finset.card s            -- |s| : ℕ
Fintype.card α           -- |α| for finite types

-- Key lemmas
Finset.card_union_add_card_inter   -- |A ∪ B| + |A ∩ B| = |A| + |B|
Finset.card_sdiff_add_card_inter   -- |A \ B| + |A ∩ B| = |A|
Finset.card_le_card                -- s ⊆ t → |s| ≤ |t|
Finset.card_image_of_injective     -- injective f → |f '' s| = |s|
Finset.card_filter_le_card         -- |{x ∈ s | p x}| ≤ |s|
Finset.card_range                  -- |range n| = n
Finset.card_product                -- |s ×ˢ t| = |s| * |t|
Finset.card_powerset               -- |s.powerset| = 2^|s|
```

## Counting and Enumeration

### Binomial coefficients
```lean
Nat.choose n k           -- C(n, k)
Nat.choose_symm_diff     -- C(n, k) = C(n, n-k)
Nat.add_choose_le        -- C(m+n, k) ≤ ...
Nat.choose_succ_succ     -- Pascal's rule
```

### Factorials and permutations
```lean
Nat.factorial n
Nat.ascFactorial n k     -- n * (n+1) * ... * (n+k-1)
Nat.descFactorial n k    -- n * (n-1) * ... * (n-k+1)
```

### Embeddings and equivalences (for counting injections/bijections)
```lean
Fintype.card_embedding   -- number of injections
Fintype.card_equiv       -- number of bijections
```

## Graph Theory

Graphs in Mathlib use `SimpleGraph V`:
```lean
variable (G : SimpleGraph V) [Fintype V] [DecidableRel G.Adj]

G.Adj u v                  -- u and v are adjacent
G.edgeFinset               -- set of edges
G.degree v                 -- degree of vertex v
SimpleGraph.Subgraph G     -- subgraphs
```

Key results available: degree-sum formula, Turán's theorem, Szemerédi regularity lemma,
triangle counting/removal lemmas.

## Set Families / Extremal Combinatorics

Mathlib has formalized:
- Sperner's theorem, LYM inequality
- Harris-Kleitman inequality
- Kruskal-Katona theorem
- Sauer-Shelah lemma (VC dimension)
- Four functions theorem

Located under `Mathlib.Combinatorics.SetFamily.*`.

## Additive Combinatorics

Rich library from the PFR project and related work:
- Ruzsa covering lemma, triangle inequality
- Plünnecke-Petridis inequality
- Freiman homomorphisms
- Doubling constant
- Shannon entropy lemmas

Located under `Mathlib.Combinatorics.Additive.*`.

## Common Proof Patterns

### Double counting
```lean
-- ∑ x ∈ s, f x = ∑ y ∈ t, g y
-- Prove by reindexing or Fubini-like argument
Finset.sum_comm  -- swap order of nested sums
Finset.sum_bij   -- reindex one sum to match the other
```

### Pigeonhole
```lean
Finset.exists_lt_card_fiber_of_nsmul_lt_card  -- generalized pigeonhole
Finset.exists_ne_map_eq_of_card_lt            -- simple pigeonhole
```

### Induction on Finsets
```lean
-- Induction on |s|
induction s using Finset.induction with
| empty => ...
| insert ha ih => ...

-- Strong induction on cardinality
Finset.strongInduction
```

### Inclusion-exclusion
```lean
-- Available through Finset.sum_powerset_insert and related
-- Also: Finset.sum_card_inter for counting version
```

## `Decidable` Instances

Combinatorics often requires decidable equality and membership:
```lean
variable [DecidableEq α]  -- for Finset.insert, Finset.erase, etc.
variable [Fintype α]       -- for Finset.univ, Fintype.card
```

If you get "failed to synthesize Decidable" errors, add the appropriate instance.
For `Prop`-valued predicates, you may need `[DecidablePred p]`.

## `Nat` Subtraction Gotcha

Natural number subtraction truncates: `3 - 5 = 0` in `ℕ`. This causes constant
friction in combinatorics. Strategies:
- Work in `ℤ` and cast back: `push_cast; ring; omega`
- Use `Nat.sub_add_cancel` with side condition `h : b ≤ a`
- Use `omega` which understands truncated subtraction
- Use `tsub_add_cancel_of_le` (general truncated subtraction)

## Key Imports
```lean
import Mathlib.Data.Finset.Basic
import Mathlib.Data.Finset.Card
import Mathlib.Data.Finset.Lattice
import Mathlib.Data.Finset.Powerset
import Mathlib.Data.Fintype.Basic
import Mathlib.Algebra.BigOperators.Group.Finset
import Mathlib.Algebra.BigOperators.Order
import Mathlib.Combinatorics.SimpleGraph.Basic
import Mathlib.Combinatorics.SimpleGraph.DegreeSum
import Mathlib.Data.Nat.Choose.Basic
import Mathlib.Tactic.Ring
import Mathlib.Tactic.Linarith
import Mathlib.Tactic.GCongr
```
