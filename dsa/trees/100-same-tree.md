# 100. Same Tree

## Pattern

Trees / DFS / BFS

## Day 22 Learning Progression

The first solution used recursive DFS and compared corresponding nodes in both trees.

### Recursive DFS

```js
var isSameTree = function(p, q) {
    if (!p && !q) return true;
    if (p?.val !== q?.val) return false;

    return isSameTree(p.left, q.left) &&
           isSameTree(p.right, q.right);
};
```

Key idea:

- If both nodes are missing, that position matches.
- If one node is missing or values differ, the trees differ.
- Otherwise compare the left pair and right pair recursively.

Time: **O(n)** in the worst case.

Space: **O(h)** recursion stack, where `h` is tree height.

### Iterative BFS

The iterative solution used a queue and compared corresponding nodes from both trees together.

The first implementation used repeated `queue.shift()`. The comparison logic was correct, but repeated `shift()` can add array re-indexing overhead in JavaScript.

A queue-index version keeps the traversal O(n):

```js
var isSameTree = function(p, q) {
    const queue = [[p, q]];
    let i = 0;

    while (i < queue.length) {
        const [node1, node2] = queue[i++];

        if (!node1 && !node2) continue;
        if (!node1 || !node2) return false;
        if (node1.val !== node2.val) return false;

        queue.push([node1.left, node2.left]);
        queue.push([node1.right, node2.right]);
    }

    return true;
};
```

With an efficient queue:

- Time: **O(n)**
- Space: **O(w)**, where `w` is maximum tree width.

## Interview Takeaway

Matching values are not enough. The two trees must have the same values at the same structural positions.
