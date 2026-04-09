# Project Architecture for Research Formalization

> **Sources:** Mathlib contributing documentation; Baanen et al., "Growing Mathlib"
> (2026); Massot's Blueprint tool; Tao's PFR experience; Mathematics in Lean
> (Avigad & Massot). For compilation debugging, see cameronfreer `compilation-errors.md`.
> For performance, see cameronfreer `performance-optimization.md`.

## Scoping

1. State the top-level theorems precisely before writing code.
2. Map the intermediate dependency chain.
3. Survey Mathlib coverage for every concept in the chain.
4. If targeting Mathlib, post your plan on Zulip early.
5. Choose the right generality: `CommMonoid` when possible, `Field` only when needed.

## Definition Engineering

- **Use Mathlib's definitions.** Prove equivalence if yours differs.
- **Typeclasses for structure:** `[CommRing R] [TopologicalSpace R] [TopologicalRing R]`
- **Bundled morphisms:** `R →+* S` (RingHom), not bare functions.
- **Prop-valued classes:** `[IsNoetherian R M]`, `Is*` prefix for nouns.
- **API lemmas immediately:** `@[simp]`, `@[ext]`, coercions, constructors.
- **Mark reducibility:** `@[reducible]` or `@[irreducible]` deliberately.
- **`autoImplicit false`** in lakefile to prevent free variables.

## File Organization

- One focused topic per file. ≤ 1500 lines (linter warns).
- Minimize imports. Each unused import slows compilation.
- File header: copyright, authors, `/-! ... -/` module docstring.
- Import order: Mathlib first, then project files. No blank lines between.

## The Blueprint Model

For projects with 20+ interconnected lemmas, use Patrick Massot's
[leanblueprint](https://github.com/leanprover-community/leanblueprint):
LaTeX proof sketches linked to Lean declarations, dependency graph, status tracking.
See Tao's PFR project for the model workflow.

## Mathlib Type Hierarchies

```
Algebra:     Monoid → Group → CommGroup
             Semiring → Ring → CommRing → Field
Topology:    TopologicalSpace → UniformSpace → MetricSpace
             T1Space → T2Space → CompactSpace
Analysis:    NormedAddCommGroup → NormedSpace → CompleteSpace (Banach)
             InnerProductSpace → CompleteSpace (Hilbert)
Morphisms:   OneHom → MonoidHom (→*) → RingHom (→+*) → AlgHom (→ₐ)
```

Use the weakest structure that suffices.

## Elaboration

- Profile slow proofs: `set_option profiler true in`
- `simp only [...]` not bare `simp`. Use `simp?` to discover.
- Scope heartbeats: `set_option maxHeartbeats 400000 in` (per declaration).
- Split large proofs into helper lemmas.
- Document elaboration workarounds in a shared markdown file.
- For deep typeclass debugging, see cameronfreer `instance-pollution.md`.

## Contributing to Mathlib

Follow https://leanprover-community.github.io/contribute/. Key points:
- Do not fork — use branches on the main repo.
- Naming, style, 100-char lines, docstrings, `#lint` clean.
- Human reviewer checks math, code quality, naming.
- Only the strongest approach to a topic is included.
- See also official `leanprover/skills` repo: `mathlib-pr`, `mathlib-review`.

## Cleanup Checklist

- [ ] Zero `sorry`s
- [ ] `#lint` clean
- [ ] Docstrings on all public definitions
- [ ] Module docstring on every file
- [ ] `simp only [...]` (no bare `simp`)
- [ ] No `exact?`/`apply?` in finished code
- [ ] Minimal imports
- [ ] ≤ 100 char lines, ≤ 1500 line files
- [ ] Mathlib naming conventions
- [ ] Scoped `set_option`
