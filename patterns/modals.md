# Modal Patterns

## Responsibility

This document defines how modal dialogs should be designed, composed, and managed within the frontend system.

Modals are high-impact UI patterns. They interrupt user flow, manage focus, and alter navigation behavior. Poorly designed modals are a major source of accessibility, usability, and state-management bugs.

Modals are patterns, not primitives.

---

## Core Principles

### 1. Explicit interruption

A modal represents a deliberate interruption of the current user task.

Use a modal only when:

* Immediate user attention is required
* The task cannot be completed inline
* Deferring the action would be harmful or confusing

Avoid modals for simple confirmations or minor edits that can be handled inline.

---

### 2. Single responsibility

A modal should focus on one primary task.

Examples:

* Confirming a destructive action
* Editing a focused set of fields
* Displaying critical information

Avoid placing complex multi-step workflows inside a single modal.

---

## Structural Composition

A modal is composed of:

* Overlay (backdrop)
* Dialog container
* Header (optional)
* Content area
* Footer actions (optional)

Conceptual structure:

```tsx
<Portal>
  <Overlay />
  <Dialog role="dialog" aria-modal="true">
    <Header />
    <Content />
    <Footer />
  </Dialog>
</Portal>
```

The modal must render outside the normal DOM flow.

---

## Accessibility Requirements

Modals must:

* Trap keyboard focus within the dialog
* Move focus into the modal on open
* Restore focus to the triggering element on close
* Close on `Escape` key
* Prevent background content from being announced

Use appropriate ARIA attributes:

```tsx
role="dialog"
aria-modal="true"
```

Failure to manage focus correctly results in broken keyboard navigation.

---

## Focus Management

Focus behavior must follow this lifecycle:

1. Capture the triggering element
2. Move focus to the first focusable element in the modal
3. Trap focus while open
4. Restore focus on close

Focus should never be lost to the document body.

---

## State Management

Modal state should be controlled by the orchestration layer.

Recommended pattern:

```tsx
const [isOpen, setIsOpen] = useState(false)
```

The modal component itself should remain stateless.

Avoid global modal state unless managing application-level workflows.

---

## Closing Behavior

A modal should close when:

* The primary action completes successfully
* The user presses `Escape`
* The user clicks the explicit close action

Backdrop click behavior must be deliberate and documented.

Never rely on implicit closure mechanisms.

---

## Scroll Management

When a modal is open:

* Background scrolling must be disabled
* Modal content should scroll independently if necessary

Scroll locking should not cause layout shift.

---

## Nested Modals

Nested modals are strongly discouraged.

If unavoidable:

* Only one modal may be focus-active at a time
* Focus trapping must cascade correctly
* Z-index and stacking context must be explicitly managed

Nested modals dramatically increase cognitive and technical complexity.

---

## Failure Modes

Common modal failures include:

* Focus escaping the dialog
* Inaccessible keyboard navigation
* Background content remaining interactive
* Scroll bleed-through
* Unclear dismissal behavior

These issues are often subtle and hard to detect without testing.

---

## Anti-Patterns

Avoid:

* Using modals as routing substitutes
* Embedding heavy business logic inside modal components
* Automatically opening modals on page load
* Rendering modals conditionally without portals

Modals should feel intentional, not surprising.

---

## Testing Strategy

Modal tests should verify:

* Focus trap behavior
* Keyboard navigation
* Escape key handling
* Screen reader semantics
* Scroll lock behavior

Manual keyboard testing is mandatory.

---

## Guiding Principle

> A modal is a controlled interruption. Control must extend to focus, state, and intent.

Use modals sparingly and deliberately.
