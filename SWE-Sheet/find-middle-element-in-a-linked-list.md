**Question**: "find-middle-element-in-a-linked-list/: Problem Statement: Given the head of a linked list of integers, determine the middle node of the linked list. However, if the linked list has an even number of nodes, return the second middle node."

**Approach 1: Brute Force** Explanation: This is a straightforward approach that iterates through the entire linked list twice. In the first pass, we count the number of nodes in the linked list, and in the second pass, we find the middle node by iterating to the node at that position.

**Approach 1 Code**:
```cpp
struct ListNode {
  int val;
  ListNode *next;
  ListNode(int x) : val(x), next(NULL) {}
};

ListNode* findMiddleBruteForce(ListNode* head) {
  int count = 0;
  ListNode* tmp = head;
  while (tmp) {
    count++;
    tmp = tmp->next;
  }
  int middle = count / 2;
  tmp = head;
  while (middle--) {
    tmp = tmp->next;
  }
  return tmp;
}
```

**Time and Space Complexity Analysis for Approach 1**: The time complexity is O(n), where n is the number of nodes in the linked list, since we iterate through the entire linked list twice. The space complexity is O(1), as we only use a constant amount of extra space.

**Approach 2: Optimized using Two Pointers**
Explanation: This approach uses two pointers, 'slow' and 'fast', which advance at different rates. The 'slow' pointer advances by one node at a time, while the 'fast' pointer advances by two nodes at a time. When the 'fast' pointer reaches the end of the linked list, the 'slow' pointer will be at the middle node.

**Approach 2 Code**:
```cpp
ListNode* findMiddleTwoPointers(ListNode* head) {
  ListNode* slow = head, *fast = head;
  while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
  }
  return slow;
}
```

**Time and Space Complexity Analysis for Approach 2**: The time complexity is O(n), where n is the number of nodes in the linked list, as both pointers traverse the entire linked list. The space complexity is O(1), as we only use a constant amount of extra space.

**Approach 3: Recursive**
Explanation: This approach uses recursion to find the middle node of the linked list. The function takes the head of the linked list and returns the middle node. If the linked list is empty, the function returns NULL. If the linked list has only one node, the function returns the single node. Otherwise, the function calls itself on the second half of the linked list (i.e., the node after the middle node) and returns the middle node of the second half.

**Approach 3 Code**:
```cpp
ListNode* findMiddleRecursive(ListNode* head) {
  if (!head || !head->next) {
    return head;
  }
  ListNode* slow = head, *fast = head;
  while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
  }
  return slow;
}
```

**Time and Space Complexity Analysis for Approach 3**: The time complexity is O(log n), where n is the number of nodes in the linked list, as the function calls itself on the second half of the linked list until the base case is reached. The space complexity is O(n), as the function calls itself recursively and stores the recursive calls on the call stack.**Question**: "find-middle-element-in-a-linked-list/: Problem Statement: Given the head of a linked list of integers, determine the middle node of the linked list. However, if the linked list has an even number of nodes, return the second middle node."

**Approach 1: Brute Force (Linear Search)**
- Traverse the linked list and count the number of nodes.
- If the number of nodes is odd, return the node at position (count % 2 == 1 ? count / 2 + 1 : count / 2).
- If the number of nodes is even, return the node at position (count / 2).
- Time Complexity: O(n) for the traversal and O(1) for finding the middle, making it O(n).
- Space Complexity: O(1).

```cpp
ListNode* findMiddleNode(ListNode* head) {
  int count = 0;
  ListNode* curr = head;
  while (curr) {
    count++;
    curr = curr->next;
  }
  int mid = count % 2 == 1 ? count / 2 + 1 : count / 2;
  curr = head;
  while (mid > 1) {
    curr = curr->next;
    mid--;
  }
  return curr;
}
```

**Approach 2: Fast and Slow Pointers (Two Pointers)**
- Create two pointers, slow and fast, both pointing to the head of the linked list.
- Move the fast pointer two steps at a time while moving the slow pointer one step at a time.
- When the fast pointer reaches the end of the linked list, the slow pointer will be at the middle node.
- Time Complexity: O(n), where n is the number of nodes in the linked list.
- Space Complexity: O(1).

```cpp
ListNode* findMiddleNode(ListNode* head) {
  ListNode* slow = head;
  ListNode* fast = head;
  while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
  }
  return slow;
}
```

**Approach 3: Bitwise Operations**
- Count the number of nodes in the linked list by traversing it once.
- Use bitwise operators to find the middle position.
- Example: If the number of nodes is 7, then the middle position is 7 >> 1 = 3.
- Time Complexity: O(n) for the traversal and O(1) for the bitwise operation, making it O(n).
- Space Complexity: O(1).

```cpp
ListNode* findMiddleNode(ListNode* head) {
  int count = 0;
  ListNode* curr = head;
  while (curr) {
    count++;
    curr = curr->next;
  }
  int mid = count >> 1;
  curr = head;
  while (mid > 0) {
    curr = curr->next;
    mid--;
  }
  return curr;
}
```