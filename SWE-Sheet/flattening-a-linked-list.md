**Question**: "flattening-a-linked-list/: Problem Statement: Given a linked list containing ‘N’ head nodes where every node in the linked list contains two pointers:"

**Approach 1**: Brute Force

**Explanation**:
- Traverse the linked list and store all the nodes in a data structure (e.g., an array or vector).
- Sort the nodes based on their values.
- Reconstruct the linked list in sorted order.

**Approach 1 Code**:
```cpp
// C++ code to flatten a linked list

// A linked list node
struct Node {
    int data;
    Node* next;
    Node* child;
};

// Function to flatten a linked list
Node* flatten(Node* head) {
    // Store all nodes in a vector
    vector<Node*> nodes;
    Node* curr = head;
    while (curr != NULL) {
        nodes.push_back(curr);
        curr = curr->next;
    }

    // Sort the nodes
    sort(nodes.begin(), nodes.end(), [](Node* a, Node* b) { return a->data < b->data; });

    // Reconstruct the linked list
    Node* newHead = NULL;
    Node* prev = NULL;
    for (auto node : nodes) {
        if (newHead == NULL) {
            newHead = node;
        } else {
            prev->next = node;
        }
        prev = node;
        node->next = NULL;
    }

    return newHead;
}
```

**Time and Space Complexity Analysis for Approach 1**:
- **Time Complexity**: O(N log N), where N is the number of nodes in the linked list. Sorting the nodes requires O(N log N) time.
- **Space Complexity**: O(N), as we store all the nodes in a vector.

**Approach 2**: Optimized Approaches using Maps, Multisets, Binary Search, Two Pointers

**Explanation**:
- Use a multiset to store the nodes and maintain them in sorted order.
- Traverse the linked list and insert each node into the multiset.
- Reconstruct the linked list by iterating over the multiset and linking the nodes together.

**Approach 2 Code**:
```cpp
#include <iostream>
#include <set>

using namespace std;

// A linked list node
struct Node {
    int data;
    Node* next;
    Node* child;
};

// Function to flatten a linked list
Node* flatten(Node* head) {
    // Store all nodes in a multiset
    multiset<Node*> nodes;
    Node* curr = head;
    while (curr != NULL) {
        nodes.insert(curr);
        curr = curr->next;
    }

    // Reconstruct the linked list
    Node* newHead = NULL;
    Node* prev = NULL;
    for (auto node : nodes) {
        if (newHead == NULL) {
            newHead = node;
        } else {
            prev->next = node;
        }
        prev = node;
        node->next = NULL;
    }

    return newHead;
}

int main() {
    // Create a linked list
    Node* head = new Node{1, new Node{2, new Node{3, new Node{4, new Node{5, NULL}}}, NULL}, NULL};

    // Flatten the linked list
    Node* newHead = flatten(head);

    // Print the flattened linked list
    Node* curr = newHead;
    while (curr != NULL) {
        cout << curr->data << " ";
        curr = curr->next;
    }

    return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:
- **Time Complexity**: O(N log N), where N is the number of nodes in the linked list. Inserting nodes into the multiset and iterating over it takes O(N log N) time.
- **Space Complexity**: O(N), as we store all the nodes in the multiset.

**Approach 3**: Greedy Algorithms

**Explanation**:
- Assign a temporary pointer to the head of the linked list.
- While the temporary pointer is not NULL:
    - If the temporary pointer has a child, assign the child to the next of the current node and move the temporary pointer to the child.
    - Otherwise, move the temporary pointer to the next node.

**Approach 3 Code**:
```cpp
Node* flatten(Node* head) {
    Node* temp = head;
    while (temp) {
        if (temp->child) {
            Node* next = temp->next;
            temp->next = temp->child;
            temp->child = NULL;
            while (temp->next) {
                temp = temp->next;
            }
            temp->next = next;
        }
        temp = temp->next;
    }
    return head;
}
```

**Time and Space Complexity Analysis for Approach 3**:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list.
- **Space Complexity**: O(1), as it uses constant extra space.

**Approach 4**: Recursive

**Explanation**:
- If the head is null, return null.
- If the head has no child, return the head.
- Flatten the child and append it to the end of the list.

**Approach 4 Code**:
```cpp
Node* flatten(Node* head) {
  if (!head) {
    return nullptr;
  }
  if (!head->child) {
    return head;
  }
  Node* child = flatten(head->child);
  head->child = nullptr;
  Node* tail = head;
  while (tail->next) {
    tail = tail->next;
  }
  tail->next = child;
  return head;
}
```

**Time and Space Complexity Analysis for Approach 4**:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list.
- **Space Complexity**: O(N), as we store the flattened list in the stack.

**Approach 5**: Backtracking

**Explanation**:
- Use a stack to store the nodes that have not been visited yet.
- Start with the head node and push it into the stack.
- While the stack is not empty:
    - Pop the top node from the stack and visit it.
    - If the node has a child, push the child into the stack.
    - If the node has a next, push the next into the stack.

**Approach 5 Code**:
```cpp
void flatten(Node* head) {
  stack<Node*> s;
  s.push(head);
  while (!s.empty()) {
    Node* curr = s.top();
    s.pop();
    if (curr->child) {
      s.push(curr->child);
    }
    if (curr->next) {
      s.push(curr->next);
    }
    curr->next = curr->child;
    curr->child = nullptr;
  }
}
```

**Time and Space Complexity Analysis for Approach 5**:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list.
- **Space Complexity**: O(N), as we store the nodes in the stack.**Question**: **flattening-a-linked-list/: Problem Statement: Given a linked list containing ‘N’ head nodes where every node in the linked list contains two pointers:**

**Approach 1: Recursive Approach**

**Explanation**: This approach involves recursively traversing the linked list and flattening it in place.

**Approach 1 Code**:

```cpp
class Node {
public:
    int val;
    Node *next;
    Node *child;

    Node(int val): val(val), next(nullptr), child(nullptr) {}
};

Node* flatten(Node *head) {
    if (head == nullptr) return head;

    head->child = flatten(head->child);
    Node *tail = head;

    while (tail->next != nullptr) {
        tail = tail->next;
    }

    tail->next = flatten(head->next);
    head->next = head->child;
    head->child = nullptr;

    return head;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(N), where N is the total number of nodes in the linked list.
* **Space Complexity**: O(N), as we need to store the flattened list in a stack frame during the recursion.

**Approach 2: Iterative Approach**

**Explanation**: This approach uses a stack to iteratively flatten the linked list.

**Approach 2 Code**:

```cpp
Node* flatten(Node *head) {
    if (head == nullptr) return head;

    stack<Node*> st;
    st.push(head);

    Node *prev = nullptr;

    while (!st.empty()) {
        Node *curr = st.top();
        st.pop();

        if (prev != nullptr) {
            prev->next = curr;
            prev->child = nullptr;
        }

        if (curr->next != nullptr) {
            st.push(curr->next);
        }

        if (curr->child != nullptr) {
            st.push(curr->child);
        }

        prev = curr;
    }

    return head;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(N), where N is the total number of nodes in the linked list.
* **Space Complexity**: O(N), as we need to store the stack frames for all the nodes in the linked list.