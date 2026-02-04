# Input Primitive

## Responsibility

The Input primitive provides a thin, accessible wrapper around the native `<input>` element.

It standardizes visual appearance using design tokens while preserving native semantics and browser behavior.

Its purpose is to ensure consistency and accessibility across form controls without embedding validation or domain logic.

---

## Design Constraints

The Input primitive:

- Wraps the native `<input>` element
- Applies typography, spacing, and color tokens
- Supports limited visual states
- Preserves native keyboard and screen reader behavior

It does not:

- Manage validation rules
- Store form state
- Format domain-specific values
- Handle submission workflows

---

## API Surface

The API extends native input attributes rather than redefining them.

Conceptual example:

```tsx
type InputProps = {
  variant?: "default" | "error"
  size?: "sm" | "md" | "lg"
} & React.InputHTMLAttributes<HTMLInputElement>
