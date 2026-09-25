# Custom `Promise.any`

## Required Behavior

- Fulfill with the first successful input.
- Ignore individual rejections while another input may fulfill.
- If every input rejects, reject with an `AggregateError`.
- Preserve rejection reasons in input order.
- Reject empty input immediately with an empty `AggregateError`.

## Initial Design and Corrections

I created one outer Promise, resolved it on the first successful task, stored errors at their task indexes, and counted failures.

The main corrections were:

- increment the counter only when a task rejects;
- compare with `tasks.length`, not `task.length`—a function's `.length` is its declared parameter count;
- reject with `AggregateError`, not the plain error array;
- explicitly reject empty input because `forEach` will not execute.

## Final Task-Function Version

```js
function promiseAny(tasks) {
    return new Promise((resolve, reject) => {
        if (tasks.length === 0) {
            reject(new AggregateError([], "All tasks were rejected"));
            return;
        }

        const errors = [];
        let rejectedCount = 0;

        tasks.forEach((task, index) => {
            Promise.resolve()
                .then(() => task())
                .then(result => {
                    resolve(result);
                })
                .catch(error => {
                    errors[index] = error;
                    rejectedCount++;

                    if (rejectedCount === tasks.length) {
                        reject(
                            new AggregateError(
                                errors,
                                "All tasks were rejected",
                            ),
                        );
                    }
                });
        });
    });
}
```

Assigning `errors[index]` preserves input order even when tasks reject in a different completion order. `Promise.resolve().then(() => task())` converts synchronous task throws into rejected Promises.

## Native API Difference

Native `Promise.any` accepts values and Promises rather than functions. A native-compatible implementation uses:

```js
Promise.resolve(value).then(resolve, handleRejection);
```

The counting and ordered-error logic otherwise remains the same.

## Complexity

- Time: **O(n)** to start tasks and attach handlers.
- Extra Space: **O(n)** for ordered rejection reasons.

## Interview Takeaway

Unlike `Promise.race`, `Promise.any` ignores rejection until every candidate has failed. Count only failures, preserve their input positions, handle empty input explicitly, and distinguish a list's length from a function's parameter-count `.length`.
