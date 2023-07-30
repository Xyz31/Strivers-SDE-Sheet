# Height of a Binary Tree


# Approach - I
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

    int maxDepth(TreeNode* root) {
        //Day-18 Binary Trees Q-2

        int ans=0;
        if(!root) return ans;
        
        //Iterative traversal level wise BFS 
        queue<TreeNode *> levels;
        levels.push(root);
        while(!levels.empty()){
            int size=levels.size();
            for(int i=0;i<size;i++){
                TreeNode *node=levels.front();
                levels.pop();
                if(node->left){
                    levels.push(node->left);
                    
                }
                if(node->right){
                    levels.push(node->right);
                }
            }
            ans++;
        }

        return ans;
    }
};

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
    int DFS(TreeNode *root){
        if(!root){
            return 0;
        }
        int lh=DFS(root->left);
        int rh=DFS(root->right);

        return 1+max(lh,rh);
    }
    int maxDepth(TreeNode* root) {
        //Day-18 Binary Trees Q-2

        int ans=0;
        if(!root) return ans;

        //recursive traversal depth wise DFS
        ans=DFS(root);
        return ans;
    }
};

```