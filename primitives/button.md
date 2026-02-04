# Button Primitive

## Responsibility

The Button primitive provides a semantic and accessible wrapper around the native `<button>` element.

It applies design tokens for visual consistency while preserving native browser behavior.

Its purpose is to standardize interaction patterns without introducing business logic or workflow assumptions.

---

## Design Constraints

The Button primitive:

- Wraps the native `<button>` element
- Applies semantic color and spacing tokens
- Supports a limited set of visual variants
- Preserves native accessibility and keyboard behavior

It does not:

- Manage loading state
- Trigger side effects
- Handle navigation logic
- Encode domain-specific meaning

---

## API Surface

The API is intentionally minimal.

Conceptual example:

```tsx
type ButtonProps = {
  variant?: "primary" | "secondary" | "danger"
  size?: "sm" | "md" | "lg"
} & React.ButtonHTMLAttributes<HTMLButtonElement>
