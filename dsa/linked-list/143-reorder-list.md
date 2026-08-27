# 143. Reorder List

**Pattern:** Linked List / Split, Reverse, and Merge

**Difficulty:** Medium

**LeetCode:** https://leetcode.com/problems/reorder-list/

## Problem

Reorder `L0 → L1 → ... → Ln` in place as `L0 → Ln → L1 → Ln-1 → ...` without changing node values.

## Recognition Clues

- The output alternates nodes from the beginning and end.
- A singly linked list cannot be traversed backward directly.
- Reversing a suffix makes its end available through forward traversal.
- The nodes must be reconnected in place.

## My Initial Approach

I first thought about reversing the whole list and interleaving the reversed list with the original list.

I then moved toward counting the nodes, splitting around the halfway point, keeping the first half, and somehow obtaining nodes from the end for the alternating merge.

## What Was Wrong or Incomplete

Reversing the whole list loses independent access to the original forward order because both ideas refer to the same linked nodes. After reversal, I cannot continue reading `L0, L1, L2...` from the original structure.

Splitting alone was not enough either. The second half still runs from the middle toward the end, but the reorder needs the last node first. The missing step was reversing only the second half.

## Final Approach

1. Count the nodes.
2. Keep `Math.ceil(count / 2)` nodes in the first half, so the first half holds the extra node when the length is odd.
3. Disconnect the two halves.
4. Reverse the second half in place using pointer reversal.
5. Insert one node from the reversed half after each node from the first half.

## Code

```js
var reorderList = function (head) {
    if (!head || !head.next) return;

    let count = 0;
    let current = head;

    while (current) {
        count++;
        current = current.next;
    }

    const firstHalfLength = Math.ceil(count / 2);
    let firstHalfTail = head;

    for (let index = 1; index < firstHalfLength; index++) {
        firstHalfTail = firstHalfTail.next;
    }

    let second = firstHalfTail.next;
    firstHalfTail.next = null;

    let reversedSecond = null;

    while (second) {
        const next = second.next;
        second.next = reversedSecond;
        reversedSecond = second;
        second = next;
    }

    let first = head;

    while (reversedSecond) {
        const firstNext = first.next;
        const secondNext = reversedSecond.next;

        first.next = reversedSecond;
        reversedSecond.next = firstNext;

        first = firstNext;
        reversedSecond = secondNext;
    }
};
```

The problem modifies the list in place, so returning a result is unnecessary. A return value would not affect the pointer work, but the implementation should follow the void contract consistently.

## Complexity

- Time: **O(n)** — counting, reversing, and merging each process the list linearly.
- Extra Space: **O(1)** — the solution uses only pointer and counter variables.

## Interview Takeaway

When a singly linked list must alternate between its front and back, make the back traversable in the required order: split the list, reverse the second half, and merge alternately. Preserve both traversal paths before reconnecting any nodes.
