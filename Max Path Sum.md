# Binary Tree Maximum Path Sum

## Problem Statement
Given the root of a binary tree, return the maximum path sum. A path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not necessarily pass through the root.

## Method of Approach

### Step 1: Define the Problem Clearly
- Input: Root node of a binary tree
- Output: Maximum path sum from any node to any node

### Step 2: Approach Explanation
1. **Recursive Traversal**: Perform a post-order traversal using recursion.
2. **Calculate Left and Right Path Sums**: Recursively calculate the maximum path sum from left and right subtrees.
3. **Ignore Negative Paths**: Use `max(0, left)` and `max(0, right)` to ensure we do not include negative path sums.
4. **Update Maximum Path Sum**: For every node, check the path sum including both left and right children and update the global maximum.
5. **Return Path Sum for Recursion**: Return the maximum path sum including the current node and one of its children.

### Step 3: Edge Cases
- Single node tree
- All nodes with negative values
- Balanced and unbalanced trees

## Solution Code
```cpp
#include <climits>

struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution {
public:
    int maxPathSum(TreeNode* root) {
       int maxi = INT_MIN;
       maxreturn(root, maxi);
       return maxi;
    }
    int maxreturn(TreeNode* root, int &maxi) {
        if(root == nullptr) {
            return 0;
        }

        int left = max(0, maxreturn(root->left, maxi));
        int right = max(0, maxreturn(root->right, maxi));
        maxi = max(maxi, left + right + root->val);
        return max(left, right) + root->val;
    }
};
```

## Complexity Analysis
- **Time Complexity**: \(O(N)\), where N is the number of nodes in the tree. Each node is visited once.
- **Space Complexity**: \(O(H)\), where H is the height of the tree. This accounts for the recursive stack.

## Conclusion
This solution is optimal for finding the maximum path sum in a binary tree using a simple and efficient recursive approach. Contributions and suggestions are welcome!

