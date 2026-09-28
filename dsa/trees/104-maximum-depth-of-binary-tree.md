# 104. Maximum Depth of Binary Tree

## Pattern

Trees / Depth-First Search (DFS) and Breadth-First Search (BFS).

## Recognition Clues

Find the longest root-to-leaf path in nodes. Each subtree has the same depth problem; alternatively, counting complete levels gives the maximum depth.

## Initial Approach

Pass the current depth to children, increment it by one, and update an external maximum. This was a valid DFS approach. The term "deep binary search" was corrected to Depth-First Search.

## Recursive DFS — Completed on Day 20

Return the subtree depth directly instead of maintaining an external maximum. A missing node has depth 0; otherwise return one plus the greater child depth.

```js
const getMaxDepth = (root) => {
    if (!root) return 0;
    const leftDepth = getMaxDepth(root.left);
    const rightDepth = getMaxDepth(root.right);
    return 1 + Math.max(leftDepth, rightDepth);
};

var maxDepth = function(root) {
    return getMaxDepth(root);
};
```

- Time: **O(n)**.
- Extra space: **O(h)** for the recursion stack, where h is tree height; O(n) for a skewed tree and O(log n) for a balanced tree.

## BFS Level-order — Also Completed on Day 20

The submitted version used a queue and manually tracked the next level's node count. Increment the depth once after processing a complete level.

```js
var maxDepth = function(root) {
    if (!root) return 0;
    let queue = [root], maxDepth = 0, node = 1;

    while (queue.length) {
        let currentNode = node;
        node = 0;

        while (currentNode) {
            let shift = queue.shift();
            if (shift?.left) {
                queue.push(shift.left);
                node++;
            }
            if (shift?.right) {
                queue.push(shift.right);
                node++;
            }
            currentNode--;
        }

        maxDepth++;
    }

    return maxDepth;
};
```

- The traversal visits each node once.
- Repeated JavaScript `queue.shift()` can add O(n²) total removal overhead in the worst case. An efficient queue supports O(n) total time.
- Queue space: **O(w)**, where w is maximum tree width.

## Dry Run

For `[3, 9, 20, null, null, 15, 7]`, BFS processes `[3]`, then `[9, 20]`, then `[15, 7]`: three levels, so the answer is 3. Recursive DFS returns the same depth. An empty tree returns 0; a single node returns 1.

## Corrections and Pending Follow-ups

- DFS is a traversal strategy, not a synonym for recursion. Iterative DFS uses a stack; BFS uses a queue.
- Simplifying the manual level counter with a snapshot of `queue.length` was discussed, not implemented.
- Replacing repeated `shift()` with an efficient queue was discussed, not implemented.
- Iterative DFS with node/depth stack entries was discussed but **not implemented**.

## Interview Takeaway

Recursive DFS combines child depths; BFS counts complete levels. Explain the height-versus-width space tradeoff and distinguish the traversal's complexity from the queue implementation's overhead.
