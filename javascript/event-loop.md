# Event Loop

## Why Event Loop?

JavaScript is single-threaded.

The Event Loop enables asynchronous operations without blocking the Call Stack.

---

## Components

- Call Stack
- Web APIs
- Callback Queue (Macrotask Queue)
- Microtask Queue
- Event Loop

---

## Priority

1. Call Stack
2. Microtask Queue
3. Callback Queue

---

## Microtasks

- Promise.then()
- Promise.catch()
- Promise.finally()
- queueMicrotask()

---

## Macrotasks

- setTimeout()
- setInterval()
- DOM Events

---

## Example

```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

Output

```
Start
End
Promise
Timeout
```

---

## Key Points

- Microtasks execute before Macrotasks.
- `setTimeout(fn, 0)` never executes immediately.
- Event Loop moves tasks to the Call Stack only when it becomes empty.