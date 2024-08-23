## Question:
Clone a linked list with random and next pointer. Given a linked list where every node in the linked list contains two pointers:
- random pointer which points to a random node of the linked list
- next pointer which points to the next node of the linked list

## Approach 1: Brute Force (Copy Random Pointers)
This approach involves copying the random pointers for each node in the cloned linked list.

### Approach 1 Code:
```cpp
class Node {
public:
    int val;
    Node* next;
    Node* random;
    Node(int val) : val(val), next(nullptr), random(nullptr) {}
};

Node* copyRandomList(Node* head) {
    if (!head) return nullptr;
    unordered_map<Node*, Node*> nodeMap;
    Node* curr = head, *cloneHead = new Node(curr->val);
    nodeMap[curr] = cloneHead;
    while (curr) {
        cloneHead->next = curr->next ? new Node(curr->next->val) : nullptr;
        cloneHead->random = curr->random ? nodeMap[curr->random] : nullptr;
        curr = curr->next;
        cloneHead = cloneHead->next;
    }
    return cloneHead;
}
```

### Time and Space Complexity Analysis for Approach 1:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list, as we traverse the list once to copy the random pointers.
- **Space Complexity**: O(N), as we use a hash map to store the original-cloned node mappings.

## Approach 2: Optimized (Multiset)
This approach leverages a multiset to efficiently clone the random pointers.

### Approach 2 Code:
```cpp
class Node {
public:
    int val;
    Node* next;
    Node* random;
    Node(int val) : val(val), next(nullptr), random(nullptr) {}
};

Node* copyRandomList(Node* head) {
    multiset<pair<Node*, Node*>> randomMap;
    unordered_map<Node*, Node*> nodeMap;
    Node* curr = head, *cloneHead = new Node(curr->val);
    nodeMap[curr] = cloneHead;
    while (curr) {
        cloneHead->next = curr->next ? new Node(curr->next->val) : nullptr;
        if (curr->random) randomMap.insert({curr->random, cloneHead});
        curr = curr->next;
        cloneHead = cloneHead->next;
    }
    for (auto& [original, clone] : randomMap) clone->random = nodeMap[original];
    return cloneHead;
}
```

### Time and Space Complexity Analysis for Approach 2:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list, as we traverse the list once to create the mappings.
- **Space Complexity**: O(N), as we use a multiset and a hash map for mappings.

## Approach 3: Optimized (Two Pointers)
This approach uses two pointers to efficiently clone the random pointers.

### Approach 3 Code:
```cpp
class Node {
public:
    int val;
    Node* next;
    Node* random;
    Node(int val) : val(val), next(nullptr), random(nullptr) {}
};

Node* copyRandomList(Node* head) {
    if (!head) return nullptr;
    Node* curr = head, *currClone;
    while (curr) {
        currClone = new Node(curr->val);
        currClone->next = curr->next;
        curr->next = currClone;
        curr = curr->next->next;
    }
    curr = head;
    while (curr) {
        curr->next->random = curr->random ? curr->random->next : nullptr;
        curr = curr->next->next;
    }
    Node* cloneHead = head->next;
    curr = head;
    while (curr) {
        curr->next = curr->next ? curr->next->next : nullptr;
        cloneHead->next = cloneHead->next ? cloneHead->next->next : nullptr;
        curr = curr->next;
        cloneHead = cloneHead->next;
    }
    return cloneHead;
}
```

### Time and Space Complexity Analysis for Approach 3:
- **Time Complexity**: O(N), where N is the number of nodes in the linked list, as we traverse the list three times to clone the random pointers.
- **Space Complexity**: O(1), as we modify the original linked list in place, effectively using constant additional space.**Question**: Clone Linked List with Random and Next Pointer

**Problem Statement**: Given a linked list where every node in the linked list contains two pointers:

* **Next**: Points to the next node in the linked list.
* **Random**: Points to a random node in the linked list or null if there is no random node.

Clone the linked list such that the cloned list has the same structure as the original linked list, but with deep copies of the nodes.

**Approach 1: Brute Force (Hashmap)**

**Explanation**:
We can clone the linked list using a hashmap:
1. Traverse the original linked list and store the node and its corresponding clone in a hashmap.
2. Traverse the original linked list again and update the next and random pointers of the clones using the hashmap.

**Approach 1 Code**:

```cpp
unordered_map<Node*, Node*> hash;

Node* clone(Node* head) {
  if (head == nullptr) return nullptr;
  Node* cloneHead = new Node(head->val);
  hash[head] = cloneHead;
  Node* curr = head, *cloneCurr = cloneHead;
  while (curr != nullptr) {
    cloneCurr->next = hash[curr->next];
    cloneCurr->random = hash[curr->random];
    curr = curr->next, cloneCurr = cloneCurr->next;
  }
  return cloneHead;
}
```

**Time and Space Complexity Analysis for Approach 1**:

- **Time Complexity**: O(N), where N is the number of nodes in the linked list.
- **Space Complexity**: O(N), for the hashmap.

**Approach 2: Divide and Conquer (Recursive)**

**Explanation**:
We can clone the linked list using a recursive approach:
1. Clone the next pointer of the current node by recursively cloning the next node.
2. Clone the random pointer of the current node by randomly choosing a node from the cloned linked list.
3. Return the cloned linked list.

**Approach 2 Code**:

```cpp
Node* clone(Node* head) {
  if (head == nullptr) return nullptr;
  Node* cloneHead = new Node(head->val);
  cloneHead->next = clone(head->next);
  cloneHead->random = head->random ? clone(head->random) : nullptr;
  return cloneHead;
}
```

**Time and Space Complexity Analysis for Approach 2**:

- **Time Complexity**: O(N), where N is the number of nodes in the linked list.
- **Space Complexity**: O(1), no additional data structure is used.