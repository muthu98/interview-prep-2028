# React Re-render Triggers and Memoization

## Day 20 — Re-renders and Memoization

### Re-render Triggers

- A component's state update can trigger a render.
- A parent render normally renders its children; new props are received through that rendering.
- Changes to consumed context or selected external store state (for example, Redux) can trigger a render.
- A click alone is not a render trigger. Its handler must cause a state, context, store, or parent update.
- An HOC is a component pattern, not itself a render trigger; updates from its props or subscriptions matter.

### Memoization Basics

| API | What it does |
|---|---|
| `React.memo` | Can skip rendering a component when its props compare unchanged. |
| `useMemo` | Caches the value returned by a calculation until dependencies change. |
| `useCallback` | Caches a function reference until dependencies change. |

The result-versus-function distinction was already understood; the explanation was tightened to say that `useMemo` caches the callback's result.

### Revision Follow-up

- [ ] Explain when a memoized component can still render, including its own state, consumed context, and changed object/function prop references.

This follow-up was raised but not completed in the Day 20 discussion.
