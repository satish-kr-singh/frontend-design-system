# Frontend Layering Architecture

## Responsibility

This document defines how responsibilities are layered within the frontend architecture.

The goal is to create a system that:

* Scales with team size
* Preserves maintainability
* Enables performance optimization
* Prevents responsibility leakage

Layering is about controlling complexity, not enforcing folders.

---

## Core Principle

> Each layer has a single primary reason to change.

When layers blur, velocity drops and defects rise.

---

## Layer Overview

The frontend system is divided into the following conceptual layers:

1. Presentation Layer (UI)
2. Composition Layer
3. State & Orchestration Layer
4. Domain Layer
5. Data Access Layer

These layers communicate through explicit contracts.

---

## 1. Presentation Layer (UI)

### Responsibility

* Render visual elements
* Apply design tokens
* Preserve accessibility semantics
* Remain stateless whenever possible

Examples:

* Primitives (`Button`, `Input`)
* Visual-only components
* Stateless display components

### Constraints

This layer must not:

* Fetch data
* Contain business rules
* Coordinate workflows
* Manage side effects

UI components should be predictable and easily testable.

---

## 2. Composition Layer

### Responsibility

* Assemble primitives into patterns
* Manage layout and structure
* Coordinate accessibility relationships

Examples:

* Forms
* Modals
* Data tables

This layer composes UI without owning domain logic.

---

## 3. State & Orchestration Layer

### Responsibility

* Coordinate user interactions
* Manage local UI state
* Bridge UI with domain logic

Examples:

* Form controllers
* Page-level components
* Feature-level containers

This layer may:

* Handle loading and error states
* Trigger domain operations
* Coordinate async workflows

It should not define business rules.

---

## 4. Domain Layer

### Responsibility

* Contain business rules
* Define domain models
* Enforce invariants

Examples:

* Validation logic
* Permission checks
* Domain-specific calculations

The domain layer must remain UI-agnostic.

This enables reuse across different interfaces.

---

## 5. Data Access Layer

### Responsibility

* Communicate with external systems
* Fetch and persist data
* Normalize API responses

Examples:

* API clients
* GraphQL hooks
* Repository abstractions

This layer isolates backend change impact.

---

## Data Flow Direction

Preferred flow:

```
UI → Composition → State → Domain → Data Access
```

Responses flow upward through the same layers.

Direct cross-layer access should be avoided.

---

## State Ownership Rules

* UI state lives in the orchestration layer
* Domain state lives in the domain layer
* Server state lives in the data layer

Avoid duplicating state across layers.

---

## Performance Implications

Clear layering enables:

* Memoization boundaries
* Reduced re-renders
* Predictable data fetching
* Easier profiling

Performance optimizations should respect layer boundaries.

---

## Testing Strategy by Layer

* UI layer: snapshot and accessibility tests
* Composition layer: interaction tests
* State layer: behavioral tests
* Domain layer: pure unit tests
* Data layer: contract tests

Testing mirrors responsibility.

---

## Common Failure Modes

* UI components performing data fetching
* Business rules embedded in components
* State duplicated across layers
* Tight coupling between UI and APIs

These failures compound over time.

---

## Guiding Principle

> Layering is a tool for thinking, not a rigid structure.

When boundaries are respected, systems scale with clarity.
