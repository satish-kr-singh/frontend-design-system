# Color Tokens

## Responsibility

This document defines how color is modeled, named, and governed within the design system.

Color tokens express **visual intent**, not raw color values. Their purpose is to ensure consistency, accessibility, and long-term flexibility across products and teams.

---

## Problem at scale

Color is one of the fastest-moving and most failure-prone aspects of frontend systems.

Common problems in large codebases:

* Inconsistent colors for the same intent (e.g., multiple “primary blues”)
* Accessibility regressions due to ad-hoc color usage
* Expensive rebranding and theme changes
* Tight coupling between components and visual appearance

These failures are rarely technical — they are *organizational*. Color tokens exist to prevent them.

---

## Semantic model

All color tokens in this system are **semantic**.

Tokens describe *why* a color is used, not *what* the color is.

Examples of semantic intent:

* Primary action
* Secondary text
* Destructive feedback
* Disabled surface

Non-semantic (literal) naming is intentionally avoided.

### Discouraged

```ts
blue500
redError
#1e40af
```

### Preferred

```ts
color.primary
color.text.default
color.feedback.error
```

This allows the underlying color values to change without requiring changes in consuming code.

---

## Token hierarchy

Color tokens are organized hierarchically to limit blast radius and clarify intent.

High-level structure (conceptual):

```ts
color
 ├── text
 │   ├── default
 │   ├── muted
 │   └── inverse
 ├── background
 │   ├── surface
 │   ├── elevated
 │   └── overlay
 ├── border
 │   ├── subtle
 │   └── strong
 └── feedback
     ├── success
     ├── warning
     └── error
```

Each branch answers a specific question:

* Is this text, background, or feedback?
* Is the usage semantic or contextual?

---

## Accessibility guarantees

Accessibility is enforced at the token level.

Rules:

* Text and background token pairs must meet contrast requirements by default
* Feedback colors must not rely on hue alone to convey meaning
* Tokens should support both light and dark themes without renaming

Consumers of the design system should not need to calculate contrast ratios manually. If a token exists, it is expected to be safe for its intended use.

---

## Theming and modes

Color tokens are designed to support:

* Light and dark modes
* Brand customization
* High-contrast or accessibility modes

Theme-specific values are applied **behind** the semantic token names.

Conceptually:

```ts
color.primary → theme.light.color.primary
color.primary → theme.dark.color.primary
```

Consumers never reference theme-specific values directly.

---

## What tokens do NOT encode

Color tokens do not:

* Encode component variants
* Express layout or spacing intent
* Represent one-off visual decisions

If a color is needed only for a single component or feature, it does not belong in the token layer.

---

## Change and evolution

Color tokens are highly sensitive and change slowly.

Guidelines:

* Adding new semantic tokens requires justification
* Changing a token’s meaning is treated as a breaking change
* Deprecated tokens must have a documented migration path

All changes should consider:

* Accessibility impact
* Theming implications
* Visual consistency across existing surfaces

---

## Failure modes to watch for

Even with tokens, systems can fail if:

* Teams bypass tokens with inline styles
* Token names become too granular
* Semantic meaning drifts over time

Regular audits and governance are required to preserve integrity.

---

## Guiding principle

> Color should communicate intent, not taste.

If a token does not clearly communicate intent, it does not belong in the system.
