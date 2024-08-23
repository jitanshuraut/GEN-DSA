**Question**: Find Intersection of Two Linked Lists

Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect. If the two linked lists have no intersection at all, return null.

**Approach 1: Brute Force**

**Explanation:**
Iterate over the first linked list and for each node, iterate over the second linked list to check if they are equal. If they are equal, return that node.

**Approach 1 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  while (headA != NULL) {
    ListNode *temp = headB;
    while (temp != NULL) {
      if (headA == temp) {
        return headA;
      }
      temp = temp->next;
    }
    headA = headA->next;
  }
  return NULL;
}
```

**Time Complexity:** O(m * n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(1).

**Approach 2: Using Maps**

**Explanation:**
Insert all nodes of one linked list into a hash map. Then, iterate over the other linked list and check if each node exists in the hash map. If it does, return that node.

**Approach 2 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  unordered_map<ListNode*, bool> seen;
  while (headA != NULL) {
    seen[headA] = true;
    headA = headA->next;
  }
  while (headB != NULL) {
    if (seen[headB]) {
      return headB;
    }
    headB = headB->next;
  }
  return NULL;
}
```

**Time Complexity:** O(m + n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(m), as we may need to store all nodes of one linked list in the hash map.

**Approach 3: Using Multisets**

**Explanation:**
Insert all nodes of one linked list into a multiset. Then, iterate over the other linked list and check if each node exists in the multiset. If it does, return that node.

**Approach 3 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  multiset<ListNode*> seen;
  while (headA != NULL) {
    seen.insert(headA);
    headA = headA->next;
  }
  while (headB != NULL) {
    if (seen.find(headB) != seen.end()) {
      return headB;
    }
    headB = headB->next;
  }
  return NULL;
}
```

**Time Complexity:** O(m + n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(m), as we may need to store all nodes of one linked list in the multiset.

**Approach 4: Using Binary Search**

**Explanation:**
If one linked list is longer than the other, we can use binary search to find the intersection point. We can calculate the difference in length between the two linked lists and move the pointer of the longer list forward by that difference. Then, we can iterate over both linked lists simultaneously and check if they intersect.

**Approach 4 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  ListNode *tempA = headA, *tempB = headB;
  int lenA = 0, lenB = 0;
  while (tempA != NULL) {
    lenA++;
    tempA = tempA->next;
  }
  while (tempB != NULL) {
    lenB++;
    tempB = tempB->next;
  }
  int diff = abs(lenA - lenB);
  if (lenA > lenB) {
    while (diff--) {
      headA = headA->next;
    }
  } else {
    while (diff--) {
      headB = headB->next;
    }
  }
  while (headA != NULL && headB != NULL) {
    if (headA == headB) {
      return headA;
    }
    headA = headA->next;
    headB = headB->next;
  }
  return NULL;
}
```

**Time Complexity:** O(m + n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(1).

**Approach 5: Using Two Pointers**

**Explanation:**
We can iterate over both linked lists simultaneously using two pointers. At each step, we move the pointer of the shorter linked list forward by one node. If the two linked lists intersect, the two pointers will eventually meet at the intersection point.

**Approach 5 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  ListNode *tempA = headA, *tempB = headB;
  while (tempA != NULL && tempB != NULL) {
    tempA = tempA->next;
    tempB = tempB->next;
  }
  if (tempA == NULL) {
    tempA = headB;
  } else {
    tempB = headA;
  }
  while (tempA != NULL && tempB != NULL) {
    if (tempA == tempB) {
      return tempA;
    }
    tempA = tempA->next;
    tempB = tempB->next;
  }
  return NULL;
}
```

**Time Complexity:** O(m + n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(1).

**Approach 6: Using Recursion**

**Explanation:**
We can use recursion to iterate over both linked lists simultaneously. At each step, we move the pointer of the shorter linked list forward by one node. If the two linked lists intersect, the two recursive calls will eventually meet at the intersection point.

**Approach 6 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  if (headA == NULL || headB == NULL) {
    return NULL;
  }
  if (headA == headB) {
    return headA;
  }
  return getIntersectionNode(headA->next, headB->next);
}
```

