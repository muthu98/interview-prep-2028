# Throttle

## Definition

Throttle limits how frequently a function can execute during repeated calls.

This implementation uses leading-edge behavior: the first call runs immediately, and calls received during the waiting period are ignored.

## Recognition Clues

- An event can fire continuously or very frequently.
- Work should run at most once during each delay period.
- Common examples include scroll, resize, mouse movement, and repeated button events.

## My Approach

Keep a Boolean waiting flag in a closure.

- If the wrapper is waiting, return without executing the function.
- Otherwise execute the function immediately and enable the waiting flag.
- Reset the flag after the delay so a future call can run.
- Forward the wrapper's arguments and `this` value with `apply`.

## Code

```js
function throttle(func, delay) {
    let shouldWait = false;

    return function (...args) {
        if (shouldWait) return;

        func.apply(this, args);
        shouldWait = true;

        setTimeout(() => {
            shouldWait = false;
        }, delay);
    };
}
```

## Behavior

- The first call executes immediately.
- Calls during the delay are dropped.
- Another call can execute after the waiting period ends.
- This version does not schedule a trailing call.

## Complexity

- Time per wrapper call: **O(1)**, excluding the work performed by `func`.
- Extra Space: **O(1)**, excluding forwarded arguments.

## Interview Takeaway

State the throttle semantics clearly because implementations can differ. This is a leading-edge throttle that drops calls during the waiting period and preserves arguments and `this`.

Explaining throttle versus debounce precisely remains a revision item.
