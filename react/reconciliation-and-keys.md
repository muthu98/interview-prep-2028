# React Reconciliation and Keys

## Day 22

Reconciliation is React's process of comparing the previous rendered tree with the new rendered tree and deciding what needs to change in the real DOM.

A component can re-render without necessarily causing a real DOM update.

## Stable Keys

For dynamic lists, prefer a stable identity:

```jsx
items.map((item) => (
  <div key={item.id}>{item.name}</div>
))
```

A stable `item.id` lets React track the same logical item across insertion, deletion, and reordering.

Using the array index can cause identity problems when list positions change, especially with:

- input state
- component-local state
- animations
- unnecessary DOM work

## Interview Takeaway

Use a stable unique key when list items can be inserted, removed, or reordered. The key helps reconciliation decide whether an item is the same logical element as before.
