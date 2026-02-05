# Form Patterns

## Responsibility

This document defines how form-related UI should be composed using design system primitives.

Forms are structured interaction flows. They are not primitives and should not be treated as reusable black-box components. The purpose of this pattern is to standardize structure, accessibility, validation handling, and state modeling while keeping orchestration in the application layer.

---

## Architectural Boundaries

The Form pattern:

* Composes primitives such as `Input`, `Label`, `Button`, and `Checkbox`
* Defines structural and accessibility rules
* Documents validation display strategy
* Standardizes layout rhythm and grouping

The Form pattern does not:

* Fetch or submit data
* Store business logic
* Encode API contracts
* Replace application state management

Forms coordinate UI. Applications control data.

---

## Structural Composition

### Label Association

Every form control must have a visible label.

Correct structure:

```tsx
<label htmlFor="email">Email</label>
<Input id="email" />
```

Alternative (wrapped):

```tsx
<label>
  Email
  <Input />
</label>
```

Placeholders must not replace labels.

---

### Field Grouping

Related fields must be grouped semantically.

```tsx
<fieldset>
  <legend>Shipping Address</legend>
  <Input id="street" />
  <Input id="city" />
</fieldset>
```

`fieldset` and `legend` improve accessibility and logical grouping.

---

## Validation Strategy

Validation should follow predictable timing rules.

Recommended approach:

* Validate on blur for field-level feedback
* Validate on submit for form-level errors
* Avoid validating on every keystroke unless required

Inconsistent timing creates cognitive friction.

---

## Error Display Pattern

Errors must be:

* Programmatically associated
* Visually consistent
* Positioned predictably

Example:

```tsx
<label htmlFor="email">Email</label>
<Input
  id="email"
  aria-invalid="true"
  aria-describedby="email-error"
/>
<span id="email-error">Invalid email address</span>
```

Error feedback must not rely solely on color.

---

## Form State Modeling

Forms typically manage:

* Field values
* Validation state
* Submission state
* Async status

State should be controlled at the application level.

Conceptual model:

```tsx
type FormState = {
  values: Record<string, string>
  errors: Record<string, string>
  isSubmitting: boolean
}
```

The design system should remain agnostic to form libraries.

---

## Submission Pattern

Submission behavior must be explicit.

```tsx
<form onSubmit={handleSubmit}>
  ...
  <Button type="submit" disabled={isSubmitting}>
    Submit
  </Button>
</form>
```

Loading indicators belong in composition, not in primitives.

---

## Layout Guidelines

* Use spacing tokens for vertical rhythm
* Prefer container-level spacing (`gap`) over per-field margins
* Align related fields logically
* Avoid overly dense layouts

Layout rules must remain consistent across products.

---

## Accessibility Requirements

Forms must:

* Be fully keyboard navigable
* Preserve visible focus indicators
* Associate error messages correctly
* Avoid color-only communication
* Support screen reader announcements for validation

Accessibility must be verified before release.

---

## Anti-Patterns

Avoid:

* Monolithic `FormField` abstractions that hide structure
* Embedding validation logic inside primitives
* Over-abstracting before patterns stabilize
* Inconsistent error placement across screens

Over-abstraction reduces flexibility and increases rigidity.

---

## Failure Modes

Common breakdowns include:

* Variant inflation inside inputs
* Divergent validation timing across teams
* Accessibility regressions during redesign
* Layout rules leaking into primitives

Complexity increases quickly when structure is not standardized.

---

## Guiding Principle

> Forms are structured user conversations. Structure must remain predictable and accessible.

Complex orchestration belongs to the application layer, not the design system.
