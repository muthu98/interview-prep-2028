# Custom `Promise.race`

## Required Behavior

- Return one Promise.
- Accept values and Promises.
- Settle exactly as the first input settles.
- Fulfill if that input fulfills and reject if it rejects.
- Leave empty input pending forever.

## Initial Task-Function Version

I first implemented the same scheduling idea for lazy task functions:

```js
function raceTasks(tasks) {
    return new Promise((resolve, reject) => {
        tasks.forEach(task => {
            Promise.resolve()
                .then(() => task())
                .then(resolve, reject);
        });
    });
}
```

This correctly starts every task, catches synchronous throws, and lets the first settlement win. However, it is a task-runner contract rather than the native `Promise.race` contract.

## Native-Compatible Version

```js
function promiseRace(values) {
    return new Promise((resolve, reject) => {
        values.forEach(value => {
            Promise.resolve(value).then(resolve, reject);
        });
    });
}
```

Each input attempts to settle the same outer Promise. A Promise changes state only once, so later fulfillment or rejection attempts have no effect.

No result array or completion counter is required. If `values` is empty, `forEach` schedules nothing and the returned Promise remains pending, matching native behavior.

## Complexity

- Time: **O(n)** to attach handlers.
- Extra Space: **O(n)** Promise reactions.

## Interview Takeaway

`Promise.race` is about first settlement, not first fulfillment. Clarify whether inputs are eager values/Promises or lazy task functions, normalize the correct input type, and rely on the outer Promise's one-time settlement rule.
