# 287. Find the Duplicate Number

**Pattern:** Fast and Slow Pointers / Floyd's Cycle Detection

**Difficulty:** Medium

**LeetCode:** https://leetcode.com/problems/find-the-duplicate-number/

## Problem

An array contains `n + 1` integers, each in the range `[1, n]`. Return the one distinct duplicated value without modifying the array and using only O(1) extra space. The duplicated value may appear more than twice.

## Baseline: Membership Tracking

My first solution used a Map, then simplified it to a Set because only membership was required:

```js
var findDuplicate = function (nums) {
    const seen = new Set();

    for (const value of nums) {
        if (seen.has(value)) return value;
        seen.add(value);
    }
};
```

This is O(n) time but O(n) extra space, so it does not satisfy the space constraint.

## Why the Sum Shortcut Is Not General

Subtracting the expected sum from the actual sum works only when the duplicate occurs exactly twice and every other value occurs exactly once.

The problem guarantees one distinct duplicated value, not one extra occurrence. For example:

```js
[2, 2, 2, 2, 2]
```

has only one distinct duplicated value, `2`, but both the actual sum and `1 + 2 + 3 + 4` equal `10`. Their difference is `0`, not the answer.

## Turning the Array into a Linked Structure

Every value is a valid next index, so define:

```text
next(index) = nums[index]
```

For `[1, 3, 4, 2, 2]`, traversal from `0` is:

```text
0 → 1 → 3 → 2 → 4 → 2 → 4...
```

The finite, deterministic traversal must repeat. The duplicated destination is the entrance to the cycle.

## Final Floyd's Algorithm

```js
var findDuplicate = function (nums) {
    let slow = 0;
    let fast = 0;

    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow !== fast);

    slow = 0;

    while (slow !== fast) {
        slow = nums[slow];
        fast = nums[fast];
    }

    return slow;
};
```

### Phase 1

Slow moves one edge and fast moves two. They eventually meet somewhere inside the cycle.

### Phase 2

Reset one pointer to `0` and move both one edge at a time. The distance from the start to the cycle entrance matches the remaining cyclic distance from the meeting point, so they meet at the entrance—the duplicate value.

## Complexity

- Time: **O(n)**.
- Extra Space: **O(1)**.
- The input array is not modified.

## Interview Takeaway

Look beyond the array representation. When values are valid indexes, each state has exactly one next state, the state space is finite, and repetition must occur, the array can be treated as an implicit linked structure. That is a strong clue for Floyd's algorithm.
