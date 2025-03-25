# Balanced Binart Tree

Given a binary tree, determine if it is height-balanced.

![image](https://github.com/user-attachments/assets/53f577a2-2f7c-4532-b140-20993ba157fc)
```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

So this is how I approached :- 

``` cpp
class Solution {
public:
    int checkheight(TreeNode *root) {
        if (root == nullptr)
            return 0; // Return 0 for null node instead of -1

        int leftheight = checkheight(root->left);
        if (leftheight == -1) return -1;

        int rightheight = checkheight(root->right);
        if (rightheight == -1) return -1;

        if (abs(leftheight - rightheight) > 1) 
            return -1; // Return -1 if unbalanced

        return 1 + max(leftheight, rightheight); // Return height
    }

    bool isBalanced(TreeNode* root) {
        return checkheight(root) != -1; // Return true if balanced
    }
};
```

Thnks for visiting 😊
Feel Free to ask answer and correct me 
