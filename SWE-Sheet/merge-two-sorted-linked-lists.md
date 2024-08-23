## Question:
**Merge Two Sorted Linked Lists:** Given two sorted linked lists, merge them to produce a combined sorted linked list. Return the head of the final linked list created.

## Approach 1: Brute Force (Insertion Sort)
**Explanation:**
This approach iterates through one linked list and inserts each node into the other linked list at the appropriate sorted position. The complexity of this approach is O(n^2) in both time and space, where n is the total number of nodes in the two linked lists.

**Code:**
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
  ListNode* dummy = new ListNode(0);
  ListNode* curr = dummy;
  while (l1 || l2) {
    if (!l1) {
      curr->next = l2;
      break;
    }
    if (!l2) {
      curr->next = l1;
      break;
    }
    if (l1->val <= l2->val) {
      curr->next = l1;
      l1 = l1->next;
    } else {
      curr->next = l2;
      l2 = l2->next;
    }
    curr = curr->next;
  }
  return dummy->next;
}
```

## Approach 2: Optimized using Two Pointers
**Explanation:**
This approach uses two pointers, one for each linked list, and advances the pointers to merge the nodes into a new linked list. The time complexity of this approach is O(n), where n is the total number of nodes in the two linked lists, and the space complexity is O(1).

**Code:**
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
  ListNode* dummy = new ListNode(0);
  ListNode* curr = dummy;
  while (l1 && l2) {
    if (l1->val <= l2->val) {
      curr->next = l1;
      l1 = l1->next;
    } else {
      curr->next = l2;
      l2 = l2->next;
    }
    curr = curr->next;
  }
  if (l1) curr->next = l1;
  if (l2) curr->next = l2;
  return dummy->next;
}
```

## Approach 3: Recursive
**Explanation:**
This approach recursively merges the two linked lists by comparing the values of their heads. The time complexity of this approach is O(n), where n is the total number of nodes in the two linked lists, and the space complexity is O(n) for the call stack.

**Code:**
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
  if (!l1) return l2;
  if (!l2) return l1;
  if (l1->val <= l2->val) {
    l1->next = mergeTwoLists(l1->next, l2);
    return l1;
  } else {
    l2->next = mergeTwoLists(l2->next, l1);
    return l2;
  }
}
```**Question**: merge-two-sorted-linked-lists/: Problem Statement: Given two sorted linked lists, merge them to produce a combined sorted linked list. Return the head of the final linked list created.

**Approach 1: Brute Force Iterative Approach**

**Explanation**:
- Create a dummy node and a current pointer, which will be used to return the head of the merged linked list.
- Iterate through both linked lists and compare the values of the current nodes.
- Append the smaller node to the current pointer of the merged linked list and advance the current pointer.
- Advance the pointer of the linked list with the smaller node.
- If one of the linked lists is empty, append the remaining nodes of the other linked list to the merged linked list.
- Return the head of the merged linked list.

**Approach 1 Code**:
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode* dummy = new ListNode(0);
    ListNode* current = dummy;
    
    while (l1 != nullptr && l2 != nullptr) {
        if (l1->val < l2->val) {
            current->next = l1;
            l1 = l1->next;
        } else {
            current->next = l2;
            l2 = l2->next;
        }
        current = current->next;
    }
    
    if (l1 != nullptr) {
        current->next = l1;
    }
    if (l2 != nullptr) {
        current->next = l2;
    }
    
    return dummy->next;
}
```

**Time and Space Complexity Analysis for Approach 1**:
- **Time Complexity**: O(n+m), where n and m are the lengths of the two input linked lists.
- **Space Complexity**: O(1), as no additional space is required to store the merged linked list.

**Approach 2: Recursion**

**Explanation**:
- If one of the linked lists is empty, return the other linked list.
- If the value of the first node of the first linked list is less than the value of the first node of the second linked list, set the next pointer of the first node of the first linked list to the result of merging the rest of the first linked list and the second linked list.
- Otherwise, set the next pointer of the first node of the second linked list to the result of merging the rest of the second linked list and the first linked list.
- Return the first node of the merged linked list.

**Approach 2 Code**:
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (l1 == nullptr) {
        return l2;
    }
    if (l2 == nullptr) {
        return l1;
    }
    if (l1->val < l2->val) {
        l1->next = mergeTwoLists(l1->next, l2);
        return l1;
    } else {
        l2->next = mergeTwoLists(l2->next, l1);
        return l2;
    }
}
```

**Time and Space Complexity Analysis for Approach 2**:
- **Time Complexity**: O(n+m), where n and m are the lengths of the two input linked lists.
- **Space Complexity**: O(n+m), as the recursion stack can grow up to n+m levels.