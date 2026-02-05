# Data Table Patterns

## Responsibility

This document defines how tabular data should be structured, rendered, and managed using design system primitives.

The goal is to ensure:

* Accessibility
* Performance at scale
* Predictable interaction patterns
* Clear separation of concerns

Data tables are complex patterns, not primitives.

---

## Core Principles

### 1. Structure before styling

A table is fundamentally structured data.

Use semantic HTML whenever possible:

```tsx
<table>
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>John</td>
      <td>Active</td>
    </tr>
  </tbody>
</table>
```

Avoid replacing table semantics with generic div layouts unless virtualization demands it.

---

### 2. Accessibility First

Tables must:

* Use `<th>` for headers
* Include `scope="col"` or `scope="row"`
* Preserve logical reading order
* Maintain keyboard navigability

Sorting indicators must be programmatically associated:

```tsx
<th aria-sort="ascending">Name</th>
```

Accessibility is not optional at scale.

---

### 3. Separation of Concerns

The table pattern does not:

* Fetch data
* Manage server synchronization
* Implement business logic
* Encode product-specific workflows

Data orchestration belongs to the application layer.

The table renders structured data predictably.

---

## State Modeling

Tables typically require multiple state layers:

* Sorting
* Filtering
* Pagination
* Row selection
* Expansion

These states should be:

* Explicit
* Controlled via props
* Composable

Conceptual API:

```tsx
type TableProps<T> = {
  data: T[]
  columns: ColumnDefinition<T>[]
  sortState?: SortState
  onSortChange?: (state: SortState) => void
}
```

Avoid hidden internal state that limits flexibility.

---

## Performance Strategy

Large datasets require deliberate strategy.

### When data < 100 rows

Simple rendering is acceptable.

### When data is large (1000+ rows)

Consider:

* Pagination (server-driven preferred)
* Virtualization
* Memoized row rendering
* Stable keys

Virtualization may require abandoning native `<table>` for layout control.

If semantic structure is sacrificed, accessibility must be reintroduced explicitly.

---

## Sorting Patterns

Sorting must:

* Be clearly indicated visually
* Be accessible via keyboard
* Announce state changes to screen readers

Sorting should not:

* Mutate original data
* Be embedded as implicit internal behavior

State should be controlled by consumers.

---

## Pagination Strategy

Preferred order of scaling:

1. Server-side pagination
2. Client-side pagination (small datasets)
3. Virtualization (large datasets)

Avoid client-side rendering of extremely large datasets without virtualization.

---

## Row Selection

Row selection must:

* Use checkboxes for multi-select
* Clearly indicate selected state
* Support keyboard interaction

Example:

```tsx
<th>
  <input type="checkbox" aria-label="Select all rows" />
</th>
```

Do not overload row click for selection without accessibility fallback.

---

## Column Definitions

Columns should be defined declaratively.

Conceptual model:

```tsx
type ColumnDefinition<T> = {
  header: string
  accessor: (row: T) => ReactNode
  sortable?: boolean
}
```

Columns describe structure.
They do not fetch or mutate data.

---

## Failure Modes

Common breakdowns include:

* Rendering thousands of rows without optimization
* Mixing business logic into cell renderers
* Over-customizing layout for edge cases
* Replacing semantic tables with div grids unnecessarily
* Inconsistent sorting behavior across products

Complexity increases non-linearly as features accumulate.

---

## Anti-Patterns

Avoid:

* Monolithic “DataGrid” components with hidden logic
* Tight coupling to specific API responses
* Embedding server calls inside the table component
* Implicit data mutation during sorting

Tables should remain predictable and composable.

---

## Guiding Principle

> A table renders structured data clearly. It does not control the data lifecycle.

Scale responsibly.
