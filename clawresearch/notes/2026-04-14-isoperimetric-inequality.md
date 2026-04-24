# Formalizing the Classical Isoperimetric Inequality in the Two-Dimensional Case

- URL: https://arxiv.org/abs/2603.14663
- Date noted: 2026-04-14
- Category: paper
- Priority: high

## Why this looks worth deeper analysis

This is one of the better analysis-facing leads so far because it is not just a theorem announcement. The abstract already exposes the kind of friction that tends to matter for `leanmath-skills`.

In particular, it appears to include concrete work on:

- classical Fourier series infrastructure
- Parseval and orthogonality lemmas
- uniform convergence via the Weierstrass M-test
- term-by-term differentiation
- interchange of infinite sums and integrals
- coordinating incompatible indexing conventions inside Mathlib

That is exactly the sort of material that can turn into useful analysis notes instead of vague inspiration.

## Likely value for leanmath-skills

Potential downstream skill material:

- how current Mathlib expresses classical Fourier-series arguments
- reusable patterns for proving analytic inequalities from series expansions
- practical handling of interval normalization and reparametrization
- tactics for sum/integral interchange obligations
- common indexing and coercion pitfalls in real-analysis formalizations

## Suggested next pass

- Inspect the public repo mentioned in the abstract.
- Identify the main files for Fourier foundations, Parseval, Wirtinger, and the final isoperimetric argument.
- Record the exact Mathlib APIs and notation that recur.
- Capture any workaround patterns around summability, integrability, differentiability, and index shifts.
- Decide whether this should drive a dedicated analysis note in `leanmath-skills`.
