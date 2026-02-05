# Rendering Strategies and Performance

## Responsibility

This document defines how rendering performance is approached within the frontend architecture.

Performance is treated as a systemic concern, not an afterthought or a collection of micro-optimizations.

The goal is to ensure predictable rendering behavior as application complexity grows.

---

## Core Principle

> Optimize based on measurement, not instinct.

Premature optimization increases complexity without guaranteed benefit. Performance work must be guided by profiling and observable bottlenecks.

---

## Rendering Model Awareness

Modern UI libraries (e.g., React) follow a declarative rendering model.

Key implications:

* State changes trigger re-renders
* Parent re-renders propagate downward
* Referential identity affects memoization

Understanding the rendering model is foundational to performance strategy.

---

## State Placement Strategy

Rendering cost is strongly influenced by where state lives.

Guidelines:

* Keep state as close as possible to where it is used
* Avoid lifting state unnecessarily
* Do not centralize state without need

Incorrect state placement increases re-render surface area.

---

## Memoization Boundaries

Memoization is a tool for stabilizing expensive subtrees.

Common techniques:

* `React.memo`
* `useMemo`
* `useCallback`

These should be applied when:

* A component is demonstrably expensive
* Props are stable and predictable
* Profiling shows measurable impact

Memoization should not be used to mask architectural flaws.

---

## Referential Stability

Unstable object and function references cause unnecessary renders.

Example issue:

```tsx
<Component config={{ sort: true }} />
```

This creates a new object each render.

Preferred:

```tsx
const config = useMemo(() => ({ sort: true }), [])
<Component config={config} />
```

Stability reduces avoidable reconciliation work.

---

## List Rendering Strategy

Lists are common performance hotspots.

Guidelines:

* Use stable keys
* Avoid index as key for dynamic lists
* Memoize row components when appropriate
* Avoid inline functions inside large lists

For large datasets:

* Prefer pagination
* Use virtualization when necessary

Rendering thousands of DOM nodes should be avoided.

---

## Server State vs Client State

Server state should be managed by specialized libraries or abstractions.

Benefits:

* Caching
* Deduplication
* Background refetching
* Reduced manual state tracking

Duplicating server state locally increases rendering complexity.

---

## Concurrent Rendering Considerations

Modern rendering engines may interrupt or restart renders.

Implications:

* Side effects must be isolated
* Rendering should remain pure
* Expensive synchronous computations should be minimized

Long blocking operations degrade responsiveness.

---

## Expensive Computation Strategy

Heavy computations should:

* Be memoized when safe
* Be moved outside render where possible
* Be offloaded to web workers if CPU intensive

Rendering must remain responsive.

---

## Network Performance

Rendering performance is influenced by data strategy.

Best practices:

* Fetch minimal required data
* Avoid over-fetching
* Defer non-critical data
* Use pagination instead of bulk loading

Network inefficiency amplifies rendering cost.

---

## Measuring Performance

Use tools such as:

* Browser performance profiler
* React DevTools Profiler
* Lighthouse

Measure:

* Commit time
* Render frequency
* Component re-render patterns

Optimization must be evidence-driven.

---

## Common Failure Modes

* Blanket use of memoization
* Global state for localized concerns
* Rendering large datasets without pagination
* Excessive prop drilling causing tree-wide updates
* Embedding heavy computations inside render

Performance issues usually reflect architectural misplacement.

---

## Performance Review Checklist

Before optimizing, verify:

1. Is the slowdown measurable?
2. Which component is re-rendering excessively?
3. Is state placed appropriately?
4. Is memoization justified?
5. Can work be deferred or segmented?

Clarity precedes optimization.

---

## Guiding Principle

> Performance is a property of architecture, not decoration.

Sustainable speed emerges from clean boundaries and measured decisions.
