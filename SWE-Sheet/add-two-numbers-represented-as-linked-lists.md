**Question**: add-two-numbers-represented-as-linked-lists/: Problem Statement: Given the heads of two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

**Approach 1: Brute Force** 
Create a new linked list to store the sum of the two numbers. Iterate through the two given linked lists, adding the digits at each position and storing the result in the new linked list. If the sum is greater than 9, carry the 1 to the next position. Return the new linked list.

**Approach 1 Code**:
```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode* head = new ListNode(0);
    ListNode* curr = head;
    int carry = 0;

    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) {
            sum += l1->val;
            l1 = l1->next;
        }
        if (l2) {
            sum += l2->val;
            l2 = l2->next;
        }
        carry = sum / 10;
        curr->next = new ListNode(sum % 10);
        curr = curr->next;
    }

    return head->next;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(max(m, n)), where m and n are the lengths of the two linked lists.
* **Space Complexity**: O(max(m, n)), since the new linked list can have a maximum length of max(m, n).

**Approach 2: Optimized using Recursion** 

Traverse the two linked lists recursively, adding the digits at each position. If the sum is greater than 9, carry the 1 to the next position. Return the head of the new linked list.

**Approach 2 Code**:
```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2, int carry) {
    if (!l1 && !l2 && carry == 0) {
        return nullptr;
    }
    int sum = carry;
    if (l1) {
        sum += l1->val;
        l1 = l1->next;
    }
    if (l2) {
        sum += l2->val;
        l2 = l2->next;
    }
    ListNode* node = new ListNode(sum % 10);
    node->next = addTwoNumbers(l1, l2, sum / 10);
    return node;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(max(m, n)), where m and n are the lengths of the two linked lists.
* **Space Complexity**: O(max(m, n)), since the recursion stack can have a maximum depth of max(m, n).

**Approach 3: Optimized using Two Pointers** 

Create two pointers, one for each linked list. Traverse the linked lists, adding the digits at each position and storing the result in a new linked list. If the sum is greater than 9, carry the 1 to the next position. Return the new linked list.

**Approach 3 Code**:
```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode* head = new ListNode(0);
    ListNode* curr = head;
    int carry = 0;

    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) {
            sum += l1->val;
            l1 = l1->next;
        }
        if (l2) {
            sum += l2->val;
            l2 = l2->next;
        }
        carry = sum / 10;
        curr->next = new ListNode(sum % 10);
        curr = curr->next;
    }

    return head->next;
}
```

**Time and Space Complexity Analysis for Approach 3**:

* **Time Complexity**: O(max(m, n)), where m and n are the lengths of the two linked lists.
* **Space Complexity**: O(max(m, n)), since the new linked list can have a maximum length of max(m, n).**Question:** Given the heads of two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

**Approach 1: Recursion**

**Explanation:**
This approach uses recursion to add the digits of the two linked lists, starting from the least significant digit (head of the list). The function adds the digits of the current nodes and the carry from the previous recursion call. If the sum is greater than 9, it creates a new node with the digit value as the remainder of the sum when divided by 10 and carries over the quotient to the next recursion call.

**Approach 1 Code:**

```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2, int carry = 0) {
  if (l1 == nullptr && l2 == nullptr && carry == 0) {
    return nullptr;
  }

  int sum = carry;
  if (l1 != nullptr) sum += l1->val;
  if (l2 != nullptr) sum += l2->val;

  ListNode* node = new ListNode(sum % 10);
  node->next = addTwoNumbers(l1 ? l1->next : nullptr, l2 ? l2->next : nullptr, sum / 10);

  return node;
}
```

**Time and Space Complexity Analysis for Approach 1:**

* Time complexity: O(max(m, n)), where m and n are the lengths of the two linked lists.
* Space complexity: O(max(m, n)), for the recursion stack.

**Approach 2: Iteration**

**Explanation:**
This approach uses iteration to add the digits of the two linked lists, starting from the least significant digit. It creates a dummy head node to which the sum of digits and carry are appended as new nodes. The carry is updated after each iteration.

**Approach 2 Code:**

```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
  ListNode* dummy = new ListNode(0);
  ListNode* curr = dummy;
  int carry = 0;

  while (l1 != nullptr || l2 != nullptr || carry) {
    int sum = carry;
    if (l1 != nullptr) {
      sum += l1->val;
      l1 = l1->next;
    }

    if (l2 != nullptr) {
      sum += l2->val;
      l2 = l2->next;
    }

    carry = sum / 10;
    curr->next = new ListNode(sum % 10);
    curr = curr->next;
  }

  return dummy->next;
}
```

**Time and Space Complexity Analysis for Approach 2:**

* Time complexity: O(max(m, n)), where m and n are the lengths of the two linked lists.
* Space complexity: O(max(m, n)), for the new linked list.