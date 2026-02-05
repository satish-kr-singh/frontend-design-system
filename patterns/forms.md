# Form Patterns

## Responsibility

This document defines how form controls should be composed using primitives.

The goal is to standardize structure, validation display, accessibility relationships, and error handling without introducing rigid composite components.

Forms are patterns, not primitives.

---

## Core Principles

### 1. Composition over abstraction

Forms should be composed from primitives (`Input`, `Label`, `Button`) rather than wrapped in monolithic “FormField” components.

Composition preserves flexibility and reduces hidden complexity.

---

### 2. Explicit label association

Every input must be associated with a visible label.

Correct pattern:

```tsx
<label htmlFor="email">Email</label>
<Input id="email" />
