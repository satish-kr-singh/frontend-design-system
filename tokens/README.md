# Design Tokens

## Responsibility

This folder defines the **foundational design contracts** for the entire frontend system.

Design tokens represent *intent*, not implementation. They encode decisions about color, spacing, typography, motion, and elevation in a way that is:

* Stable across products
* Shareable across teams
* Decoupled from specific UI components

Everything else in the design system depends on tokens. If tokens are unstable or poorly defined, the entire system becomes brittle.

---

## Why tokens exist

At scale, hard-coded values fail for predictable reasons:

* Visual inconsistency across teams
* Inaccessible color and contrast choices
* Expensive brand or theme changes
* Uncontrolled divergence in spacing and typography

Tokens solve this by creating a **single source of truth** for visual decisions.

Instead of asking *"What color should I use?"*, teams ask *"What intent am I expressing?"*

---

## Semantic over literal

Tokens in this system are **semantic**, not literal.

Literal tokens describe values:

* `blue-500`
* `16px`
* `#ff0000`

Semantic tokens describe purpose:

* `color.primary`
* `color.text.muted`
* `spacing.sm`

Semantic tokens allow the system to evolve without forcing consumers to change code.

Example (conceptual):

```ts
// ❌ discouraged
color: '#1e40af'

// ✅ preferred
color: token.color.primary
```

The underlying value may change. The intent should not.

---

## Token categories

This system defines the following token categories:

* **Color** — text, background, border, semantic feedback
* **Spacing** — margin, padding, layout rhythm
* **Typography** — font families, sizes, weights, line heights
* **Motion** — duration, easing, reduced-motion support
* **Elevation** — shadows and layering semantics

Each category is documented independently to limit blast radius and keep responsibilities clear.

---

## Accessibility as a contract

Accessibility is not an afterthought at the token layer.

Color tokens are designed to:

* Meet contrast requirements by default
* Avoid exposing raw color values to consumers
* Support high-contrast and reduced-vision themes

Motion tokens are designed to:

* Respect reduced-motion preferences
* Centralize animation timing decisions

By enforcing accessibility at the token layer, primitives and patterns inherit these guarantees automatically.

---

## Platform-agnostic by design

Tokens are defined independently of any rendering technology.

They may be consumed by:

* Web applications
* Native applications
* Documentation tools
* Design tooling

The representation (CSS variables, JSON, TypeScript) is an implementation detail. The contract is the token name and its meaning.

---

## Change strategy

Tokens are expected to evolve, but carefully.

Rules:

* **Additive changes** are preferred
* Renaming tokens is avoided
* Deleting tokens requires a migration plan

If a token’s meaning changes, it must be treated as a breaking change even if the name remains the same.

---

## What this layer does NOT do

The token layer does not:

* Encode component-specific decisions
* Contain layout or behavior logic
* Expose raw values for ad-hoc usage

Those concerns belong to primitives and consuming applications.

---

## How to use tokens

Consumers should:

* Reference tokens by semantic name
* Avoid re-exporting or aliasing tokens locally
* Treat tokens as read-only inputs

Tokens should feel boring and predictable. That is a feature, not a limitation.

---

## How this layer evolves

Changes to tokens should be proposed via a documented decision (ADR) explaining:

* The problem being solved
* Why existing tokens are insufficient
* Impact on accessibility and theming
* Backward compatibility considerations

This process is intentionally slower than feature development to protect system integrity.

---

## Guiding principle

> Tokens are promises.
> Breaking them breaks trust.

The primary responsibility of this layer is to preserve that trust over time.
