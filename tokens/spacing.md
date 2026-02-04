# Spacing Tokens

## Responsibility

This document defines how spacing is modeled and governed within the design system.

Spacing tokens establish a **consistent spatial rhythm** across the UI by standardizing margins, padding, and layout gaps. Their purpose is to prevent visual drift, reduce arbitrary layout decisions, and make interfaces feel intentional rather than accidental.

---

## Problem at scale

In large frontend codebases, spacing issues surface quickly:

* Slightly different paddings for similar components
* Inconsistent vertical rhythm across screens
* Magic numbers scattered across layouts
* Difficult global adjustments to density or responsiveness

These problems compound as teams grow. Spacing tokens exist to remove guesswork and encode layout decisions centrally.

---

## Semantic spacing model

Spacing tokens are **semantic and scale-based**, not ad-hoc numeric values.

Consumers should never decide spacing by asking:

> “Is this 12px or 14px?”

They should ask:

> “Is this tight, regular, or loose spacing?”

### Discouraged

```ts
margin: 14
padding: '10px'
gap: 18
```

### Preferred

```ts
margin: token.spacing.sm
padding: token.spacing.md
gap: token.spacing.lg
```

This ensures consistency and allows global density changes without touching component code.

---

## Scale and hierarchy

Spacing tokens follow a deliberate, limited scale.

Conceptual structure:

```ts
spacing
 ├── xs
 ├── sm
 ├── md
 ├── lg
 ├── xl
```

Rules:

* The scale is small on purpose
* Tokens increase predictably
* Intermediate values are avoided

A constrained scale reduces visual noise and prevents overfitting layouts to one-off cases.

---

## Vertical rhythm

Vertical spacing has a greater impact on perceived quality than horizontal spacing.

Guidelines:

* Vertical spacing between sections should come from the same token category
* Headings and body content should follow predictable spacing rules
* Stacking components should rely on `gap` rather than individual margins where possible

Consistent vertical rhythm improves readability and scanning, especially in data-heavy interfaces.

---

## Responsive considerations

Spacing tokens may resolve to different values across breakpoints, but their **semantic meaning remains stable**.

Example (conceptual):

```ts
spacing.md → compact: 12px, regular: 16px
```

Consumers continue to use `spacing.md` regardless of viewport size. Responsiveness is handled centrally.

---

## What spacing tokens do NOT do

Spacing tokens do not:

* Encode layout structure (grid, flex, columns)
* Represent component-specific quirks
* Replace layout primitives or utilities

If a layout decision is unique to a single feature, it does not belong in the token layer.

---

## Change strategy

Spacing tokens change infrequently.

Guidelines:

* Avoid adding new scale steps unless absolutely necessary
* Prefer reusing existing tokens over creating new ones
* Global spacing changes must be tested across representative screens

Even small spacing changes can have large visual impact.

---

## Failure modes

Common failure patterns include:

* Teams bypassing tokens for pixel-perfect tweaks
* Over-expanding the scale to satisfy edge cases
* Mixing margin-based and gap-based spacing inconsistently

Governance and code review discipline are required to maintain consistency.

---

## Guiding principle

> Spacing should feel invisible.

If users notice spacing, it is usually because something is wrong.
