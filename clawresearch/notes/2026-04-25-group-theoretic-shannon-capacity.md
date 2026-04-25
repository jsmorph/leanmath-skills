# GroupTheoreticShannonCapacity looks worth deeper analysis

Date: 2026-04-25
Link: https://github.com/jzuiddam/GroupTheoreticShannonCapacity
Paper: https://arxiv.org/abs/2506.14654

## Why this stands out

This is a strong repo-level artifact, not just a paper announcement.
The README exposes exactly the sort of structure that makes later extraction efficient:
main theorem names, corresponding Lean declarations, file sizes, dependency layering, and an interactive dependency graph.

That combination is unusually useful for `leanmath-skills`, because it supports both domain notes and workflow notes.

## Strong signals

- Clear mapping from paper theorems to Lean names such as `limit_cycles`, `limit_fraction_graphs`, and `subgroup_limit`.
- Substantial formalization spread across focused files rather than a single opaque blob.
- Concrete architecture around fraction graphs, cohomomorphism theory, lattice constructions, and matrix arguments.
- Interactive dependency graph published alongside the repo.
- The underlying paper is mathematically specific and nontrivial, not generic theorem-prover demonstration material.

## Why this matters for skill authoring

Likely targets:

- combinatorics-oriented notes on graph constructions and proof decomposition
- repo-reading guidance for large formalizations with published dependency graphs
- examples of how to package theorem statements and proofs cleanly at the top level
- downstream discovery notes for graph theory / extremal combinatorics / information-theoretic formalization in Lean

## Suggested next pass

- Read the dependency graph and identify the smallest reusable file cluster.
- Check whether `FractionGraphs.lean` and `Basic.lean` expose definitions or lemmas likely to transfer beyond this project.
- Note any naming or packaging conventions that make the development easier to navigate than average.
- Decide whether this should become a dedicated combinatorics case-study note in `leanmath-skills`.
