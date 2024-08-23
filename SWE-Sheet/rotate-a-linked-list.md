## Question:
Rotate a Linked List/: Problem Statement: Given the head of a linked list, rotate the list to the right by k places.

## Approach 1: Brute Force

### Explanation:
This approach involves iterating through the linked list k times, where each iteration, we move the last node to the front.

### Approach 1 Code:
```cpp
ListNode* rotateRight(ListNode* head, int k) {
  if (!head || !head->next) return head;
  ListNode* curr = head;
  int len = 1;
  while (curr->next) {
    curr = curr->next;
    len++;
  }
  k %= len;
  if (k == 0) return head;
  curr->next = head;
  for (int i = 0; i < len - k; i++) curr = curr->next;
  head = curr->next;
  curr->next = nullptr;
  return head;
}
```

### Time and Space Complexity Analysis for Approach 1:
- **Time Complexity**: O(N * k), where N is the number of nodes in the linked list.
- **Space Complexity**: O(1), as no additional space is required.

## Approach 2: Optimized Using Two Pointers

### Explanation:
This approach uses two pointers, slow and fast, to traverse the list. We move fast k steps ahead of slow. When fast reaches the end, we move slow to the next node. We repeat this process until fast reaches the beginning. At that point, slow will be pointing to the new head of the rotated list.

### Approach 2 Code:
```cpp
ListNode* rotateRight(ListNode* head, int k) {
  if (!head || !head->next) return head;
  ListNode* slow = head;
  ListNode* fast = head;
  for (int i = 0; i < k; i++) fast = fast->next;
  while (fast->next) {
    slow = slow->next;
    fast = fast->next;
  }
  fast->next = head;
  head = slow->next;
  slow->next = nullptr;
  return head;
}
```

### Time and Space Complexity Analysis for Approach 2:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list.
- **Space Complexity**: O(1), as no additional space is required.**Question**: rotate-a-linked-list/: Problem Statement: Given the head of a linked list, rotate the list to the right by k places.

**Approach 1: Brute Force Approach**

This approach involves iterating through the linked list k times, moving the last node to the front of the list in each iteration. This approach is straightforward but has a time complexity of O(nk), where n is the number of nodes in the linked list and k is the number of rotations.

**Approach 1 Code**:

```cpp
struct ListNode {
  int val;
  ListNode *next;
  ListNode(int x) : val(x), next(NULL) {}
};

ListNode* rotateRight(ListNode* head, int k) {
  if (!head || !head->next || k == 0) return head;

  ListNode* curr = head;
  int len = 1;
  while (curr->next) {
    curr = curr->next;
    len++;
  }

  k %= len;
  if (k == 0) return head;

  curr->next = head;
  for (int i = 0; i < len - k; i++) {
    curr = curr->next;
  }

  head = curr->next;
  curr->next = NULL;
  return head;
}
```

**Time and Space Complexity Analysis for Approach 1**:

Time Complexity: O(nk)
Space Complexity: O(1)

**Approach 2: Sliding Window Technique**

This approach involves using a sliding window of size k to keep track of the last k nodes in the linked list. As we iterate through the list, we move the sliding window by one position to the right in each iteration. This approach has a time complexity of O(n), where n is the number of nodes in the linked list.

**Approach 2 Code**:

```cpp
ListNode* rotateRight(ListNode* head, int k) {
  if (!head || !head->next || k == 0) return head;

  ListNode* slow = head;
  ListNode* fast = head;

  for (int i = 0; i < k; i++) {
    fast = fast->next;
    if (!fast) fast = head;
  }

  while (fast->next) {
    slow = slow->next;
    fast = fast->next;
  }

  fast->next = head;
  head = slow->next;
  slow->next = NULL;
  return head;
}
```

**Time and Space Complexity Analysis for Approach 2**:

Time Complexity: O(n)
Space Complexity: O(1)

**Approach 3: Mathematical Technique**

This approach uses the fact that rotating a linked list k times is equivalent to rotating it n - k times, where n is the number of nodes in the linked list. We can use this fact to reduce the number of rotations to at most n - 1.

**Approach 3 Code**:

```cpp
ListNode* rotateRight(ListNode* head, int k) {
  if (!head || !head->next || k == 0) return head;

  int len = 0;
  ListNode* curr = head;
  while (curr) {
    curr = curr->next;
    len++;
  }

  k %= len;
  if (k == 0) return head;

  k = len - k;
  ListNode* slow = head;
  ListNode* fast = head;

  while (k--) {
    fast = fast->next;
  }

  while (fast->next) {
    slow = slow->next;
    fast = fast->next;
  }

  fast->next = head;
  head = slow->next;
  slow->next = NULL;
  return head;
}
```

**Time and Space Complexity Analysis for Approach 3**:

Time Complexity: O(n)
Space Complexity: O(1)