**Question**: Delete a Given Node in a Linked List with O(1) Approach

**Problem Statement**: Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list instead, you will be given access to the node to be deleted directly. It is guaranteed that the node to be deleted is not a tail node in the list.

**Approach 1: Brute Force**

**Explanation**: The brute force approach involves traversing the entire linked list from the head until we find the node to be deleted. Once we find the node, we can delete it by modifying the pointers of the previous and next nodes.

**Approach 1 Code**:

```cpp
void deleteNode(ListNode* node) {
  // Check if the node is valid
  if (!node) return;

  // Find the previous and next nodes of the node to be deleted
  ListNode* prev = nullptr;
  ListNode* curr = node;
  ListNode* next = curr->next;

  // Traverse the linked list until we find the node to be deleted
  while (curr != node) {
    prev = curr;
    curr = next;
    next = next->next;
  }

  // If the node is not the head of the list
  if (prev) {
    prev->next = next;
  }

  // Delete the node
  delete curr;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* Time complexity: O(n), where n is the number of nodes in the linked list.
* Space complexity: O(1), as we only use a constant amount of extra space.

**Approach 2: Optimized Approach using Swapping**

**Explanation**: This approach is more efficient than the brute force approach because it doesn't require traversing the entire linked list. Instead, we can simply swap the data of the node to be deleted with the data of the next node and then delete the next node.

**Approach 2 Code**:

```cpp
void deleteNode(ListNode* node) {
  // Check if the node is valid
  if (!node) return;

  // If the node is not the last node in the list
  if (node->next) {
    // Swap the data of the node to be deleted with the data of the next node
    int temp = node->val;
    node->val = node->next->val;
    node->next->val = temp;

    // Delete the next node
    ListNode* next = node->next;
    node->next = next->next;
    delete next;
  }
}
```

**Time and Space Complexity Analysis for Approach 2**:

* Time complexity: O(1), as we only perform a constant number of operations.
* Space complexity: O(1), as we don't use any extra space.## Question: delete-given-node-in-a-linked-list-o1-approach
**Problem Statement**: Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list instead, you will be given access to the node to be deleted directly. It is guaranteed that the node to be deleted is not a tail node in the list.

## Approach 1: Copy data from the next node
**Explanation**: Since we do not have access to the previous node, we cannot delete the current node directly. Instead, we can copy the data from the next node to the current node and then delete the next node. This way, the current node will effectively be deleted from the list.

**C++ Code**:
```cpp
void deleteNode(Node* node) {
    if (node == nullptr || node->next == nullptr) {
        return;
    }
    
    node->data = node->next->data;
    node->next = node->next->next;
}
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(1). The operation is constant time as it only involves copying data from one node to another and modifying the next pointer.
- Space Complexity: O(1). No additional space is required beyond the space occupied by the node itself.

## Approach 2: Swap with last node
**Explanation**: If we cannot delete the current node directly, we can swap its data with the data of the last node in the list and then delete the last node. This way, the current node will be effectively removed from the list without affecting the integrity of the list.

**C++ Code**:
```cpp
void deleteNode(Node* node) {
    if (node == nullptr || node->next == nullptr) {
        return;
    }
    
    Node* last = node;
    while (last->next != nullptr) {
        last = last->next;
    }
    
    node->data = last->data;
    node->next = last->next;
    delete last;
}
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(n). In the worst case, we need to traverse the entire list to find the last node.
- Space Complexity: O(1). No additional space is required beyond the space occupied by the nodes in the list.