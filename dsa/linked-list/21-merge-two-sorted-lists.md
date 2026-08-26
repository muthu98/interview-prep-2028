# 21. Merge Two Sorted Lists

**Pattern:** Linked List / Pointer Merge

**Difficulty:** Easy

**LeetCode:** https://leetcode.com/problems/merge-two-sorted-lists/

## Problem

Merge two sorted linked lists into one sorted list and return its head.

## Recognition Clues

- Both input linked lists are already sorted.
- Compare the current node from each list.
- Advance only the list whose node was selected.
- Reconnect existing nodes to achieve O(1) extra space.

## My Initial Approach

I compared `list1.val` and `list2.val`, selected the smaller value, and used `tail` to build the merged list.

My first implementation copied every selected node with object spread:

```js
const temp = { ...list1 };
```

or:

```js
const temp = { ...list2 };
```

I preserved the first selected node separately and attached the remaining list after one input became empty.

## What Was Wrong or Incomplete

The merge order was correct, but object spread created a new object for every selected node while both lists were non-empty. The result also mixed copied objects with original nodes.

Renaming `result` to `tail` and `resultValue` to `mergedHead` improved clarity, but did not fix the space usage because the object spreads were still present.

To achieve O(1) extra space, the selected existing node must be connected directly to `tail`.

## Final Approach

- Return the other list immediately if either input is empty.
- Compare the current values while both lists contain nodes.
- Use the first selected existing node as both `mergedHead` and `tail`.
- Connect each later selected node directly to `tail.next`.
- Advance only the list from which the node was selected.
- Attach the remaining portion of the non-empty list after the loop.

## Code

```js
var mergeTwoLists = function (list1, list2) {
    if (!list1) return list2;
    if (!list2) return list1;

    let tail = null;
    let mergedHead;

    while (list1 && list2) {
        if (list1.val > list2.val) {
            if (tail) {
                tail.next = list2;
                tail = tail.next;
            } else {
                tail = list2;
                mergedHead = tail;
            }

            list2 = list2.next;
        } else {
            if (tail) {
                tail.next = list1;
                tail = tail.next;
            } else {
                tail = list1;
                mergedHead = tail;
            }

            list1 = list1.next;
        }
    }

    if (list1) tail.next = list1;
    if (list2) tail.next = list2;

    return mergedHead;
};
```

## Complexity

- Time: **O(n + m)** — each node is processed at most once.
- Extra Space: **O(1)** — existing nodes are reused and only pointer variables are stored.

The object-spread version used O(n + m) extra space in the worst case because it could copy nearly every node before attaching the remaining original nodes.

## Interview Takeaway

Use one pointer to preserve the merged head and another to track the tail. When an interview asks for an in-place linked-list merge, clearer variable names alone do not improve space complexity—the implementation must reconnect the existing nodes instead of copying them.
