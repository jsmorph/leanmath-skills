# MAT740 Topology in Lean looks worth deeper analysis

Date: 2026-04-20
Link: https://github.com/MariusFurter/MAT740-Topology-in-Lean-HS25

## Why this stands out

This is not just a course shell.
It explicitly rebuilds point-set topology in Lean 4 while avoiding `Mathlib.Topology`.
That makes it a plausible source of topology-specific onboarding material, definition choices, and proof patterns that are otherwise hard to extract from polished mathlib files.

## Strong signals

- The README is explicit about the pedagogical constraint: use Mathlib, but not `Mathlib.Topology`.
- The repo is organized around definitions, background files, and exercises, which should make reusable examples easier to mine than in a paper or a large production repo.
- It looks well suited to extracting “how do I encode the basic objects from scratch?” guidance for topological spaces, continuity, and open-set arguments.

## Why this matters for skill authoring

Likely targets:

- topology onboarding notes
- translating textbook point-set topology into Lean definitions
- proof patterns for continuity and open-set reasoning
- guidance on when to lean on Mathlib abstractions versus rebuilding local foundations for understanding

## Suggested next pass

- Inspect the definitions and exercises folders for especially clean examples of `TopologicalSpace`, continuity, and induced constructions.
- Compare its local definitions with current mathlib APIs to see where it aligns cleanly and where it intentionally simplifies.
- Extract a shortlist of topology lemmas or notation patterns that would make good `leanmath-skills` notes.
