# Level Order Traversal of a Binary Tree


# Approach - I
```cpp



```

# Approach - II
```cpp

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        //Day-18 Binary Trees Q-1
        //BFS problem 

        if(!root){
            return {};
        }
        
        queue<TreeNode *> qu;
        qu.push(root);
        vector<vector<int>> ans;

        while(!qu.empty()){
            
            vector<int> level;
            int size=qu.size();

            for(int i=0;i<size;i++){
                TreeNode *node=qu.front();
                qu.pop();
            if(node->left){
                
                qu.push(node->left);
            }
            if(node->right){
                
                qu.push(node->right);
            }
            level.push_back(node->val);
            }
            ans.push_back(level);
        }
        return ans;
    }
};

```