```c++
struct Item {
    int value;
    Item* prev;
};

class MyStack {
private: 
    Item* item;

public:
    MyStack() {
        this->item = NULL;
    }
    
    void push(int x) {
        Item* item = new Item();
        item->value = x;
        item->prev = this->item;
        this->item = item;
    }
    
    int pop() {
        Item* cur = this->item;
        int value = cur->value;
        this->item = cur->prev;
        delete cur;
        return value;
    }
    
    int top() {
        return this->item->value;
    }
    
    bool empty() {
        return this->item == NULL;
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
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
