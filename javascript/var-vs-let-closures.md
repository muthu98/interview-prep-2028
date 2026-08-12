# Closures

## Day 11 — Closure Deep Dive

A closure is a function together with its lexical environment.

It allows a function to access variables from its outer scope even after the outer function has finished executing.

```js
function outer() {
    let count = 0;

    return function () {
        count++;
        return count;
    };
}

const counter = outer();

counter(); // 1
counter(); // 2
counter(); // 3
```

## Why Does Closure Remember Variables?

JavaScript uses lexical scoping.

The inner function maintains a reference to the variables available in its lexical environment. Therefore, the outer function's local variables remain reachable while the inner function still references them.

## Closure with Objects

```js
function createCounter() {
    let count = 0;

    return {
        increment() {
            count++;
        },

        getCount() {
            return count;
        }
    };
}

const counter = createCounter();

counter.increment();
counter.increment();

console.log(counter.getCount()); // 2
```

Both methods share access to the same closed-over `count`.

# var vs let with Closures

## var

```js
for (var i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 0);
}
```

Output:

```text
3
3
3
```

`var` is function-scoped. The callbacks close over the same `i` binding.

The loop finishes before the callbacks execute, so `i` has become `3`.

## let

```js
for (let i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 0);
}
```

Output:

```text
0
1
2
```

`let` is block-scoped and provides a separate binding for each loop iteration.

Each callback therefore closes over a different `i`.

## Interview Comparison

| | var | let |
|---|---|---|
| Scope | Function | Block |
| Loop binding | Shared | New binding per iteration |
| Closure example | `3 3 3` | `0 1 2` |

# First-Class Functions

JavaScript treats functions as first-class values.

Functions can be:

- Assigned to variables
- Passed as arguments
- Returned from functions
- Stored in objects or arrays

```js
const greet = function () {
    console.log("Hello");
};

function execute(fn) {
    fn();
}

execute(greet);
```

# Higher-Order Functions

A higher-order function is a function that:

- Accepts another function as an argument
- Or returns a function
- Or does both

```js
function execute(fn) {
    fn();
}
```

`execute` is a higher-order function because it accepts a function as an argument.

# Interview Mistakes

## Mistake 1

Incorrect:

> `var` is global.

Correct:

> `var` is function-scoped. It is not inherently global.

## Mistake 2

Incorrect:

> A higher-order function only returns another function.

Correct:

> A higher-order function can accept a function, return a function, or both.

## Mistake 3

Function declaration:

```js
function test() {}
```

Function expression:

```js
const test = function () {};
```

Arrow-function expression:

```js
const test = () => {};
```

## Mistake 4

Do not assume every regular function has the same `this`.

A regular function's `this` depends on how the function is invoked.
