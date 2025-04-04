# Lowest Common Ancestor of deepest Leaves
Given the root of a binary tree, return the lowest common ancestor of its deepest leaves.

- The node of a binary tree is a leaf if and only if it has no children
- The depth of the root of the tree is 0. if the depth of a node is d, the depth of each of its children is d + 1.
- The lowest common ancestor of a set S of nodes, is the node A with the largest depth such that every node in S is in the subtree with root A.

**Example1 :-**
![image](https://github.com/user-attachments/assets/7ff5bc8c-ee37-40b8-9168-7fa24847964c)
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4]
Output: [2,7,4]
Explanation: We return the node with value 2, colored in yellow in the diagram.
The nodes coloured in blue are the deepest leaf-nodes of the tree.
Note that nodes 6, 0, and 8 are also leaf nodes, but the depth of them is 2, but the depth of nodes 7 and 4 is 3.
```

**Example2 :-**
```
Input: root = [1]
Output: [1]
Explanation: The root is the deepest node in the tree, and it's the lca of itself.
```

## ✅ Approach: BFS + Iterative LCA

### 🔧 Step-by-step Breakdown:

1. **Level Order Traversal (BFS)**:
   - Use a queue to perform a level-order traversal (BFS).
   - For every level, store the nodes in a vector `v`.
   - When BFS completes, `v` will contain **only the nodes at the deepest level** of the tree.

2. **Finding LCA of Deepest Nodes**:
   - Define a recursive helper function `findlca(root, a, b)` to compute the LCA of any two nodes.
   - Initialize `lca` with the first node from the deepest level.
   - Iterate through the rest of the nodes in `v`, and **update `lca` by finding the LCA of the current `lca` and the next node**.

3. **Return the Final LCA**:
   - After processing all deepest leaf nodes, the `lca` variable will hold the Lowest Common Ancestor of all deepest leaves.

---

## 🧠 Why This Works:

- BFS guarantees that the last level we process is the **deepest level**.
- The LCA of all nodes in that deepest level is their **lowest shared ancestor**.
- The recursive `findlca()` function works in **O(n)** time for each pair, and the loop runs `k-1` times (where `k` is number of deepest nodes), resulting in an overall acceptable complexity for most cases.

---

## 🕒 Time and Space Complexity:

- **Time Complexity:**
  - BFS traversal: O(n)
  - LCA calculations: O(k × n) in the worst case (where `k` is the number of deepest leaves)
- **Space Complexity:**
  - Queue for BFS: O(w) (width of the tree)
  - Vector to store deepest leaves: O(k)
  - Recursive stack for LCA: O(h) (height of the tree)
 
***Code :-***

``` cpp
class Solution {
public:
    TreeNode* findlca(TreeNode* root, TreeNode* a, TreeNode* b) {
        if (!root || root == a || root == b) {
            return root;
        }
        TreeNode* left = findlca(root->left, a, b);
        TreeNode* right = findlca(root->right, a, b);
        if (left && right) return root;
        return left ? left : right;
    }

    TreeNode* lcaDeepestLeaves(TreeNode* root) {
        if (root == nullptr) return nullptr;

        queue<TreeNode*> q;
        q.push(root);
        vector<TreeNode*> v;

        while (!q.empty()) {
            int size = q.size();
            v.clear(); // [FIX] Clear the vector for each level
            for (int i = 0; i < size; i++) {
                TreeNode* tempv = q.front();
                q.pop();
                if (tempv->left) q.push(tempv->left);
                if (tempv->right) q.push(tempv->right);
                v.push_back(tempv);
            }
        }

        // [FIX] Correctly compute the LCA
        TreeNode* lca = v[0];
        for (int i = 1; i < v.size(); i++) {
            lca = findlca(root, lca, v[i]);
        }

        return lca; // [FIX] return final LCA instead of tempans
    }
};
```


Feel Free to ask 😊
