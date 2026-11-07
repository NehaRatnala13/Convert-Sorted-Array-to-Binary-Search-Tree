# Convert-Sorted-Array-to-Binary-Search-Tree
Given an integer array `nums` where the elements are sorted in **ascending order**, convert it to a **height-balanced** binary search tree.  A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.
# LeetCode 108: Convert Sorted Array to Binary Search Tree

A clean, efficient Python 3 solution for [LeetCode 108: Convert Sorted Array to Binary Search Tree](https://leetcode.com).

## Problem Description

Given an integer array `nums` where the elements are sorted in **ascending order**, convert it to a **height-balanced** binary search tree.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

### Example
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted.
## Solution Strategy

The algorithm utilizes a **Divide and Conquer** recursive pattern:
1. **Find the Midpoint:** Since the array is already sorted, the absolute middle element (`mid = (left + right) // 2`) is chosen as the root node to guarantee a perfect height balance.
2. **Index Pointers:** Pass `left` and `right` boundary markers to avoid expensive O(N) array slicing overhead operations.
3. **Subtree Construction:** Recursively build the left subtree using elements before the midpoint, and the right subtree using elements after the midpoint.

## Code Implementation

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def sortedArrayToBST(self, nums: list[int]) -> TreeNode | None:
        def build_bst(left: int, right: int) -> TreeNode | None:
            # Base case: invalid range means a leaf node's child pointer is hit
            if left > right:
                return None
            
            # Find midpoint to pick the balance root element
            mid = (left + right) // 2
            root = TreeNode(nums[mid])
            
            # Recursively build out left and right subtrees
            root.left = build_bst(left, mid - 1)
            root.right = build_bst(mid + 1, right)
            
            return root
            
        return build_bst(0, len(nums) - 1)
```

## Complexity Analysis

- **Time Complexity:** $\mathcal{O}(N)$ — The algorithm visits every single integer element in the input array exactly once to map out the tree nodes.
- **Space Complexity:** $\mathcal{O}(\log N)$ — Because the tree is height-balanced, the implicit recursion system call stack depth is bounded by $\log N$.
