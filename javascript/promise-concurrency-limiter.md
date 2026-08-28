# Promise Concurrency Limiter

## Requirement

Implement `promisePool(tasks, limit)` where each task is a function that returns a value or Promise.

- Run at most `limit` tasks at once.
- Preserve input order in the results.
- Reject on the first task failure.
- Stop scheduling queued tasks after failure.
- Treat synchronous task throws as rejections.
- Resolve an empty task list with `[]`.

## Initial Design

I chose the right main pieces early:

- a queue of task functions,
- a count of running tasks,
- an index for result order,
- an outer Promise,
- and a scheduler that starts work while capacity remains.

The early implementations exposed several async coordination mistakes:

- `runningTask <= limit` started one task too many;
- handlers used a shared changing index instead of capturing the task's index;
- results used all-settled-style objects even though the requirement was fail-fast;
- `finally` syntax was invalid in one version;
- the pool resolved when the queue emptied, before active tasks had finished;
- rejection did not stop new tasks from being scheduled;
- a final `catch` turned rejection back into fulfillment;
- completed tasks did not reliably restart scheduling.

## Correct Scheduling Invariants

1. Start work only while `runningTask < limit`.
2. Capture `taskIndex` before starting that task.
3. Increment the running count when scheduled and decrement it in `.finally()`.
4. Store success at `results[taskIndex]` to preserve input order.
5. On the first failure, set `failed = true`, reject, and schedule nothing else.
6. Resolve only when the queue is empty and `runningTask === 0`.
7. Otherwise call the scheduler again when capacity becomes available.

Wrapping invocation like this handles a task that throws before returning a Promise:

```js
Promise.resolve().then(() => task())
```

## Final Code

```js
async function promisePool(tasks, limit) {
    return new Promise((resolve, reject) => {
        if (tasks.length === 0) {
            resolve([]);
            return;
        }

        let runningTask = 0;
        let index = 0;
        let failed = false;
        const queue = [...tasks];
        const results = [];

        const execute = () => {
            while (runningTask < limit && queue.length > 0 && !failed) {
                const task = queue.shift();
                const taskIndex = index;

                Promise.resolve()
                    .then(() => task())
                    .then(result => {
                        results[taskIndex] = result;
                    })
                    .catch(error => {
                        failed = true;
                        reject(error);
                    })
                    .finally(() => {
                        runningTask--;

                        if (failed) return;

                        if (queue.length === 0 && runningTask === 0) {
                            resolve(results);
                        } else {
                            execute();
                        }
                    });

                runningTask++;
                index++;
            }
        };

        execute();
    });
}
```

The outer `async` keyword is unnecessary because the function already returns a Promise, but keeping it does not change behavior.

## Failure Semantics

Fail-fast does not cancel tasks that are already running. It rejects the pool as soon as the first failure is observed and prevents queued tasks from starting. Already-started task Promises continue independently.

The `failed` flag also prevents later `.finally()` handlers from restarting the scheduler or trying to complete the pool successfully.

## Complexity

- Time: **O(n)** scheduling work, excluding the cost of the tasks and `queue.shift()` implementation overhead.
- Space: **O(n)** for the copied queue and ordered results.
- Active tasks: at most **`limit`**.

## Interview Follow-ups

- Validate `limit > 0`; otherwise a non-empty input remains pending. This guard was optional for the completed requirements.
- Replace repeated `queue.shift()` calls with a task cursor to avoid array reindexing overhead.
- Explain that result order follows task input order, not completion order.
- Explain why stopping future scheduling is different from cancelling work already in flight.

## Interview Takeaway

A concurrency pool is a scheduler with explicit invariants. Count active work, capture per-task state before the async boundary, refill capacity after settlement, and separate fail-fast rejection from cancellation.
