```c++
#include <algorithm>

class Solution {
private:
    vector<int> nums;
    vector<int> temp;
public:
    Solution(vector<int>& nums) {
        this->nums = vector<int>(nums);
        this->temp = vector<int>(nums);
    }
    
    vector<int> reset() {
        return this->nums;
    }
    
    vector<int> shuffle() {
        next_permutation(temp.begin(), temp.end());

        return this->temp;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * vector<int> param_1 = obj->reset();
 * vector<int> param_2 = obj->shuffle();
 */
 ```
 
 ```c++
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
    TreeNode* pruneTree(TreeNode* root) {
        if (root == nullptr) {
            return nullptr;
        }


        root->left = pruneTree(root->left);
        root->right = pruneTree(root->right);

        // leaf node
        if (root->left == nullptr && root->right == nullptr) {
            if (root->val == 0) {
                return nullptr;
            }
            return root;
        }



        return root;
    }
};
```
