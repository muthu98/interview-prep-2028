# Custom EventEmitter

## Required Behavior

- `on(eventName, listener)` registers a reusable listener.
- `once(eventName, listener)` registers a listener for one emission.
- `off(eventName, listener)` removes the latest matching registration under the chosen contract.
- `off(eventName)` removes every listener for that event.
- `emit(eventName, ...args)` invokes listeners in registration order.
- Listener removal and reentrant emission behave predictably.

## Initial Approach

I started with two Maps: one for regular listeners and one for once-only listeners.

During that version, I confused `Map.has()` with `Map.get()` and the array returned by `get()`. I also used the return value of `push()`, which is the new array length rather than the array. My first `off()` removed the whole event instead of one supplied listener, and `emit()` used `else if`, so it could not run both regular and once-only listeners for the same event.

## Corrections During Implementation

- Use `Map.has(eventName)` only to test membership and `Map.get(eventName)` to retrieve entries.
- Push into the stored array without assigning the numeric return value of `push()`.
- When a listener is supplied to `off()`, remove only the intended matching registration.
- Do not use `else if` when both listener categories may exist.
- Remove a once-only registration before invoking it. If its callback emits the same event recursively, it must not run a second time.
- Iterate over a snapshot so additions or removals do not change the current emission pass.

The larger design problem remained: separate Maps group regular and once-only listeners, so they cannot preserve the order of mixed `on()` and `once()` registrations.

## Final Design

Use one Map. Each event maps to a single ordered array of entries:

```text
eventName → [{ listener, once }, { listener, once }, ...]
```

`off()` uses strict function-reference equality and `findLastIndex()` because this implementation deliberately removes the latest matching registration. During `emit()`, a snapshot fixes the current pass. For a once entry, the exact entry object is found in the live array and removed before its listener runs.

## Code

```js
class EventEmitter {
    constructor() {
        this.events = new Map();
    }

    on(eventName, listener, once = false) {
        if (this.events.has(eventName)) {
            this.events.get(eventName).push({ listener, once });
        } else {
            this.events.set(eventName, [{ listener, once }]);
        }
    }

    off(eventName, listener) {
        if (!listener) {
            this.events.delete(eventName);
        } else if (this.events.has(eventName)) {
            const values = this.events.get(eventName);
            const targetIndex = values.findLastIndex(
                value => value.listener === listener,
            );

            if (targetIndex !== -1) {
                values.splice(targetIndex, 1);

                if (values.length === 0) {
                    this.events.delete(eventName);
                }
            }
        }
    }

    once(eventName, listener) {
        this.on(eventName, listener, true);
    }

    emit(eventName, ...args) {
        if (this.events.has(eventName)) {
            const values = this.events.get(eventName);

            [...values].forEach(value => {
                if (value.once) {
                    const index = values.indexOf(value);

                    if (index !== -1) {
                        values.splice(index, 1);

                        if (values.length === 0) {
                            this.events.delete(eventName);
                        }
                    }
                }

                value.listener(...args);
            });
        }
    }
}
```

## Complexity

For `k` listeners registered to one event:

- `on()`: **O(1)** amortized.
- `once()`: **O(1)** amortized.
- `off()`: **O(k)**.
- `emit()`: **O(k)** normally.
- Storage: **O(total listeners)**.

With many once-only listeners, repeated `indexOf()` and `splice()` calls can make one `emit()` approach **O(k²)**. This is an interview optimization follow-up, not a correctness failure in the completed design.

## Interview Takeaway

An EventEmitter is not only a Map of callbacks. Registration order, duplicate-listener policy, mutation during emission, and reentrancy are part of its contract. Store mixed listener types in one ordered structure, iterate a snapshot, and remove once-only entries before invoking them.
