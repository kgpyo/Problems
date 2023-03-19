```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
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
    TreeNode* sortedListToBST(ListNode* head) {
        if (head == NULL) {
            return NULL;
        }

        if (head->next == NULL) {
            return new TreeNode(head->val);
        }

        if (head->next->next == NULL) {
            TreeNode* node = new TreeNode(head->val);
            TreeNode* parent = new TreeNode(head->next->val);
            parent->left = node;
            return parent;
        }

        ListNode* fast = head;
        ListNode* slow = head;
        ListNode* prev = NULL;
        while(fast != NULL && fast->next != NULL) {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        if (prev != NULL) {
            prev->next = NULL;
        }
        TreeNode* parent = new TreeNode(slow->val); 
        parent->left = sortedListToBST(head);
        parent->right = sortedListToBST(slow->next);

        return parent;
    }
};
```


```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
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
    TreeNode* sortedListToBST(ListNode* head) {
        if (head == NULL) {
            return NULL;
        }

        if (head->next == NULL) {
            return new TreeNode(head->val);
        }

        if (head->next->next == NULL) {
            TreeNode* node = new TreeNode(head->val);
            TreeNode* parent = new TreeNode(head->next->val);
            parent->left = node;
            return parent;
        }

        ListNode* fast = head;
        ListNode* slow = head;
        ListNode* prev = NULL;
        while(fast != NULL && fast->next != NULL) {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        if (prev != NULL) {
            prev->next = NULL;
        }
        TreeNode* parent = new TreeNode(slow->val); 
        parent->left = sortedListToBST(head);
        parent->right = sortedListToBST(slow->next);

        return parent;
    }
};
```
