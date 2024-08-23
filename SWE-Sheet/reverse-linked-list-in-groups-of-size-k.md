## Question

Given the head of a singly linked list of `n` nodes and an integer `k`, where `k` is less than or equal to `n`. Your task is to reverse the order of each group of `k` consecutive nodes, if `n` is not divisible by `k`, then the last group of remaining nodes should remain unchanged.

## Approach 1: Brute Force

**Explanation:**
The brute force approach involves iterating over the linked list and reversing the order of each group of `k` consecutive nodes. We can use two pointers, `prev` and `curr`, to keep track of the previous and current nodes, respectively. We start by reversing the first `k` nodes by setting `prev` to `curr` and `curr` to `curr->next`. Then, we move `prev` to the node before the current group of `k` nodes and repeat the process until we reach the end of the linked list.

**C++ Code:**

```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    if (k == 1 || head == nullptr) {
        return head;
    }
    
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* prev = dummy;
    ListNode* curr = head;
    
    while (curr) {
        ListNode* first = prev->next;
        ListNode* last = curr;
        for (int i = 0; i < k - 1 && last; i++) {
            last = last->next;
        }
        if (last == nullptr) {
            break;
        }
        ListNode* next = last->next;
        ListNode* newHead = last;
        
        while (first != next) {
            ListNode* tmp = first->next;
            first->next = newHead;
            newHead = first;
            first = tmp;
        }
        
        prev->next = newHead;
        prev = curr;
        curr = next;
    }
    
    return dummy->next;
}
```

**Time and Space Complexity Analysis:**
* Time complexity: O(`n`), where `n` is the number of nodes in the linked list.
* Space complexity: O(1), as we only use a constant number of pointers.

## Approach 2: Optimized Using Multiset

**Explanation:**
We can use a multiset to store the elements of the linked list in sorted order. This will allow us to reverse the order of each group of `k` consecutive nodes in O(1) time. We iterate over the linked list and insert each node into the multiset. Then, we use a sliding window of size `k` to reverse the order of each group of `k` nodes.

**C++ Code:**

```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    if (k == 1 || head == nullptr) {
        return head;
    }
    
    multiset<int> window;
    ListNode* curr = head;
    while (curr) {
        window.insert(curr->val);
        if (window.size() == k) {
            ListNode* prev = nullptr;
            ListNode* newHead = nullptr;
            for (auto it = window.rbegin(); it != window.rend(); it++) {
                ListNode* newNode = new ListNode(*it);
                if (prev == nullptr) {
                    newHead = newNode;
                } else {
                    prev->next = newNode;
                }
                prev = newNode;
            }
            curr->next = newHead;
            window.clear();
        }
        curr = curr->next;
    }
    
    return head;
}
```

**Time and Space Complexity Analysis:**
* Time complexity: O(`n` log `k`), where `n` is the number of nodes in the linked list and `k` is the size of the group.
* Space complexity: O(`k`), as we use a multiset to store the elements of the current window.

## Approach 3: Optimized Using Two Pointers

**Explanation:**
This approach uses two pointers, `prev` and `curr`, to reverse the order of each group of `k` consecutive nodes. We start by setting `prev` to `nullptr` and `curr` to the head of the linked list. Then, we iterate over the linked list and reverse the order of each group of `k` consecutive nodes by moving `prev` to the node before the current group of `k` nodes and setting `prev->next` to `curr`. We repeat this process until `curr` reaches the end of the linked list.

**C++ Code:**

```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    if (k == 1 || head == nullptr) {
        return head;
    }
    
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* prev = dummy;
    ListNode* curr = head;
    
    while (curr) {
        ListNode* first = prev->next;
        ListNode* last = curr;
        for (int i = 0; i < k - 1 && last; i++) {
            last = last->next;
        }
        if (last == nullptr) {
            break;
        }
        ListNode* next = last->next;
        prev->next = last;
        curr->next = next;
        ListNode* tmp = first;
        while (tmp != last) {
            ListNode* newTmp = tmp->next;
            tmp->next = curr;
            curr = tmp;
            tmp = newTmp;
        }
        prev = curr;
        curr = next;
    }
    
    return dummy->next;
}
```

**Time and Space Complexity Analysis:**
* Time complexity: O(`n`), where `n` is the number of nodes in the linked list.
* Space complexity: O(1), as we only use a constant number of pointers.**Question**: Reverse Linked List in Groups of Size K: Problem Statement: Given the head of a singly linked list of `n` nodes and an integer `k`, where `k` is less than or equal to `n`. Your task is to reverse the order of each group of `k` consecutive nodes, if `n` is not divisible by `k`, then the last group of remaining nodes should remain unchanged.

## **Approach 1: Iterative Approach**

**Explanation:**

This approach iterates through the linked list and reverses the order of nodes in groups of size `k`.
1. Initialize three pointers: `prev`, `curr`, and `next`.
2. Iterate while `curr` is not null.
3. Reverse the order of the next `k` nodes by updating the `prev`, `curr`, and `next` pointers.
4. Move `prev` and `curr` `k` steps ahead.

**Approach 1 Code:**

```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    if (!head || k == 1) return head;

    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* prev = dummy;
    ListNode* curr = head;

    while (curr) {
        ListNode* next = nullptr;
        for (int i = 0; i < k && curr; i++) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        
        ListNode* nextFromPrev = prev->next;
        curr = nextFromPrev; 
        prev = nextFromPrev->next; 
    }
    return dummy->next;
}
```

**Time and Space Complexity Analysis for Approach 1:**
- Time Complexity: O(n), where `n` is the number of nodes in the linked list.
- Space Complexity: O(1), as no additional space is required.

## **Approach 2: Recursive Approach**

**Explanation:**

This approach uses a recursive function to reverse the order of nodes in groups of size `k`.
1. If `k` is 1 or the linked list is null, return the head.
2. Reverse the next `k` nodes recursively.
3. Connect the reversed portion to the remaining nodes.

**Approach 2 Code:**

```cpp
ListNode* reverseKGroup(ListNode* head, int k) {
    if (!head || k == 1) return head;
    
    ListNode* curr = head;
    for (int i = 0; i < k; i++) {
        if (!curr) return head;
        curr = curr->next;
    }
    
    ListNode* newHead = reverseKGroup(curr, k);
    
    while (k--) {
        ListNode* next = head->next;
        head->next = newHead;
        newHead = head;
        head = next;
    }
    return newHead;
}
```

**Time and Space Complexity Analysis for Approach 2:**
- Time Complexity: O(n), where `n` is the number of nodes in the linked list.
- Space Complexity: O(n), as the recursion stack can grow up to `n` levels.