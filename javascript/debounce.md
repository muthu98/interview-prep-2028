# Debounce

## Definition

Debounce delays a function until calls have stopped for a specified amount of time.

When another call arrives before the delay ends, the previous timer is cancelled and a new waiting period begins.

## Recognition Clues

- A function is triggered repeatedly in a short period.
- Only the final call should run after activity stops.
- Common examples include search input, resize handling, and validation after typing.

## My Approach

Keep the timer identifier in a closure. Return a wrapper function that:

1. Cancels the previous timer.
2. Starts a new timer.
3. Calls the original function after the delay.
4. Forwards the wrapper's arguments and `this` value.

## Code

```js
function debounce(func, delay) {
    let timeoutId;

    return function (...args) {
        clearTimeout(timeoutId);

        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}
```

## Why It Works

- `timeoutId` remains available through closure after `debounce` returns.
- `clearTimeout(timeoutId)` prevents an earlier scheduled call from running.
- The arrow callback captures the returned function's `this` value.
- `func.apply(this, args)` invokes the original function with the same receiver and arguments.

## Complexity

- Time per wrapper call: **O(1)**, excluding the work performed by `func`.
- Extra Space: **O(1)**, excluding the forwarded arguments.

## Interview Takeaway

Debounce waits for a quiet period and then runs the latest call. The closure preserves the timer, while `apply` preserves the original calling context and arguments.

Throttle is related but different: it limits how often a function can run during continuous activity rather than waiting until activity stops.