**Time Complexity:** O(m + n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(m + n).

**Approach 7: Using Backtracking**

**Explanation:**
We can use backtracking to explore all possible paths in both linked lists. At each step, we can either move the pointer of the first linked list forward, move the pointer of the second linked list forward, or check if the two pointers have intersected. If the two linked lists intersect, we will eventually backtrack to the intersection point.

**Approach 7 Code:**
```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
  if (headA == NULL || headB == NULL) {
    return NULL;
  }
  if (headA == headB) {
    return headA;
  }
  ListNode *nextA = headA->next;
  ListNode *nextB = headB->next;
  ListNode *intersection = NULL;
  if (visited.find(headA) == visited.end()) {
    visited.insert(headA);
    intersection = getIntersectionNode(nextA, headB);
  }
  if (intersection == NULL) {
    if (visited.find(headB) == visited.end()) {
      visited.insert(headB);
      intersection = getIntersectionNode(headA, nextB);
    }
  }
  return intersection;
}
```

**Time Complexity**: O(m * n), where m and n are the lengths of the two linked lists.
**Space Complexity:** O(m + n), as we may need to store all nodes of one linked list in the visited set.**Question**: Find the intersection of two linked lists.

**Approach 1: Brute Force**

**Explanation**: Iterate through each node in the first linked list and compare it to every node in the second linked list. If a match is found, return the intersecting node.

**Code**:

```cpp
ListNode* findIntersection(ListNode* headA, ListNode* headB) {
  while (headA) {
    ListNode* currB = headB;
    while (currB) {
      if (headA == currB) {
        return headA;
      }
      currB = currB->next;
    }
    headA = headA->next;
  }
  return nullptr;
}
```

**Time and Space Complexity**: O(m*n), where m and n are the lengths of the two linked lists.

**Approach 2: Set**

**Explanation**: Use a set to store the nodes of the first linked list. Then, iterate through the second linked list and check if each node is present in the set. If a match is found, return the intersecting node.

**Code**:

```cpp
ListNode* findIntersection(ListNode* headA, ListNode* headB) {
  unordered_set<ListNode*> visited;
  while (headA) {
    visited.insert(headA);
    headA = headA->next;
  }
  while (headB) {
    if (visited.count(headB)) {
      return headB;
    }
    headB = headB->next;
  }
  return nullptr;
}
```

**Time and Space Complexity**: O(m+n), where m and n are the lengths of the two linked lists.

**Approach 3: Two Pointers**

**Explanation**: Start two pointers, one at the beginning of each linked list. Iterate through both lists at the same time, advancing the pointer of the shorter list when necessary. When the pointers meet, they will be at the intersection node (if one exists).

**Code**:

```cpp
ListNode* findIntersection(ListNode* headA, ListNode* headB) {
  ListNode* ptrA = headA, *ptrB = headB;
  while (ptrA || ptrB) {
    if (ptrA == ptrB) {
      return ptrA;
    }
    ptrA = ptrA ? ptrA->next : headB;
    ptrB = ptrB ? ptrB->next : headA;
  }
  return nullptr;
}
```

**Time and Space Complexity**: O(m+n), where m and n are the lengths of the two linked lists.

**Approach 4: Dummy Head**

**Explanation**: Create two dummy nodes and attach them to the heads of the two linked lists. Then, iterate through both lists at the same time, advancing both pointers by one each time. When one pointer reaches the end of its list, move it to the head of the other list. When the two pointers meet, they will be at the intersection node (if one exists).

**Code**:

```cpp
ListNode* findIntersection(ListNode* headA, ListNode* headB) {
  ListNode* dummyA = new ListNode(0, headA), *dummyB = new ListNode(0, headB);
  ListNode* ptrA = dummyA, *ptrB = dummyB;
  while (ptrA || ptrB) {
    if (ptrA == ptrB) {
      return ptrA->next;
    }
    ptrA = ptrA ? ptrA->next : dummyB;
    ptrB = ptrB ? ptrB->next : dummyA;
  }
  return nullptr;
}
```

**Time and Space Complexity**: O(m+n), where m and n are the lengths of the two linked lists.