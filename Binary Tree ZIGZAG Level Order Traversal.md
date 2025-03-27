# Binary Tree ZIGZAG Level Order Traversal

**Statement** :- Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

**Example** :- 
![image](https://github.com/user-attachments/assets/2d10e03a-4526-4718-9f1b-f5fa37c21d13)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```

### My first approach(although wrong 🥲)

``` c++
class Solution {
public:
vector<vector<int>> ans;
string s = "left";
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if(root == nullptr)
        {
            return ans;
        }
        vector<int> temp;
        temp.push_back(root->val)        
        ans.push_back(temp;);
        if(s == 'left')
        {
            s = right;
            zigzagLevelOrder(root->left);
        }
        else
        {
            s = left;
            zigzagLevelOrder(root->right);
        }
        return ans;  
    }
};
```

**After reviwing it I changed my apprach and thought for the solution with the usage of queue like the levelwise traversal**
*Step1* :- I made a empty queue 
*Step2* :- Stored the top of the queue in the temp variable and then poped it, after that pushing the left and right subtress if they exist
*Step3* :- if the traversal need to be start from the right the reverse the queue and store the ans else continue and at the end of each loop change the direction

**Final Code** :- 

``` c++
class Solution {
public:
    vector<vector<int>> ans;
    string s = "left";

    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if (root == nullptr)
            return ans;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int size = q.size();
            vector<int> tempv; // Reset tempv for every level

            for (int i = 0; i < size; i++) {
                TreeNode* temp = q.front();
                q.pop();
                tempv.push_back(temp->val);
                
                if (temp->left) q.push(temp->left);
                if (temp->right) q.push(temp->right);
            }

            if (s == "right") {
                reverse(tempv.begin(), tempv.end()); 
            }
            ans.push_back(tempv);
            if (s == "right") {
                s = "left";
            } else {
                s = "right";
            }
        }
        return ans;
    }
};
```

Thanks for visiting, 😊 Feel free to contact
