# teorth/analysis looks worth deeper analysis

Date: 2026-04-15
Link: https://github.com/teorth/analysis
Docs: https://teorth.github.io/analysis/

## Why this stands out

This is not just another formalization repo.
It is unusually explicit about the places where textbook mathematics and current Lean/Mathlib practice diverge.
That is exactly the kind of material that tends to become useful in `leanmath-skills`.

## Strong signals

- It documents concrete Mathlib-facing design tradeoffs instead of only presenting finished proofs.
- It explains why sequence indexing is shifted to start at `0` instead of `1`.
- It explains why partial textbook operations are often replaced by total functions with junk values.
- It explicitly describes a gradual transition from custom textbook definitions to Mathlib-native ones.
- It publishes generated docs, which makes declaration-level mining easier.

## Why this matters for skill authoring

Likely targets:

- analysis onboarding notes
- “translating textbook statements into Lean” guidance
- notation / indexing pitfalls
- when to keep custom local definitions versus when to align with Mathlib early
- cross-navigation between tutorial-style developments and Mathlib docs

## Suggested next pass

- Inspect the generated docs and file structure for especially reusable chapters.
- Extract a short list of recurring adaptation patterns, for example indexing changes, totalization, and compatibility shims.
- Check whether any sections already give especially clean examples for limits, sequences, continuity, or measure/probability-adjacent material.
