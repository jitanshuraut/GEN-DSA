**Question**: remove-n-th-node-from-the-end-of-a-linked-list/: Problem Statement: Given a linked list and an integer N, the task is to delete the Nth node from the end of the linked list and print the updated linked list.

**Approach 1: Brute Force**

**Explanation**: This approach traverses the entire linked list twice. In the first traversal, it counts the number of nodes in the linked list. In the second traversal, it moves N nodes from the beginning of the linked list and deletes the next node.

**Approach 1 Code**:
```cpp
struct Node {
  int data;
  Node* next;
};

Node* deleteNthNodeFromEnd(Node* head, int n) {
  // Count the number of nodes in the linked list
  int count = 0;
  Node* temp = head;
  while (temp != nullptr) {
    count++;
    temp = temp->next;
  }

  // Move N nodes from the beginning of the linked list
  temp = head;
  for (int i = 0; i < n; i++) {
    temp = temp->next;
  }

  // Delete the next node
  Node* prev = nullptr;
  while (temp->next != nullptr) {
    prev = temp;
    temp = temp->next;
  }

  if (prev != nullptr) {
    prev->next = temp->next;
  } else {
    head = head->next;
  }

  delete temp;
  return head;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* Time Complexity: O(N), where N is the number of nodes in the linked list.
* Space Complexity: O(1), as no additional space is required.

**Approach 2: Optimized Approach using Two Pointers**

**Explanation**: This approach uses two pointers, slow and fast. The fast pointer moves N nodes ahead of the slow pointer. Then, both pointers move together until the fast pointer reaches the end of the linked list. At this point, the slow pointer will be pointing to the Nth node from the end of the linked list, which can be deleted.

**Approach 2 Code**:
```cpp
struct Node {
  int data;
  Node* next;
};

Node* deleteNthNodeFromEnd(Node* head, int n) {
  Node* slow = head;
  Node* fast = head;

  // Move the fast pointer N nodes ahead of the slow pointer
  for (int i = 0; i < n; i++) {
    fast = fast->next;
  }

  // Move both pointers together until the fast pointer reaches the end of the linked list
  while (fast != nullptr) {
    slow = slow->next;
    fast = fast->next;
  }

  // Delete the slow pointer
  Node* prev = nullptr;
  while (slow->next != nullptr) {
    prev = slow;
    slow = slow->next;
  }

  if (prev != nullptr) {
    prev->next = slow->next;
  } else {
    head = head->next;
  }

  delete slow;
  return head;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* Time Complexity: O(N), where N is the number of nodes in the linked list.
* Space Complexity: O(1), as no additional space is required.**Question**: remove-n-th-node-from-the-end-of-a-linked-list/: Problem Statement: Given a linked list and an integer N, the task is to delete the Nth node from the end of the linked list and print the updated linked list.

**Approach 1: Brute Force (Single Pass)**

**Explanation**: This approach involves traversing the linked list once to calculate its length (N), then traversing the linked list again to locate and delete the (N - n)th node from the beginning.

**Approach 1 Code**:

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
    Node(int x) : data(x), next(NULL) {}
};

Node *removeNthFromEnd(Node *head, int n) {
    int length = 0;
    Node *temp = head;
    while (temp) {
        length++;
        temp = temp->next;
    }

    int pos = length - n;
    Node *prev = NULL, *curr = head;
    while (pos--) {
        prev = curr;
        curr = curr->next;
    }

    if (prev)
        prev->next = curr->next;
    else
        head = head->next;
    delete curr;

    return head;
}

int main() {
    Node *head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    int n = 2;
    head = removeNthFromEnd(head, n);

    Node *temp = head;
    while (temp) {
        cout << temp->data << " ";
        temp = temp->next;
    }

    return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(2N), where N is the number of nodes in the linked list.
* **Space Complexity**: O(1)

**Approach 2: Two Pointers (Single Pass)**

**Explanation**: This approach uses two pointers, 'slow' and 'fast', to traverse the linked list. 'fast' is moved n nodes ahead of 'slow'. When 'fast' reaches the end, 'slow' will be at the (N - n)th node from the beginning.

**Approach 2 Code**:

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
    Node(int x) : data(x), next(NULL) {}
};

Node *removeNthFromEnd(Node *head, int n) {
    Node *slow = head, *fast = head;
    while (n--)
        fast = fast->next;

    if (!fast)
        return head->next;

    while (fast->next) {
        slow = slow->next;
        fast = fast->next;
    }

    slow->next = slow->next->next;
    return head;
}

int main() {
    Node *head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(4);
    head->next->next->next->next = new Node(5);

    int n = 2;
    head = removeNthFromEnd(head, n);

    Node *temp = head;
    while (temp) {
        cout << temp->data << " ";
        temp = temp->next;
    }

    return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(N), where N is the number of nodes in the linked list.
* **Space Complexity**: O(1)