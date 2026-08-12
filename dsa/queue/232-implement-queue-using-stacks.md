# 232. Implement Queue using Stacks

**Pattern:** Queue  
**Difficulty:** Easy  
**LeetCode:** https://leetcode.com/problems/implement-queue-using-stacks/

## Problem

Implement a FIFO queue using only stacks.

Operations:

- `push(x)`
- `pop()`
- `peek()`
- `empty()`

## Initial Approach

Initially considered using a normal array:

```js
queue.push(x);
queue.shift();
```

The issue is that removing the first element can require shifting the remaining elements.

So `pop()` can become O(n).

## Optimized Approach

Use two stacks:

- `stack1` → used for `pop()` and `peek()`
- `stack2` → used for `push()`

When `stack1` is empty, move all elements from `stack2` to `stack1`.

This reverses the order and puts the oldest element on top of `stack1`.

## Important Insight

A single transfer can take O(n), but every element is transferred at most once before it is popped.

Therefore:

- A single `pop()` can be O(n)
- Amortized `pop()` is O(1)
- Amortized `peek()` is O(1)

## Code

```js
var MyQueue = function () {
    this.stack1 = [];
    this.stack2 = [];
};

MyQueue.prototype.push = function (x) {
    this.stack2.push(x);
};

MyQueue.prototype.pop = function () {
    if (this.stack1.length === 0) {
        while (this.stack2.length) {
            this.stack1.push(this.stack2.pop());
        }
    }

    return this.stack1.pop();
};

MyQueue.prototype.peek = function () {
    if (this.stack1.length === 0) {
        while (this.stack2.length) {
            this.stack1.push(this.stack2.pop());
        }
    }

    return this.stack1[this.stack1.length - 1];
};

MyQueue.prototype.empty = function () {
    return this.stack1.length === 0 && this.stack2.length === 0;
};
```

## Complexity

| Operation | Complexity |
|---|---|
| push | O(1) |
| pop | O(1) amortized |
| peek | O(1) amortized |
| empty | O(1) |
| Space | O(n) |

## Interview Learning

My initial concern was that moving all elements from `stack2` to `stack1` would make the solution inefficient.

The important concept is **amortized complexity**.

An element is transferred only once from `stack2` to `stack1`, so the total work over many operations remains O(n).
