# Typography Tokens

## Responsibility

This document defines how typography is modeled and governed within the design system.

Typography tokens establish a **clear information hierarchy**, ensure readability across devices, and prevent inconsistent text styling across teams.

The purpose of this layer is not aesthetic expression. It is structured communication.

---

## Problem at scale

Typography inconsistencies appear quickly in growing products:

* Multiple font sizes for the same semantic role
* Arbitrary line-heights
* Overuse of bold or large text to compensate for poor hierarchy
* Accessibility regressions due to small text or insufficient contrast

Without a controlled system, typography becomes subjective and difficult to refactor.

Typography tokens exist to make hierarchy predictable and durable.

---

## Semantic hierarchy model

Typography tokens describe **role**, not visual size.

Consumers should not ask:

> "Should this be 18px or 20px?"

They should ask:

> "Is this a heading, body text, caption, or label?"

### Discouraged

```ts
fontSize: 18
fontWeight: 600
lineHeight: 1.3
```

### Preferred

```ts
text.heading.lg
text.body.md
text.caption.sm
```

This ensures consistent hierarchy and allows global refinements without modifying component code.

---

## Token structure

Typography tokens are organized by semantic role first, scale second.

Conceptual structure:

```ts
text
 ├── heading
 │   ├── xl
 │   ├── lg
 │   └── md
 ├── body
 │   ├── lg
 │   ├── md
 │   └── sm
 ├── label
 │   └── md
 └── caption
     └── sm
```

Rules:

* The number of roles is intentionally limited
* Each role has a clear use case
* Size variants are constrained to prevent hierarchy inflation

A small, disciplined type scale creates stronger visual clarity than an expansive one.

---

## Readability principles

Typography tokens are designed with readability as the default outcome.

Guidelines:

* Body text must maintain comfortable line length and spacing
* Line-height is defined alongside font size, not independently
* Text size should adapt responsibly across viewports

Consumers should not manually override line-height or letter-spacing unless addressing a documented exception.

---

## Accessibility considerations

Typography tokens must:

* Meet minimum readable size standards
* Avoid relying solely on weight or color to convey emphasis
* Work correctly with user-adjusted browser font settings

The system should remain usable at increased zoom levels and support users who override default font sizes.

---

## Responsive behavior

Typography tokens may resolve differently across breakpoints while maintaining semantic meaning.

Example (conceptual):

```ts
text.heading.lg → mobile: 20px, desktop: 24px
```

Consumers continue referencing `text.heading.lg` without concern for viewport differences.

Responsiveness is handled centrally.

---

## What typography tokens do NOT do

Typography tokens do not:

* Encode layout spacing
* Represent marketing-specific display styles
* Allow arbitrary scaling outside the defined system

If a text style is used only once and lacks clear semantic purpose, it does not belong in the token layer.

---

## Change strategy

Typography changes are highly visible and must be approached cautiously.

Guidelines:

* Prefer adjusting underlying scale values over introducing new roles
* Avoid expanding the hierarchy unnecessarily
* Test global typography changes across representative screens

Typography evolution should increase clarity, not complexity.

---

## Failure modes

Even with tokens, typography systems can degrade if:

* Teams bypass semantic roles for visual tweaks
* New roles are introduced without governance
* Heading levels are misused for styling instead of document structure

Regular audits and documentation reviews are necessary to maintain consistency.

---

## Guiding principle

> Typography should communicate structure before it communicates style.

If the hierarchy is unclear, increasing font size will not fix the problem.
