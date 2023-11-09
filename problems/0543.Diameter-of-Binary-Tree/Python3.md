# [543. Diameter of Binary Tree]()

## Solution 1: Postorder Traversal with Depth-First Search

### Intuition

Visit the nodes via postorder traversal (left, right, then root). For each node, we first get the height of the left and right subtrees (using depth-first search), and the diameter can be calculated as the sum of both heights. Then we just update a global variable if a larger `diameter` is seen.

### Approach

1. Initialize a global variable `diameter` as `0`.
1. Define a recursive depth-first search function `getHeight()` to get the maximum height of a tree.
1. In the recursive function:
   - Define base case when a leaf node (null) is reached and return `0`.
   - Call depth-first search recursively on the `root.left` and `root.right` subtrees.
   - Update `diameter` as `max(diameter, left + right)`.
   - Return `max(left, right) + 1`.
1. Finally, return `diameter`.

### Code

```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.diameter = 0
        self.getHeight(root)
        return self.diameter

    def getHeight(self, root: Optional[TreeNode]) -> int:
        if root is None: return 0
        left = self.getHeight(root.left)
        right = self.getHeight(root.right)
        self.diameter = max(self.diameter, left + right)
        return max(left, right) + 1
```

### Complexity

- Time complexity: $O(n)$

  Each node is accessed once.

- Space complexity: $O(n)$

  Recursive call stack requires a size equals to the maximum height of the tree, which is in the worst-case the total number of nodes when the tree is degenerate (every parent node only has one child node).
