# JavaScript Promises

## What is a Promise?

A Promise is an object that represents the eventual completion or failure of an asynchronous operation.

---

## Promise States

- Pending
- Fulfilled
- Rejected

---

## resolve()

Marks the Promise as fulfilled and passes the value to `.then()`.

---

## reject()

Marks the Promise as rejected and passes the error to `.catch()`.

---

## .then()

Executes when the Promise is fulfilled.

---

## .catch()

Handles rejected Promises and errors.

---

## .finally()

Executes regardless of whether the Promise is fulfilled or rejected.

---

## Promise Chaining

Allows multiple asynchronous operations to execute sequentially using multiple `.then()` calls.

---

## Important Points

- Promise settles only once.
- Pending → Fulfilled
- Pending → Rejected
- Cannot change state after settlement.

---

# Custom Promise.all

## Required Behavior

- Return one Promise rather than an array of Promises.
- Accept Promises and ordinary values.
- Preserve input order regardless of completion order.
- Resolve after every input resolves.
- Reject as soon as any input rejects.
- Resolve with `[]` for an empty input.

## Initial Approach

Initially used `map` with an async callback. This returned an array of Promises instead of one combined Promise.

The attempt also awaited each item and then tried to call `.then()` on the resolved value. That fails for ordinary values and for Promise results that are not themselves Promises.

Another attempt returned the results array from inside the Promise executor. Returning from an executor does not settle its Promise; only `resolve` or `reject` does.

## Corrected Approach

- Return one outer Promise.
- Normalize every input with `Promise.resolve(value)`.
- Store each fulfilled value at its original index.
- Count successful completions.
- Resolve with the ordered results when the count matches the input length.
- Reject the outer Promise immediately when an input rejects.

## Code

```js
function myPromiseAll(values) {
    return new Promise((resolve, reject) => {
        const results = [];
        let completed = 0;

        if (values.length === 0) {
            resolve([]);
            return;
        }

        values.forEach((value, index) => {
            Promise.resolve(value)
                .then(result => {
                    results[index] = result;
                    completed++;

                    if (completed === values.length) {
                        resolve(results);
                    }
                })
                .catch(error => reject(error));
        });
    });
}
```

## Why It Works

- `Promise.resolve` accepts both ordinary values and Promise-like inputs.
- `results[index]` preserves input order even when completion order differs.
- The counter prevents early fulfillment.
- Rejection is fail-fast: the outer Promise rejects immediately, though other asynchronous operations continue running because they are not automatically cancelled.

## Promise.all vs Promise.allSettled

- `Promise.all` asks whether everything succeeded and rejects when any input rejects.
- `Promise.allSettled` waits for every input and resolves with fulfilled and rejected outcome objects.
- `Promise.allSettled` resolves the outer Promise because failures are returned as report data.

The `Promise.allSettled` comparison was understood, but a separate custom implementation was not completed.

## Complexity

- Time: **O(n)**, excluding the asynchronous work performed by the inputs.
- Extra Space: **O(n)** for the ordered results.

## Interview Takeaway

Mapping async callbacks produces an array of Promises; it does not create one aggregate Promise. A Promise executor must call `resolve` or `reject`, and completion order must be separated from result order.
