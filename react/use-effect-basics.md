# React `useEffect` Basics

## Day 23

### No dependency array

```jsx
useEffect(() => {
  // ...
});
```

Runs after every render.

### Empty dependency array

```jsx
useEffect(() => {
  // ...
}, []);
```

Runs after the first render in normal production behavior.

In development StrictMode, React may intentionally run effects more than once to expose unsafe side effects.

### Dependency array

```jsx
useEffect(() => {
  // ...
}, [userId]);
```

Runs after the first render and again when `userId` changes.

### Cleanup

```jsx
useEffect(() => {
  const id = setInterval(() => {
    console.log("running");
  }, 1000);

  return () => {
    clearInterval(id);
  };
}, []);
```

The cleanup runs when the component unmounts and before the effect runs again when dependencies change.

Common cleanup cases:

- intervals and timeouts
- event listeners
- WebSocket/subscription cleanup
- aborting requests

## Interview Takeaway

The dependency array controls when the effect re-runs; the returned function cleans up resources from the previous effect lifecycle.
