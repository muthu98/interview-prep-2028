# 226. Invert Binary Tree

## Pattern and Recognition Clues

Trees / DFS / BFS. Mirror a binary tree by swapping the left and right children of every node.

## Day 21 — Completed Work

Completed recursive DFS, iterative BFS with a queue, and iterative DFS with a stack; discussed complexity. The original code and any initial mistakes were not supplied, so the examples below are reference implementations of the completed approaches, not a verbatim transcript.

## Final Approaches and Code

All three mutate the tree and return its root. Handle an empty tree by returning null.

### Recursive DFS

Swap the children, then recursively invert each subtree.

```javascript
function invertTreeRecursive(root) {
  if (!root) return null;
  [root.left, root.right] = [root.right, root.left];
  invertTreeRecursive(root.left);
  invertTreeRecursive(root.right);
  return root;
}
```

### Iterative BFS — Queue

Visit nodes in FIFO order and swap each node's children. This reference uses a linked queue to keep enqueue/dequeue O(1) and live queue storage O(w).

```javascript
function invertTreeBFS(root) {
  if (!root) return null;
  let head = { node: root, next: null };
  let tail = head;
  while (head) {
    const node = head.node;
    head = head.next;
    if (!head) tail = null;
    [node.left, node.right] = [node.right, node.left];
    for (const child of [node.left, node.right]) {
      if (!child) continue;
      const entry = { node: child, next: null };
      if (tail) tail.next = entry;
      else head = entry;
      tail = entry;
    }
  }
  return root;
}
```

### Iterative DFS — Stack

Visit nodes in LIFO order, swap children, and push existing children.

```javascript
function invertTreeDFS(root) {
  if (!root) return null;
  const stack = [root];
  while (stack.length) {
    const node = stack.pop();
    [node.left, node.right] = [node.right, node.left];
    if (node.right) stack.push(node.right);
    if (node.left) stack.push(node.left);
  }
  return root;
}
```

## Complexity

Let n be node count, h tree height, and w maximum width.

| Approach | Time | Auxiliary space |
|---|---|---|
| Recursive DFS | O(n) | O(h) call stack; O(n) for a skewed tree |
| BFS with efficient queue | O(n) | O(w) |
| Iterative DFS | O(n) | O(h) upper bound; O(n) worst case |

Repeated JavaScript array `shift()` can add O(n²) total overhead. An array with a growing head index avoids shifting but retains O(n) array slots unless storage is reclaimed.

## Dry Run and Revision

For [4,2,7,1,3,6,9], swap 4's children, then swap the children of 7 and 2: [4,7,2,9,6,3,1]. Also consider empty, single-node, and skewed trees.

Interview takeaway: recursion and an explicit stack both implement DFS; BFS uses a queue. Swap references, not just values. Completing iterative DFS here does not imply completing the pending iterative depth solution for LeetCode 104.

