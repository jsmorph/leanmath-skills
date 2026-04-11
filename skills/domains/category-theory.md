# Domain: Category Theory in Mathlib

> **Sources:** Mathlib API docs; Mathlib category theory overview; Lean community blog.
> See [Sources and References](../SOURCES.md).

## Core Structures

### Categories
```lean
variable [Category C]           -- a category with Hom and composition
variable [Category.{v} C]       -- with explicit universe for morphisms

-- Morphisms
f : X ⟶ Y                       -- notation for CategoryStruct.Hom X Y (type: \hom or \-->)
f ≫ g                            -- composition (f then g, "diagrammatic order")
𝟙 X                              -- identity morphism (type: \b1)
```

**Critical convention:** Mathlib uses **diagrammatic order** for composition:
`f ≫ g` means "first `f`, then `g`" (so `f : X ⟶ Y`, `g : Y ⟶ Z`, `f ≫ g : X ⟶ Z`).
This is the opposite of the usual `g ∘ f` convention.

### Functors
```lean
F : C ⥤ D                       -- functor (type: \func)
F.obj X : D                     -- object map
F.map f : F.obj X ⟶ F.obj Y    -- morphism map

-- Identity and composition
𝟭 C : C ⥤ C                     -- identity functor
F ⋙ G : C ⥤ E                   -- functor composition (F then G)
```

### Natural transformations
```lean
α : F ⟶ G                       -- natural transformation (same notation as morphisms!)
α.app X : F.obj X ⟶ G.obj X    -- component at X
NatTrans.naturality α f          -- the naturality square commutes
```

### Equivalences and isomorphisms
```lean
C ≌ D                            -- equivalence of categories
X ≅ Y                            -- isomorphism (type: \~=)
Iso.hom : X ⟶ Y
Iso.inv : Y ⟶ X
```

## Key Automation: `aesop_cat`

The standard tactic for category theory. Closes goals about commutative diagrams,
functoriality, naturality, etc.:
```lean
example (f : X ⟶ Y) : 𝟙 X ≫ f = f := by aesop_cat
example (f : X ⟶ Y) (g : Y ⟶ Z) (h : Z ⟶ W) : f ≫ (g ≫ h) = (f ≫ g) ≫ h := by aesop_cat
```

Other useful tactics:
- `simp` with categorical simp lemmas (`Category.comp_id`, `Category.id_comp`, `Category.assoc`)
- `slice_lhs n m => rw [...]` / `slice_rhs n m => rw [...]` — rewrite inside a specific
  segment of a composition chain
- `ext` — for natural transformations (reduces to checking components)
- `reassoc` attribute / `reassoc_of%` — generate reassociated versions of equalities

## Limits and Colimits

```lean
-- Limits
HasLimit F                       -- the limit of diagram F exists
limit F                          -- the limit object
limit.π F j                      -- projection to j-th component
limit.lift F c                   -- universal property: cone → limit

-- Specific limits
HasTerminal C                    -- terminal object exists
terminal C : C                   -- the terminal object ⊤
HasBinaryProducts C              -- binary products exist
X ⨯ Y                           -- product (type: \x with subscript)
prod.fst : X ⨯ Y ⟶ X
prod.snd : X ⨯ Y ⟶ Y

HasEqualizers C
equalizer f g                    -- the equalizer

HasPullbacks C
pullback f g                     -- the pullback
```

Dually: `HasColimit`, `colimit`, `HasInitial`, `initial`, `HasBinaryCoproducts`,
`X ⨿ Y` (coproduct), `HasCoequalizers`, `HasPushouts`.

```lean
-- Preserving limits
PreservesLimitsOfShape J F       -- F preserves J-shaped limits
PreservesLimits F                -- F preserves all limits

-- Creating limits
CreatesLimits F                  -- F creates limits
ReflectsLimits F                 -- F reflects limits
```

## Adjunctions

```lean
F ⊣ G                            -- F is left adjoint to G
Adjunction.homEquiv adj X Y      -- Hom(FX, Y) ≃ Hom(X, GY)
adj.unit : 𝟭 C ⟶ F ⋙ G         -- unit natural transformation
adj.counit : G ⋙ F ⟶ 𝟭 D       -- counit
```

## Yoneda

```lean
yoneda : C ⥤ (Cᵒᵖ ⥤ Type v)   -- Yoneda embedding
yoneda.obj X                     -- representable presheaf Hom(-, X)
Yoneda.fullyFaithful             -- Yoneda is fully faithful
```

## Abelian Categories

```lean
variable [Abelian C]             -- C is an abelian category

-- Kernels and cokernels (always exist in abelian)
kernel f : C
cokernel f : C
kernel.ι f : kernel f ⟶ X       -- inclusion
cokernel.π f : Y ⟶ cokernel f   -- projection

-- Exact sequences
Exact f g                        -- f ≫ g = 0 and kernel g = image f

-- Homology
HomologicalComplex C (ComplexShape.down ℕ)  -- chain complex
```

## Concrete Categories

Mathlib provides "forgetful functor" patterns for concrete categories:

```lean
-- Category of types
Type v                           -- has Category instance

-- Category of groups
GroupCat                         -- bundled groups
GroupCat.of G                    -- make a bundled group from [Group G]

-- Category of rings
RingCat, CommRingCat

-- Category of topological spaces
TopCat

-- Category of modules
ModuleCat R
```

## Sheaves and Sites

```lean
GrothendieckTopology C           -- a Grothendieck topology on C
Sheaf J C                        -- category of sheaves
Presheaf C                       -- category of presheaves (Cᵒᵖ ⥤ Type)
```

## Monoidal Categories

```lean
MonoidalCategory C               -- category with tensor product
X ⊗ Y                           -- tensor product of objects
f ⊗ g                           -- tensor product of morphisms
𝟙_ C                            -- tensor unit
```

## Common Proof Patterns

### Commutative diagrams
```lean
-- Most diagram chasing is done by simp + aesop_cat
example (f : X ⟶ Y) (g : Y ⟶ Z) (h : X ⟶ Z) (w : f ≫ g = h) :
    f ≫ (g ≫ 𝟙 Z) = h := by
  simp [w]  -- or: aesop_cat
```

### Universal property arguments
```lean
-- Show two maps to a limit are equal
limit.hom_ext (fun j => ...)    -- suffices to check on each projection
```

### Naturality
```lean
-- Natural transformation equality
NatTrans.ext α β (h : ∀ X, α.app X = β.app X)
```

### The `reassoc` trick
```lean
-- If you have h : f ≫ g = h ≫ k, you often need
-- h ≫ g ≫ m = h ≫ k ≫ m. The reassoc attribute helps:
@[reassoc] theorem my_comm : f ≫ g = h ≫ k := ...
-- This also generates my_comm_assoc : f ≫ g ≫ m = h ≫ k ≫ m
```

## Key Imports
```lean
import Mathlib.CategoryTheory.Category.Basic
import Mathlib.CategoryTheory.Functor.Basic
import Mathlib.CategoryTheory.NatTrans
import Mathlib.CategoryTheory.Limits.Shapes.Products
import Mathlib.CategoryTheory.Limits.Shapes.Equalizers
import Mathlib.CategoryTheory.Limits.Shapes.Pullbacks
import Mathlib.CategoryTheory.Adjunction.Basic
import Mathlib.CategoryTheory.Yoneda
import Mathlib.CategoryTheory.Abelian.Basic
import Mathlib.CategoryTheory.Monoidal.Category
import Mathlib.CategoryTheory.Sites.Sheaf
```
