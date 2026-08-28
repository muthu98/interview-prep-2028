# 138. Copy List with Random Pointer

**Pattern:** Linked List / Hash Map and Interleaving

**Difficulty:** Medium

**LeetCode:** https://leetcode.com/problems/copy-list-with-random-pointer/

## Problem

Create a deep copy of a linked list where every node has both `next` and `random` references. Each copied reference must point only to copied nodes, never to the original list.

## Recognition Clues

- Nodes contain arbitrary references in addition to `next`.
- Repeated values cannot identify which node a pointer targets.
- A deep copy must preserve relationships between nodes.
- The straightforward solution needs a mapping from each original identity to its copied identity.
- If O(1) extra space is requested, temporarily place each copy beside its original.

## My Initial Thinking

I first thought about shallow copy versus deep copy and tried object spread:

```js
const copy = { ...node };
```

This creates a new outer object, but `copy.next` and `copy.random` still point to original node objects. It does not deep-copy the linked structure.

I then proposed a two-pass Map from each original node to its copy. The idea was correct, but the first implementation created a separate shallow-copied head and later changed original nodes while trying to connect the copied list. That produced more than one copy source and broke the requirement that the original list remain unchanged.

## Baseline: Two-Pass Map

The Map is the single source of every copied node:

1. Traverse the original list and create one new node for each original.
2. Store `originalNode -> copiedNode` in a Map.
3. Traverse again and translate both references through the Map.
4. Return the mapped copy of `head`.

```js
var copyRandomList = function (head) {
    if (!head) return null;

    const copies = new Map();
    let current = head;

    while (current) {
        copies.set(current, new Node(current.val));
        current = current.next;
    }

    current = head;

    while (current) {
        const copy = copies.get(current);
        copy.next = current.next ? copies.get(current.next) : null;
        copy.random = current.random ? copies.get(current.random) : null;
        current = current.next;
    }

    return copies.get(head);
};
```

### Complexity

- Time: **O(n)** — two linear traversals.
- Extra Space: **O(n)** — one Map entry and one copied node per original node.

## Optimization: Interleave the Copies

To remove the Map, temporarily make each copy the next node after its original:

```text
A → B → C

A → A' → B → B' → C → C'
```

Now every original-to-copy lookup is encoded in the list itself: the copy of `original` is `original.next`.

### Step 1: Insert Each Copy

```js
let current = head;

while (current) {
    const copy = new Node(current.val, current.next, null);
    current.next = copy;
    current = copy.next;
}
```

### Step 2: Connect Random References

If an original node points randomly to `X`, the copied target is immediately after `X`:

```js
current.next.random = current.random ? current.random.next : null;
```

I initially explored a flag-based traversal to locate random targets. The interleaved structure makes that search unnecessary and keeps this phase linear.

### Step 3: Separate and Restore

Walk original and copied nodes together. Restore each original `next` and build the copied `next` chain. A dummy tail can make separation work, but direct pointer restoration is enough.

## Final O(1)-Extra-Space Code

```js
var copyRandomList = function (head) {
    if (!head) return null;

    let current = head;

    while (current) {
        const copy = new Node(current.val, current.next, null);
        current.next = copy;
        current = copy.next;
    }

    current = head;

    while (current) {
        const copy = current.next;
        copy.random = current.random ? current.random.next : null;
        current = copy.next;
    }

    const copiedHead = head.next;
    current = head;

    while (current) {
        const copy = current.next;
        const nextOriginal = copy.next;

        current.next = nextOriginal;
        copy.next = nextOriginal ? nextOriginal.next : null;
        current = nextOriginal;
    }

    return copiedHead;
};
```

### Complexity

- Time: **O(n)** — three linear traversals.
- Extra Space: **O(1)** — excluding the required copied nodes.

## Interview Takeaway

Deep copying means reproducing object identity relationships, not just copying field values. Start with the original-to-copy Map because it makes the invariant explicit. For the space optimization, interleave nodes so `original.next` acts as the lookup, use `original.random.next` for the copied random target, and restore the input while separating the result.
