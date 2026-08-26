# 141. Linked List Cycle

**Pattern:** Linked List + Hashing

**Difficulty:** Easy

**LeetCode:** https://leetcode.com/problems/linked-list-cycle/

## Problem

Determine whether a singly linked list contains a cycle.

## Recognition Clues

- Following `next` references may return to a previously visited node.
- Traversal may never reach `null` when a cycle exists.
- Repeated node identity, rather than repeated node value, proves a cycle.

## My Initial Approach

Traverse from `head`, use a `Map` to store each node and its position, and return `true` when a node repeats. If traversal reaches `null`, return `false`.

## What Was Wrong or Incomplete

The approach was correct, but storing each node's position was unnecessary. Cycle detection only needs to know whether a node reference has already appeared, so a `Set` communicates the intention more directly.

Node references must be stored instead of node values because different nodes can contain the same value without forming a cycle.

## Final Approach

Traverse the list while storing every visited node reference in a `Set`.

- If the current node is already in the set, return `true`.
- Otherwise add it and continue to `head.next`.
- If traversal reaches `null`, return `false`.

## Code

```js
var hasCycle = function (head) {
    const set = new Set();

    while (head) {
        if (set.has(head)) return true;

        set.add(head);
        head = head.next;
    }

    return false;
};
```

## Complexity

- Time: **O(n)** — each distinct node is visited once before traversal ends or a repeat is found.
- Extra Space: **O(n)** — the set can contain every node.

## Interview Takeaway

Repeated values do not prove that a linked list has a cycle; revisiting the same node reference does.

The Set-based solution is the completed approach. Detecting a cycle with O(1) extra space remains an optimization to learn and has not yet been completed.
