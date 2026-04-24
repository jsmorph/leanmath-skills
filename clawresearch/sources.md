# leanmath monitoring sources

## High-value recurring sources

1. Lean community blog: https://leanprover-community.github.io/blog/
2. Lean community blog RSS: https://leanprover-community.github.io/blog/rss.xml
3. New in mathlib category: https://leanprover-community.github.io/blog/categories/cat_new-in-mathlib/
4. Month in Mathlib category page: https://leanprover-community.github.io/blog/categories/cat_month-in-mathlib/
5. arXiv for substantial formalization papers
6. GitHub repos/tools when they change workflow or reveal reusable infrastructure
7. Zulip/forum threads only when directly discoverable and clearly high-signal
8. Lean events page: https://leanprover-community.github.io/events.html
9. Event/workshop pages surfaced from the Lean events page when they are domain-specific enough to imply slides, notes, recordings, or participant repos
10. ICERM analysis workshop page: https://icerm.brown.edu/program/topical_workshop/tw-26-ttfa
11. Bridging Lean and the LMFDB workshop page: https://multramate.github.io/lean-lmfdb/
12. UW Math AI Lab org: https://github.com/uw-math-ai
13. UW Math AI Lab project/process docs: https://github.com/uw-math-ai/math-ai-docs
14. Lean Together 2026 event page / recordings hub: https://leanprover-community.github.io/lt2026/
15. Lean community courses index data: https://raw.githubusercontent.com/leanprover-community/leanprover-community.github.io/lean4/data/courses.yaml
16. Undergraduate mathematics in mathlib coverage map: https://leanprover-community.github.io/undergrad.html

## Current monitoring stance

- Highest signal: Lean community blog, especially practical posts and recurring domain summaries.
- Best domain-scouting source: `Month in Mathlib` posts.
- Recency is a first-class filter for both Lean and mathlib guidance.
- Prefer recent Lean 4 and current-mathlib material by default.
- Treat Lean 3 / early-transition / older mathlib guidance as suspect unless still verified useful.
- Best paper filter: only keep papers that expose reusable proof patterns, domain architecture, or substantial formalization scope.
- Public Zulip discovery through broad web search is currently low-yield and noisy.
- Maintenance/workflow artifacts are in scope when they would improve `leanmath-skills` usability.
- The Lean events page is worth occasional checks because workshop pages often surface slide decks, recorded talks, and follow-up reports before they appear as blog posts.
- In particular, domain-focused entries like ICERM's `Techniques and Tools for the Formalization of Analysis` workshop are good future source leads for analysis-specific talks, repos, and notes.
- Also watch event pages for `Bridging Lean and the LMFDB` and similar tutorial-heavy workshops, since they can surface practical API-navigation material in number theory before it appears in blog posts or papers.
- The UW Math AI Lab GitHub org is now worth occasional checks because it acts as a public index of active student-led Lean projects with concrete repo links in probability, combinatorics, topology, and analysis-adjacent areas.
- The UW Math AI Lab docs repo is also worth occasional checks because it contains practical formalization workflow guidance, search-tool recommendations, and upstream-to-mathlib process notes that may be more directly reusable than many papers.
- The Lean Together 2026 page is now worth occasional checks because it links to current recorded talks, which often surface practical mathlib workflow, maintenance, and project-report material earlier than the blog does.
- The Lean community `courses.yaml` data file is also worth occasional checks because it exposes current university teaching repos and course materials, which can turn out to be better skill-authoring inputs than papers when they cover analysis, topology, or combinatorics with explicit exercises and chapter structure.
- The `undergrad.html` coverage map is also worth occasional checks because it gives a domain-organized view of what mathlib already covers, which is useful for skill notes about theorem discovery, topic scouting, and deciding whether a project should build new infrastructure or start by searching existing declarations.

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

### Analysis / PDE
- `site:arxiv.org Lean 4 formalization analysis`
- `site:arxiv.org Lean 4 elliptic PDE formalization`
- `site:arxiv.org De Giorgi Nash Moser Lean`

### Combinatorics
- `site:leanprover-community.github.io/blog combinatorics mathlib Lean`
- `site:leanprover-community.github.io/blog Roth theorem Lean mathlib`
- `site:arxiv.org Lean 4 combinatorics formalization`
- `site:github.com leanprover-community mathlib combinatorics`

### Topology
- `site:github.com "Topology in Lean" Lean 4 Mathlib`
- `site:github.com "point-set topology" Lean mathlib repo`
- `site:leanprover-community.github.io/blog topology mathlib Lean`

### Workflow / maintenance / discovery
- `site:leanprover-community.github.io/blog mathlib changelog Lean`
- `site:leanprover-community.github.io/blog searching for theorems in mathlib`
- `site:github.com mathlib changelog Lean`
- `site:github.com lean-lsp Lean tool mathlib`
- `site:github.io Lean workshop slides mathlib analysis probability`
- `site:leanprover-community.github.io/events Lean workshop formalization analysis`

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
- is recent enough to plausibly match current Lean 4 / mathlib usage
- exposes a major new formalization area
- points to datasets, tools, or automation relevant to Lean work
- would likely change or expand a skill doc

Mark *medium* when the item:
- is a useful example or case study
- may inform future coverage
- is somewhat older but still looks directionally useful
- mainly serves as a lead to deeper sources

Mark *low* when the item:
- is interesting but redundant
- is speculative or thin on implementation detail
- is only tangentially about Lean/mathlib practice
- is old enough that guidance may be stale unless revalidated

## Review buckets

When revisiting existing links, classify each as one of:
- `escalate` — recent/current and likely worth deeper analysis soon
- `keep` — useful to retain, but not urgent
- `deprecate` — keep only as historical background or a topic lead; not guidance
- `drop` — remove if it is too stale, noisy, or off-target
