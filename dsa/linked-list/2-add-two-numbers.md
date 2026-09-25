# 2. Add Two Numbers

**Pattern:** Linked List / Carry Simulation

**Difficulty:** Medium

**LeetCode:** https://leetcode.com/problems/add-two-numbers/

## Problem

Two non-empty linked lists store non-negative integers in reverse digit order. Add the numbers and return the sum in the same reversed linked-list format.

## Recognition Clues

- Digits are already ordered from least significant to most significant.
- Corresponding nodes can be added in one forward traversal.
- Each position may produce a carry for the next position.
- The lists may have different lengths, and a final carry may require one extra node.

## Initial Approach

I planned to traverse `l1` and `l2` together, add their values plus a carried value, split the sum using `%` and division, continue through whichever list remained, and append a final node if a carry still existed.

I chose to reuse `l1` as the result list instead of allocating a separate result list. That keeps auxiliary space constant but means the first input is intentionally mutated and must be extended when it is shorter than `l2`.

## Final In-Place Code

```js
var addTwoNumbers = function (l1, l2) {
    let carry = 0;
    const result = l1;

    while (l1 || l2) {
        const value1 = l1?.val ?? 0;
        const value2 = l2?.val ?? 0;
        const sum = value1 + value2 + carry;

        l1.val = sum % 10;
        carry = Math.floor(sum / 10);

        if (!l1.next && (l2?.next || carry)) {
            l1.next = new ListNode();
        }

        l1 = l1.next;
        l2 = l2?.next ?? null;
    }

    return result;
};
```

LeetCode guarantees both input lists are non-empty, so `l1` exists when the first result digit is written.

## Why the Extension Condition Works

```js
if (!l1.next && (l2?.next || carry)) {
    l1.next = new ListNode();
}
```

A new result node is required when `l1` has ended but either:

- `l2` still has another digit, or
- the current addition produced a carry.

The next loop iteration fills that new node with the correct digit.

## Complexity

- Time: **O(max(n, m))**.
- Auxiliary Space: **O(1)**, excluding new nodes required when `l1` is shorter or a final carry exists.

## Interview Takeaway

Reversed digit order makes ordinary addition natural: process one position at a time, write `sum % 10`, and carry `Math.floor(sum / 10)`. State clearly that this version reuses and mutates `l1`; a dummy-headed result list is preferable when inputs must remain unchanged or symmetric code is desired.
