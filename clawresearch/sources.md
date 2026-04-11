# leanmath monitoring sources

## High-value recurring sources

1. Lean community blog: https://leanprover-community.github.io/blog/
2. New in mathlib category: https://leanprover-community.github.io/blog/categories/cat_new-in-mathlib/
3. Month in Mathlib posts (browse via blog search/category pages)
4. arXiv for substantial formalization papers
5. GitHub repos/tools when they change workflow or reveal reusable infrastructure
6. Zulip/forum threads only when directly discoverable and clearly high-signal

## Current monitoring stance

- Highest signal: Lean community blog, especially practical posts and recurring domain summaries.
- Best domain-scouting source: `Month in Mathlib` posts.
- Best paper filter: only keep papers that expose reusable proof patterns, domain architecture, or substantial formalization scope.
- Public Zulip discovery through broad web search is currently low-yield and noisy.
- Maintenance/workflow artifacts are in scope when they would improve `leanmath-skills` usability.

## Priority domains

- Probability
- Measure theory
- Combinatorics
- Analysis
- Algebra / topology when material is especially strong

## Domain-specific query families

### Probability / measure theory
- `site:leanprover-community.github.io/blog probability mathlib Lean`
- `site:leanprover-community.github.io/blog measure theory mathlib Lean`
- `site:arxiv.org Lean 4 probability formalization`
- `site:arxiv.org Lean 4 measure theory formalization`
- `site:arxiv.org Lean Brownian motion Markov kernels`

### Combinatorics
- `site:leanprover-community.github.io/blog combinatorics mathlib Lean`
- `site:leanprover-community.github.io/blog Roth theorem Lean mathlib`
- `site:arxiv.org Lean 4 combinatorics formalization`
- `site:github.com leanprover-community mathlib combinatorics`

### Workflow / maintenance / discovery
- `site:leanprover-community.github.io/blog mathlib changelog Lean`
- `site:leanprover-community.github.io/blog searching for theorems in mathlib`
- `site:github.com mathlib changelog Lean`
- `site:github.com lean-lsp Lean tool mathlib`

## Lower-yield sources for now

- Broad `site:leanprover.zulipchat.com ...` searches unless searching for a known topic/person/resource
- Generic AI+Lean benchmark chatter unless it clearly produces reusable math workflow insights

## What to capture per link

- Title
- URL
- Date seen
- Source class
- One or two lines on why it matters
- Suggested target file(s) in `leanmath-skills`
- Whether further analysis is warranted

## Triage rubric

Mark *high* when the item:
- teaches a reusable workflow
- reflects current community best practice
- exposes a major new formalization area
- points to datasets, tools, or automation relevant to Lean work
- would likely change or expand a skill doc

Mark *medium* when the item:
- is a useful example or case study
- may inform future coverage
- mainly serves as a lead to deeper sources

Mark *low* when the item:
- is interesting but redundant
- is speculative or thin on implementation detail
- is only tangentially about Lean/mathlib practice
