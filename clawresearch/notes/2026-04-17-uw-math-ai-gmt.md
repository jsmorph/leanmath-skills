# UW Math AI Lab and FormalizingGMT

Why this warrants deeper analysis:

- It is not just one repo. The UW Math AI Lab org page acts as a public map of active Lean projects, and several are in target domains: random graphs, central limit theorem, geometric measure theory, and point-set topology.
- `FormalizingGMT` looks especially strong for leanmath-skills because it is explicit about project decomposition: upstream mathlib-ready lemmas first, then Falconer / Evans GMT results on top.
- The repo also links concrete mathlib PRs, which is useful for tracing what actually made it upstream and what naming / API choices mathlib settled on.
- The org's `math-ai-docs` repo contains practical workflow advice that lines up with likely skill-authoring needs: theorem search before proving, shared-repo discipline, staged upstreaming, and lightweight project management.

Likely follow-up work:

1. Inspect `FormalizingGMT` more closely for file layout, theorem names, and reusable measure-theory / topology conventions.
2. Check whether `central_limit_theorem` and `random_graphs` have enough substance yet to mine proof patterns or API usage.
3. Extract the best workflow guidance from `math-ai-docs` into future theorem-discovery / project-workflow notes.
4. Cross-check linked mathlib PRs to see which abstractions already landed upstream.
