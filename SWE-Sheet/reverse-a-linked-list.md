## Question: "reverse-a-linked-list/: Problem Statement:
Problem Statement: Given the head of a singly linked list, write a program to reverse the linked list, and return the head pointer to the reversed list."

## Approach 1: Brute Force
- **Explanation:** Start from the last node of the list and move towards the beginning. Keep swapping the values of the current node with the value of the first node. Repeat this process until you reach the head of the list.
- **C++ Code:**
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *temp, *prev = NULL;
        while (head) {
            temp = head->next;
            head->next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
};
```
- **Time and Space Complexity Analysis:**
  - Time Complexity: O(n), where n is the number of nodes in the linked list.
  - Space Complexity: O(1), as no additional space is allocated.

## Approach 2: Optimized Solution using Two Pointers
- **Explanation:** This approach involves using two pointers, `curr` and `prev`, to keep track of the current node and the previous node, respectively. The `curr` pointer moves forward through the list, while the `prev` pointer is updated to point to the `curr` node. The `curr` pointer is then updated to point to the next node in the list, thereby effectively reversing the order of the nodes.
- **C++ Code:**
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *curr = head, *prev = NULL;
        while (curr) {
            ListNode *next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
};
```
- **Time and Space Complexity Analysis:**
  - Time Complexity: O(n), where n is the number of nodes in the linked list.
  - Space Complexity: O(1), as no additional space is allocated.

## Approach 3: Recursive Solution
- **Explanation:** This approach utilizes the recursive nature of linked lists. The `reverseList` function is defined to take a `ListNode*` as input and return a `ListNode*`. The function first checks if the input node is `NULL` or if it is the last node in the list. If either of these conditions is met, the function simply returns the input node. Otherwise, the function recursively calls itself on the `next` node of the input node. Once the recursive call returns, the function sets the `next` pointer of the input node to `NULL` and sets the `next` pointer of the recursive call's return value to point to the input node. The function then returns the recursive call's return value, which is the reversed list.
- **C++ Code:**
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode* newHead = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return newHead;
    }
};
```
- **Time and Space Complexity Analysis:**
  - Time Complexity: O(n), where n is the number of nodes in the linked list.
  - Space Complexity: O(n), as the recursion stack can grow to a depth of n.

## Approach 4: Solution using Stack
- **Explanation:** This approach utilizes a stack to reverse the list. The function `reverseList` takes a `ListNode*` as input and returns a `ListNode*`. The function first creates a stack. Then, it iterates through the input list, pushing each node onto the stack. Once the end of the list is reached, the function pops nodes from the stack, building the reversed list as it does so.
- **C++ Code:**
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        stack<ListNode*> stack;
        while (head) {
            stack.push(head);
            head = head->next;
        }
        ListNode *newHead = NULL;
        while (!stack.empty()) {
            ListNode *node = stack.top();
            stack.pop();
            node->next = newHead;
            newHead = node;
        }
        return newHead;
    }
};
```
- **Time and Space Complexity Analysis:**
  - Time Complexity: O(n), where n is the number of nodes in the linked list.
  - Space Complexity: O(n), as the stack can grow to a size of n.**Question**: "reverse-a-linked-list/: Problem Statement: Problem Statement: Given the head of a singly linked list, write a program to reverse the linked list, and return the head pointer to the reversed list."

**Approach 1: Iterative Approach**

**Explanation**: 
This approach iterates through the list and reverses the pointers of each node. It maintains three pointers: `prev`, `curr`, and `next`. The `prev` pointer points to the previous node, `curr` points to the current node, and `next` points to the next node. In each iteration, we update the `prev` and `next` pointers of the `curr` node and move to the next node. Finally, we return the `prev` pointer, which points to the new head of the reversed list.

**Approach 1 Code**:

```cpp
struct ListNode {
  int val;
  ListNode *next;
  ListNode(int x) : val(x), next(NULL) {}
};

ListNode* reverseList(ListNode* head) {
  ListNode *prev = NULL, *curr = head, *next = NULL;
  while (curr) {
    next = curr->next;
    curr->next = prev;
    prev = curr;
    curr = next;
  }
  return prev;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* Time complexity: O(n), where n is the number of nodes in the linked list.
* Space complexity: O(1), as we only use extra pointers.

**Approach 2: Recursive Approach**

**Explanation**: 
This approach uses recursion to reverse the linked list. It takes the head of the list as an argument and returns the new head of the reversed list. If the list is empty or the next node of the head is null, we return the head. Otherwise, we call the function recursively on the next node and set the next node of the current node to the previous node. Finally, we update the head of the list to point to the new reversed list.

**Approach 2 Code**:

```cpp
struct ListNode {
  int val;
  ListNode *next;
  ListNode(int x) : val(x), next(NULL) {}
};

ListNode* reverseList(ListNode* head) {
  if (!head || !head->next) return head;
  ListNode* reversedList = reverseList(head->next);
  head->next->next = head;
  head->next = NULL;
  return reversedList;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* Time complexity: O(n), where n is the number of nodes in the linked list.
* Space complexity: O(n), as we use the recursion stack.