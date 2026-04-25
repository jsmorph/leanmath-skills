# leanmath priority domains

Date: 2026-04-11

## Current conclusions

After two initial passes, the best recurring source appears to be the Lean community blog.
In particular, `Month in Mathlib` posts are strong for scouting domain-specific developments, while standalone blog posts are stronger for workflow and implementation detail.

Most importantly: recency is a first-class filter.
For both Lean and mathlib, recent Lean 4 / current-mathlib guidance should be preferred by default.
Older Lean 3, early-port, or otherwise old material should be treated as suspect unless revalidated.
It can remain useful as background, historical context, or a lead to deeper mining, but should not drive skill authoring without verification.

Public Zulip discovery via generic web search is currently weak: too much noise, poor indexing, and too few directly actionable technical threads.
That may still be worth revisiting later with topic-specific or person-specific searches, but it should not drive the daily monitor.

## Highest-priority domains

1. Probability
2. Measure theory
3. Combinatorics

These domains already produced useful artifacts in the first two passes:
- practical probability commentary
- measure-theory implementation notes
- recurring mathlib updates pointing to combinatorics and martingale/measure developments

## What should count as especially valuable

Favor items that provide one or more of the following:
- direct guidance on how concepts are encoded in Mathlib
- implementation or architecture details, not just announcements
- mature case studies of nontrivial formalizations
- reusable workflow advice for theorem search, navigation, maintenance, or version drift
- pointers to specific mathlib areas or PR clusters worth later mining

## Current best examples

- `Basic probability in Mathlib`
- `The Radon-Nikodym theorem in Lean`
- `Markov kernels in Mathlib’s probability library`
- `Formalization of Brownian motion in Lean`
- `Introducing Mathlib Changelog`
- selected `Month in Mathlib` posts for domain scouting

## Operational guidance for future passes

- Start with the Lean community blog.
- Check for new `Month in Mathlib` / `New in mathlib` material.
- Prefer recent Lean 4 and current-mathlib guidance over older material.
- When research suggests `leanmath-skills` edits, update iteratively in small passes rather than large rewrites.
- Treat publication date and current-mathlib alignment as first-pass ranking signals; older material must earn its place by offering something still not covered by newer sources.
- Use arXiv selectively, not as the primary feed.
- Treat maintenance/discovery tools as first-class if they would improve `leanmath-skills`.
- Add links only when they are genuinely informative; avoid filling the list with thin announcements.
- Periodically review existing links for `escalate`, `keep`, `deprecate`, or `drop` status as the ecosystem moves.
