# 206. Reverse Linked List

**Pattern:** Linked List / Pointer Reversal

**Difficulty:** Easy

**LeetCode:** https://leetcode.com/problems/reverse-linked-list/

## Problem

Given the head of a singly linked list, reverse the list and return its new head.

## Linked List Fundamentals

Each node stores a value and a `next` reference to another node.

Unlike an array, a linked list does not provide direct indexed access. Reaching a position requires following references from the head, so access by position is O(n).

Insertion or deletion is O(1) when the required node or predecessor reference is already available. Finding that reference can take O(n). In a singly linked list, deleting the tail is O(n) if its predecessor must be found.

## Recognition Clues

- The input is the head of a singly linked list.
- The links between existing nodes must be reversed.
- The expected extra-space complexity is O(1).
- Pointer order matters because changing `next` can disconnect the unprocessed list.

## My Initial Approach

I first created a new node for each node in the original list and inserted it at the front of a new list:

```js
var reverseList = function (head) {
    let reverseLinkedList = null;

    while (head) {
        reverseLinkedList = new ListNode(head.val, reverseLinkedList);
        head = head.next;
    }

    return reverseLinkedList;
};
```

This correctly returns the values in reverse order, but it creates n new nodes.

## Second Attempt

I then replaced `new ListNode` with object spread:

```js
var reverseList = function (head) {
    let reverseLinkedList = null;

    while (head) {
        const temp = { ...head };
        temp.next = reverseLinkedList;
        reverseLinkedList = temp;
        head = head.next;
    }

    return reverseLinkedList;
};
```

## What Was Wrong or Incomplete

Object spread still creates a new object for every node. Both early approaches therefore:

- Use O(n) extra space.
- Build a copied list instead of reversing the original nodes.
- Miss the in-place pointer-reversal requirement.

The important risk in an in-place solution is losing the rest of the list after overwriting `head.next`.

## Final Approach

Maintain two pointers:

- `previous` points to the already reversed portion.
- `head` points to the current node.

Before reversing the current link, save `head.next`. Then point the current node backward and advance both pointers.

## Code

```js
var reverseList = function (head) {
    let previous = null;
    let next;

    while (head) {
        next = head.next;
        head.next = previous;
        previous = head;
        head = next;
    }

    return previous;
};
```

## Complexity

- Time: **O(n)** — each node is visited once.
- Extra Space: **O(1)** — only pointer variables are used.

The initial and object-spread approaches both take O(n) time and O(n) extra space.

## Interview Takeaway

The critical sequence is:

1. Save the next node.
2. Reverse the current node's `next` reference.
3. Advance `previous`.
4. Advance `head` using the saved reference.

When changing linked-list pointers in place, preserve access to the unprocessed nodes before breaking the original link.
