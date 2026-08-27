# 19. Remove Nth Node From End of List

**Pattern:** Linked List / Fast and Slow Pointers

**Difficulty:** Medium

**LeetCode:** https://leetcode.com/problems/remove-nth-node-from-end-of-list/

## Problem

Remove the nth node from the end of a linked list and return its head.

The follow-up asks for a one-pass solution using O(1) extra space.

## Recognition Clues

- The position is measured from the end.
- The list length is not known in advance.
- A fixed gap between two pointers can locate the target in one pass.
- A dummy node can remove the head without a separate deletion case.

## My Initial Approach

I first traversed the list to calculate its length. I converted `n` from an end-based position into a start-based position, traversed again, saved the previous node, and bypassed the target.

```js
var removeNthFromEnd = function (head, n) {
    let finalNode = head;
    let previous;
    let count = 0;
    let check = head;

    while (check) {
        count++;
        check = check.next;
    }

    n = count - n;

    while (head && n > -1) {
        if (n === 0) {
            if (previous) {
                previous.next = head.next;
            } else {
                finalNode = head.next;
            }
        }

        previous = head;
        n--;
        head = head.next;
    }

    return finalNode;
};
```

## What Was Wrong or Incomplete

The initial solution returned the correct result in O(L) time and O(1) extra space, but it used two passes:

1. Calculate the list length.
2. Restart from the head to remove the target.

It also continued traversing after completing the deletion. The problem's interview follow-up specifically asks for one pass without first determining the length.

The optimized solution has the same Big-O complexity. Its advantage is satisfying the one-pass constraint and demonstrating pointer-distance reasoning.

## Final Approach

- Create a dummy node before `head`.
- Start `fast` and `slow` at the dummy.
- Move `fast` forward `n + 1` positions.
- Move both pointers together until `fast` reaches `null`.
- `slow` is now immediately before the target.
- Bypass the target with `slow.next = slow.next.next`.
- Return `dummy.next`.

The `n + 1` gap positions `slow` before the target. The dummy node handles removing the original head uniformly.

## Code

```js
var removeNthFromEnd = function (head, n) {
    const dummy = new ListNode(0, head);
    let fast = dummy;
    let slow = dummy;

    while (n > -1) {
        n--;
        fast = fast.next;
    }

    while (fast) {
        slow = slow.next;
        fast = fast.next;
    }

    slow.next = slow.next.next;

    return dummy.next;
};
```

## Complexity

- Time: **O(L)** — the pointers move forward without restarting from the head.
- Extra Space: **O(1)** — only a dummy node and pointer variables are used.

## Interview Takeaway

When a linked-list position is measured from the end, use a fixed gap between fast and slow pointers. A dummy node turns head deletion into the same pointer operation used for every other node.
