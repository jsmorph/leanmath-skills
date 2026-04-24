# Math-to-Lean Phrasebook

> **Sources:** Adapted from cameronfreer/lean4-skills
> [lean-phrasebook.md](https://github.com/cameronfreer/lean4-skills/blob/main/plugins/lean4/skills/lean4/references/lean-phrasebook.md), which is
> itself inspired by [Terence Tao's Lean Phrasebook](https://docs.google.com/spreadsheets/d/1Gsn5al4hlpNc_xKoXdU6XGmMyLiX4q-LFesFVsMlANo/).
> For the full version with more examples, see cameronfreer's original.
> See [Sources and References](SOURCES.md) for full citations.

This reference translates mathematical proof language into Lean 4 tactic proofs.
Organized by the kind of reasoning step you want to express.

Because Lean 4 and Mathlib evolve quickly, prefer recent Lean 4 / current-Mathlib sources when choosing notation, APIs, and workflow patterns. Older Lean 3 or early-port material can still be useful as background, but should not drive authoring unless revalidated against current practice.

---

## Forward Reasoning (building from what you know)

| Math phrase | Lean |
|------------|------|
| "Observe that A holds because r" | `have h : A := by r` |
| "We claim A. [proof]" | `have h : A := by ...` |
| "X equals Y by definition" | `have : X = Y := rfl` |
| "From h, applying f gives B" | `have hB : B := f h` |
| "The claim follows from h" | `exact h` or `assumption` |
| "This follows by definition" | `rfl` |
| "Replace h with its consequence" | `replace h := f h` |
| "h is no longer needed" | `clear h` |

## Backward Reasoning (working from the goal)

| Math phrase | Lean |
|------------|------|
| "By lemma A, it suffices to show..." | `apply A` |
| "It suffices to show B" | `suffices h : B by ...` then prove B |
| "Later we'll prove A; assume it now" | `suffices h : A from ...` then prove A |
| "We need to show A'" | `show A'` |
| "By definition, the goal is A'" | `change A'` |
| "We reduce to a close variant" | `convert my_lemma using n` |

## Case Analysis

| Math phrase | Lean |
|------------|------|
| "h says A or B; split into cases" | `rcases h with hA \| hB` |
| "Either P or ¬P" | `by_cases h : P` |
| "We split into cases n = 0 and n = k+1" | `cases n with \| zero => ... \| succ k => ...` |
| "We induct on n" | `induction n with \| zero => ... \| succ n ih => ...` |

## Quantifiers

| Math phrase | Lean |
|------------|------|
| "Assume A holds" / "Let x ∈ X" | `intro hA` / `intro x hx` |
| "Take x = a [to prove ∃ x, P x]" | `use a` |
| "By h, ∃ x with P(x); call it x₀" | `obtain ⟨x₀, hx₀⟩ := h` |
| "Since h : ∀ x ∈ X, P x, apply to a" | `have := h a ha` or `specialize h a ha` |
| "Select a canonical element" | `let x := h.some` |

## Conjunction, Disjunction, Iff

| Math phrase | Lean |
|------------|------|
| "To prove A ∧ B, prove each" | `constructor` or `exact ⟨proof_A, proof_B⟩` |
| "From h : A ∧ B, extract both" | `obtain ⟨hA, hB⟩ := h` or `h.1`, `h.2` |
| "To prove A ∨ B, we show A" | `left` (or `right` for B) |
| "To prove A ↔ B, prove both directions" | `constructor` |
| "By h : A ↔ B, convert A to B" | `rw [h]` or `h.mp hA` |

## Contradiction and Contrapositive

| Math phrase | Lean |
|------------|------|
| "We seek a contradiction" | `exfalso` |
| "But h and ¬h contradict" | `contradiction` or `absurd h nh` |
| "Suppose for contradiction ¬A" | `by_contra nh` |
| "Taking contrapositives" | `contrapose!` |
| "Push negation inward" | `push_neg` or `push_neg at h` |

## Equational and Inequality Reasoning

| Math phrase | Lean |
|------------|------|
| "Rewrite using h : X = Y" | `rw [h]` (left→right) or `rw [← h]` (right→left) |
| "Rewrite h in a hypothesis" | `rw [h] at hyp` |
| "Rewrite under binders (∀, ∃, ∫)" | `simp_rw [h]` (NOT `rw`) |
| "Chain of equalities/inequalities" | `calc x = y := by ... ; _ ≤ z := by ...` |
| "Both sides differ by monotone f" | `gcongr` |
| "Transitivity: X ≤ Y from X ≤ Z, Z ≤ Y" | `exact h₁.trans h₂` or `calc` |
| "X = Y by ≤ and ≥" | `apply le_antisymm` |

## Set Theory

| Math phrase | Lean |
|------------|------|
| "x ∈ S ∩ T means x ∈ S and x ∈ T" | `rcases hx with ⟨hxS, hxT⟩` |
| "To show x ∈ S ∪ T, show x ∈ S" | `left; exact hxS` |
| "S ⊆ T means ∀ x ∈ S, x ∈ T" | `intro x hx` |
| "To show S = T, show mutual inclusion" | `ext x; constructor <;> intro h ...` |
| "The preimage of S under f" | `f ⁻¹' S` |
| "The image of S under f" | `f '' S` |

## Extensionality

| Math phrase | Lean |
|------------|------|
| "Two functions equal iff equal pointwise" | `ext x` |
| "Two sets equal iff same membership" | `ext x` |
| "Two linear maps equal iff equal on all inputs" | `ext x` |
| "Two morphisms equal iff ..." | `ext` (works for most bundled types) |

## Algebraic Reasoning

| Math phrase | Lean |
|------------|------|
| "By ring arithmetic" | `ring` |
| "Clear denominators, then ring" | `field_simp; ring` |
| "By group calculation" | `group` (multiplicative) or `abel` (additive) |
| "By linear arithmetic" | `linarith` or `omega` (for ℕ/ℤ) |
| "Obviously nonneg/positive" | `positivity` |
| "By numerical computation" | `norm_num` |

## Almost-Everywhere Reasoning (Measure Theory)

| Math phrase | Lean |
|------------|------|
| "P holds for all x" → "P holds a.e." | `ae_of_all μ h` |
| "Combine a.e. hypotheses pointwise" | `filter_upwards [h₁, h₂] with x hx₁ hx₂` |
| "a.e. equal functions have equal integrals" | `integral_congr_ae h` |
| "P holds a.e., so Q holds a.e." | `filter_upwards [hP] with x hx; exact ...` |

## Textbook-to-Mathlib Adaptation Patterns

Recent analysis-oriented repos make the same point repeatedly: the mathematically natural statement in a paper or textbook is often not the most workable Lean statement. Before forcing the paper's surface form, check whether Mathlib already prefers a nearby formulation.

### Common adaptation moves

| Textbook habit | Lean / Mathlib adaptation |
|---------------|---------------------------|
| Sequences indexed from `1` | Reindex to start at `0` when working with `Nat`, `Finset.range`, series APIs, or recursion patterns |
| Partial operations with side conditions | Prefer total functions plus explicit hypotheses or side lemmas |
| Paper-local definitions introduced early | Prefer Mathlib's existing definitions; prove equivalence if needed |
| One large theorem statement mirroring the paper | Break into helper lemmas that match existing Mathlib abstractions |
| Custom notation matching the paper | Use Mathlib notation unless custom notation removes substantial friction |

### Practical guidance

- If a textbook proof uses indexing that fights `Nat` recursion or `Finset.range`, rewrite the statement early instead of carrying shifts through every lemma.
- If a paper uses a partial operation, check whether Mathlib models it as a total function with junk values outside the intended domain. That style is often easier to compose with automation.
- If you start with a pedagogical local definition, decide explicitly whether it is temporary onboarding scaffolding or part of the long-term API.
- When a result feels awkward to state, search for the surrounding Mathlib definitions first. Often the real issue is not the proof but the formulation.

### Warning sign

If you find yourself repeatedly coercing between nearly identical definitions, rewriting index shifts by hand, or carrying avoidable domain side conditions, step back and restate the problem in a more Mathlib-native way.

## Goal Management

| Math phrase | Lean |
|------------|------|
| "The other goal first" | `swap` |
| "Apply same tactic to all goals" | `all_goals ...` or `<;> ...` |
| "This goal is trivial" | `trivial` or `simp` |
| "Skip this for now" | `sorry` (development only — never in finished code) |
| "Show what simp would do" | `simp?` → replace with `simp only [...]` |
| "What lemma closes this?" | `exact?` (development only) |
