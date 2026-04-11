# Tactics, Automation, and Proof Strategies

> **Sources:** Lean 4 Tactic Reference (lean-lang.org); Mathlib tactic list; Kevin Buzzard
> et al. "Simp" guide; Terence Tao's proof tours; Mathematics in Lean (Avigad & Massot).
> See [Sources and References](SOURCES.md) for full citations.

## Table of Contents

1. [Tactic Philosophy](#tactic-philosophy)
2. [Core Tactics Reference](#core-tactics-reference)
3. [Decision Procedures and Closers](#decision-procedures-and-closers)
4. [Domain-Specific Automation](#domain-specific-automation)
5. [Search Tactics](#search-tactics)
6. [Rewriting and Simplification](#rewriting-and-simplification)
7. [Structural Tactics](#structural-tactics)
8. [Proof Strategy Patterns](#proof-strategy-patterns)
9. [Performance and Compilation](#performance-and-compilation)
10. [Common Pitfalls](#common-pitfalls)

---

## Tactic Philosophy

### Development vs. production proofs

During development, use powerful search tactics freely:
```lean
-- Development: discover what works
example : goal := by
  simp        -- find simplifications
  exact?      -- find the closing lemma
```

For finished proofs, pin everything explicitly:
```lean
-- Production: fast, stable, maintainable
example : goal := by
  simp only [add_zero, mul_one]
  exact Nat.le_succ_of_le h
```

### Why this matters

- `simp` (bare) scans 40,000+ lemmas; `simp only [...]` scans a handful.
- Search tactics (`exact?`, `apply?`) are not meant for checked-in code.
- Mathlib CI rejects non-terminal `simp` calls without `only`.
- Compilation speed directly affects iteration speed on large projects.

---

## Core Tactics Reference

### Introduction and elimination

| Tactic | Purpose | Example |
|--------|---------|---------|
| `intro h` | Introduce hypothesis | `⊢ P → Q` becomes `h : P ⊢ Q` |
| `rintro ⟨h₁, h₂⟩` | Introduce with pattern matching | Destructures `∧`, `∃`, etc. |
| `obtain ⟨x, hx⟩ := h` | Destructure a term | Like `rcases` but for a specific term |
| `rcases h with ⟨a, b⟩ \| c` | Recursive case split | Handles nested `∨`, `∧`, `∃` |
| `constructor` | Split a goal into parts | `⊢ P ∧ Q` becomes two goals |
| `left` / `right` | Choose disjunct | `⊢ P ∨ Q` becomes `⊢ P` or `⊢ Q` |
| `use x` | Provide existential witness | `⊢ ∃ n, P n` becomes `⊢ P x` |
| `exact h` | Close goal with exact term | |
| `apply f` | Apply function to goal | Leaves subgoals for arguments |
| `have h : T := proof` | Introduce intermediate result | |
| `suffices h : T by tac` | Reduce goal via sufficiency | |
| `show T` | Change goal display | Must be definitionally equal |

### Rewriting

| Tactic | Purpose |
|--------|---------|
| `rw [h]` | Rewrite goal left-to-right using `h` |
| `rw [← h]` | Rewrite right-to-left |
| `rw [h] at hyp` | Rewrite in a hypothesis |
| `simp_rw [h]` | Rewrite under binders (unlike `rw`) |
| `conv => ...` | Targeted rewriting in specific subexpression |
| `change T` | Replace goal with definitionally equal term |

### Case analysis

| Tactic | Purpose |
|--------|---------|
| `by_cases h : P` | Classical case split on decidable `P` |
| `by_contra h` | Proof by contradiction |
| `push_neg` | Push negation inward |
| `contrapose` | Replace goal with contrapositive |
| `exfalso` | Change goal to `False` |
| `contradiction` | Close goal from contradictory hypotheses |
| `absurd h₁ h₂` | Close from `h₁ : P` and `h₂ : ¬P` |

### Induction

```lean
-- Standard induction
induction n with
| zero => ...
| succ n ih => ...

-- Strong induction (well-founded)
induction n using Nat.strong_rec_on with
| _ n ih => ...

-- Induction with generalization
induction n generalizing m with
| zero => ...
| succ n ih => ...
```

### Calculation proofs

```lean
calc a
    _ = b := by ...
    _ ≤ c := by ...
    _ < d := by ...
```

`calc` chains can mix `=`, `≤`, `<`, `↔`, and other transitive relations. The
`gcongr` tactic is particularly useful inside calc blocks for inequalities.

---

## Decision Procedures and Closers

These tactics solve goals completely or fail:

| Tactic | Domain | Import |
|--------|--------|--------|
| `ring` | Commutative (semi)ring equations | `Mathlib.Tactic.Ring` |
| `group` | Non-commutative group equations | `Mathlib.Tactic.Group` |
| `abel` | Abelian group equations | `Mathlib.Tactic.Abel` |
| `noncomm_ring` | Non-commutative ring equations | — |
| `field_simp` | Clear denominators in field expressions | `Mathlib.Tactic.FieldSimp` |
| `omega` | Linear arithmetic over `ℕ` and `ℤ` | core (no import needed) |
| `linarith` | Linear arithmetic over ordered fields | `Mathlib.Tactic.Linarith` |
| `nlinarith` | Nonlinear arithmetic (heuristic) | `Mathlib.Tactic.Linarith` |
| `polyrith` | Polynomial arithmetic (calls external) | `Mathlib.Tactic.Polyrith` |
| `norm_num` | Numerical normalization | core |
| `decide` | Decidable propositions (small instances) | core |
| `norm_cast` | Normalize casts/coercions | `Mathlib.Tactic.NormCast` |
| `push_cast` | Push casts toward leaves | `Mathlib.Tactic.NormCast` |
| `positivity` | Prove `0 < x` or `0 ≤ x` | `Mathlib.Tactic.Positivity` |
| `tauto` | Propositional tautologies | — |
| `aesop` | General-purpose automation | `Aesop` |
| `grind` | E-matching + congruence closure | core |

### Common combinations

```lean
-- Field equations: clear denominators, then ring
field_simp
ring

-- Inequalities with multiplication: positivity for signs, then linarith
have h₁ : 0 < a := by positivity
linarith

-- Cast-heavy goals: normalize casts, then use arithmetic
push_cast
ring

-- Nonlinear bounds: provide key intermediate inequality
have h : a ^ 2 ≥ 0 := sq_nonneg a
nlinarith
```

---

## Domain-Specific Automation

These tactics call specialized lemma databases:

| Tactic | Domain | What it does |
|--------|--------|-------------|
| `continuity` | Topology | Proves continuity goals | 
| `fun_prop` | Multiple | Proves function properties (continuous, measurable, differentiable) |
| `measurability` | Measure theory | Proves measurability goals |
| `gcongr` | Ordered structures | "Generalized congruence" for inequalities |
| `mono` | Monotonicity | Applies monotonicity lemmas |
| `bound_tac` | Analysis | Bound estimation (project-specific) |

### `fun_prop` — the universal function-property tactic

`fun_prop` is the recommended first attempt for proving that a function has a property
like continuity, measurability, or differentiability. It composes lemmas tagged with
`@[fun_prop]` automatically.

```lean
-- Proves continuity of a composed expression
example : Continuous (fun x : ℝ => Real.exp (x ^ 2 + 3 * x)) := by
  fun_prop
```

### `gcongr` — inequality congruence

Proves goals like `f a ≤ f b` from `a ≤ b` when `f` is monotone, or more complex
composed inequalities:

```lean
example (h₁ : a ≤ b) (h₂ : c ≤ d) : a + c ≤ b + d := by
  gcongr
```

Especially useful in `calc` blocks:
```lean
calc ∫ x, f x ∂μ
    _ ≤ ∫ x, g x ∂μ := by gcongr; exact hfg
    _ ≤ M * μ s := by ...
```

---

## Search Tactics

| Tactic | Purpose | Use when |
|--------|---------|---------|
| `exact?` | Find lemma closing goal | Goal looks like it should be one lemma |
| `apply?` | Find lemma matching goal head | Goal might need one more step |
| `rw?` | Find rewrite rule | You need to transform an expression |
| `simp?` | Report simp lemmas used | Converting `simp` to `simp only` |
| `hint` | Try multiple tactics | Completely stuck |

**Never leave search tactics in finished code.** They are development tools only.

---

## Rewriting and Simplification

### `simp` family

```lean
simp                          -- Full simp database (SLOW, fragile — avoid in production)
simp only [lemma1, lemma2]    -- Only specified lemmas (PREFERRED)
simp [extra_lemma]            -- Simp database + extra lemma
simp [-bad_lemma]             -- Simp database minus a lemma
simp_all                      -- Simplify goal and all hypotheses
simp at h                     -- Simplify a hypothesis
simp_rw [h]                   -- Rewrite under binders (simp + rw hybrid)
norm_num                      -- Normalize numerical expressions
ring_nf                       -- Ring normal form (without closing)
```

### When to use what

- **`rw`**: Targeted rewrite at a specific location. Does NOT go under binders.
- **`simp_rw`**: Like `rw` but works under `∀`, `∃`, `∫`, `∑`, etc.
- **`simp only [...]`**: Multiple rewrites in no particular order, with congruence.
- **`conv`**: Surgical rewriting in a specific subexpression.

### `conv` mode (for precise targeting)

```lean
-- Rewrite only the LHS of an equation
conv_lhs => rw [h]

-- Rewrite inside a lambda
conv => arg 2; ext x; rw [h x]

-- Navigate to specific argument
conv => lhs; arg 1; rw [h]
```

---

## Structural Tactics

### `ext` — extensionality
```lean
-- Prove f = g by proving f x = g x for all x
ext x
```

### `congr` / `gcongr` — congruence
```lean
-- Reduce f a = f b to a = b
congr 1

-- Reduce f a ≤ f b to a ≤ b (for monotone f)
gcongr
```

### `convert` — approximate matching
```lean
-- Like exact but generates subgoals for mismatches
convert my_lemma using 2
-- "using 2" controls depth of matching
```

### `calc` — calculational proofs
The standard pattern for inequality chains in analysis:
```lean
theorem bound : ‖f x‖ ≤ C := by
  calc ‖f x‖
      _ = ‖g x + h x‖ := by rw [decomposition]
      _ ≤ ‖g x‖ + ‖h x‖ := norm_add_le _ _
      _ ≤ C₁ + C₂ := by gcongr <;> [exact hg; exact hh]
      _ = C := by ring
```

---

## Proof Strategy Patterns

### Forward vs. backward reasoning

**Backward (goal-directed):** Start from the goal and work toward hypotheses.
```lean
-- "I need to show IsCompact (f '' s). What lemma gives me that?"
apply IsCompact.image
· exact hs     -- subgoal: IsCompact s
· exact hf     -- subgoal: Continuous f
```

**Forward (hypothesis-directed):** Start from what you know and derive new facts.
```lean
-- "I have hf : Continuous f and hs : IsCompact s. What can I derive?"
have h := hs.image hf   -- IsCompact (f '' s)
```

### The "have / suffices" pattern for complex proofs

```lean
theorem main_result : conclusion := by
  -- Reduce to key claims
  suffices key : KeyStatement by
    exact key.some_consequence
  -- Prove the key claim
  have step1 : Intermediate1 := by ...
  have step2 : Intermediate2 := by ...
  exact combine step1 step2
```

### Epsilon-delta and quantitative arguments

```lean
theorem continuous_at_of_bound (hf : ∀ ε > 0, ∃ δ > 0, ...) : ContinuousAt f a := by
  rw [Metric.continuousAt_iff]
  intro ε hε
  obtain ⟨δ, hδ_pos, hδ⟩ := hf ε hε
  exact ⟨δ, hδ_pos, fun x hx => hδ x hx⟩
```

### Measure theory patterns

```lean
-- "Almost everywhere" reasoning
filter_upwards [h₁, h₂] with x hx₁ hx₂
-- Introduces x and the pointwise hypotheses from ae filters

-- Integral inequalities via monotonicity
apply integral_mono_of_nonneg
· exact ae_of_all _ (fun x => ...)   -- nonnegativity
· exact hf_integrable                -- integrability
· filter_upwards with x              -- pointwise bound
  intro hx; exact ...
```

---

## Performance and Compilation

### Diagnosing slow proofs

```lean
set_option profiler true in
theorem slow_proof : ... := by
  ...
```

Look for:
- `simp` taking > 1 second → replace with `simp only [...]`
- Typeclass resolution taking long → provide instances explicitly
- Large term elaboration → break into smaller lemmas

### Making proofs faster

1. **`simp only` not `simp`**: Always.
2. **Avoid `simp` in non-terminal position** unless wrapped in `simp only`.
3. **Provide typeclass instances explicitly** when resolution is slow:
   ```lean
   -- Instead of relying on instance search:
   @my_lemma _ _ instFooBar x y
   ```
4. **Use `set_option maxHeartbeats 400000 in`** scoped to single declarations, not globally.
5. **Split large proofs** into helper lemmas. Each lemma compiles independently.
6. **Avoid `decide`** on large instances — it evaluates at kernel level and can be
   exponentially slow.

### `set_option` usage

```lean
-- Scoped to one declaration (GOOD)
set_option maxHeartbeats 400000 in
theorem big_proof : ... := by ...

-- Global (BAD — linter rejects this)
set_option maxHeartbeats 400000
```

---

## Common Pitfalls

### 1. "unknown identifier" for a tactic
**Cause:** Missing import.
```lean
import Mathlib.Tactic.Ring          -- ring, ring_nf
import Mathlib.Tactic.Linarith      -- linarith, nlinarith
import Mathlib.Tactic.FieldSimp     -- field_simp
import Mathlib.Tactic.Positivity    -- positivity
import Mathlib.Tactic.FunProp       -- fun_prop
import Mathlib.Tactic.Measurability -- measurability
import Mathlib.Tactic.GCongr       -- gcongr
import Mathlib.Tactic.NormNum       -- norm_num extensions
```

### 2. "typeclass instance not found"
**Cause:** Missing instance in context. Either add it as a hypothesis
(`[TopologicalSpace α]`) or provide it explicitly.

### 3. "simp made no progress"
**Cause:** The simp lemma's LHS doesn't match the goal's syntactic form.
Try `simp_rw` (works under binders) or `simp only [...]` with explicit lemmas.

### 4. "`rw` failed: did not find instance of the pattern"
**Cause:** `rw` matches only at the top level and does not go under binders.
Use `simp_rw` or `conv` for targeted rewriting under `∀`, `∃`, `∫`, etc.

### 5. Definitional equality surprises
`a ≥ b` is definitionally `b ≤ a`, but automation may not treat them identically.
Mathlib standardizes on `≤` and `<` — rewrite `≥`/`>` to `≤`/`<` early.

### 6. Universe issues
If you see "universe level mismatch," check that your type variables have consistent
universe annotations. Use `Type*` (universe-polymorphic) by default.

### 7. Coercion chains
Deep coercion chains (ℕ → ℤ → ℚ → ℝ → ℂ) can confuse the elaborator.
Use `push_cast` and `norm_cast` to normalize. Provide explicit casts when needed.
