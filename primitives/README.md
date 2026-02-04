# Primitives

## Responsibility

This layer provides thin, accessible wrappers around native HTML elements.

Primitives are the bridge between design tokens and application code. They apply visual contracts while preserving semantic HTML and predictable behavior.

Their purpose is stability, not abstraction.

---

## Design Principles

### 1. Native-first

Primitives wrap native elements (`button`, `input`, `label`, etc.) and preserve their default semantics.

They should not replace native behavior unless strictly necessary.

---

### 2. Minimal API Surface

Each primitive exposes only what is required to:

- Apply tokens
- Enforce accessibility defaults
- Support common use cases

Additional convenience props increase complexity and are avoided.

---

### 3. No Business Logic

Primitives do not:

- Fetch data
- Manage domain state
- Encode workflow decisions
- Apply feature-specific styling

They are infrastructural, not feature components.

---

### 4. Accessibility by Default

Primitives enforce:

- Keyboard interaction
- Focus visibility
- Proper ARIA attributes where necessary
- Correct semantic roles

Consumers should not need to manually fix accessibility for common elements.

---

## Example (Conceptual)

```tsx
function Button({ variant = "primary", ...props }) {
  return (
    <button
      data-variant={variant}
      {...props}
    />
  );
}
