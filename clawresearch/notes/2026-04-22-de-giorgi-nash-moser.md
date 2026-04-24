# Formalization of De Giorgi--Nash--Moser Theory in Lean (arXiv:2604.05984)

Link: https://arxiv.org/abs/2604.05984  
Date added: 2026-04-22

## Why this merits deeper analysis

- It is a major, modern analysis formalization (elliptic PDE regularity), not a narrow lemma pack.
- The abstract indicates substantial new infrastructure in exactly the areas skill authors struggle with:
  - Sobolev spaces on bounded domains
  - weak solutions for elliptic equations
  - quantitative regularity estimates
- It is likely to contain reusable proof-architecture patterns for hard analysis:
  - how theorems are staged (local boundedness → weak Harnack → Moser Harnack → Hölder regularity)
  - how measure/integration and function-space APIs are composed in practice
  - where current mathlib abstractions create friction

## Candidate follow-up extraction targets for leanmath-skills

- Dependency map of key files/modules used by the formalization.
- Practical conventions for weak-solution definitions and coercions.
- Common proof patterns and helper lemmas for iterative regularity arguments.
- Any notation/API pitfalls that repeatedly force rewrites or local wrappers.

## Suggested placement in leanmath-skills

- Analysis/advanced case study note.
- Cross-links from measure-theory and functional-analysis workflow docs.
