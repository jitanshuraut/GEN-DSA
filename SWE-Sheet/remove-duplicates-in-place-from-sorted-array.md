**Question:** remove-duplicates-in-place-from-sorted-array/: Problem Statement: Given an integer array sorted in non-decreasing order, remove the duplicates in place such that each unique element appears only once. The relative order of the elements should be kept the same.

**Approach 1: Brute Force**
 
**Explanation:**

Use a nested loop to compare each element with every other element in the array. If duplicates are found, overwrite one of them with a special value (e.g., -1).

**Approach 1 Code:**
```cpp
void removeDuplicates(int* nums, int size) {
    for (int i = 0; i < size; i++) {
        for (int j = i + 1; j < size; j++) {
            if (nums[i] == nums[j]) {
                nums[j] = -1; 
            }
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 1:**
* **Time Complexity**: O(n^2), where n is the size of the array.
* **Space Complexity**: O(1), as no additional space is required.

**Approach 2: Optimized Approach using Two Pointers**

**Explanation:**

Use two pointers, `slow` and `fast`, to traverse the array. If the value pointed to by `fast` is unique, copy it to the value pointed by `slow` and increment `slow`. Otherwise, increment `fast`.

**Approach 2 Code:**
```cpp
void removeDuplicates(int* nums, int size) {
    int slow = 0, fast = 0;

    while (fast < size) {
        if (nums[slow] != nums[fast]) {
            nums[slow+1] = nums[fast];
            slow++;
        }
        fast++;
    }
}
```

**Time and Space Complexity Analysis for Approach 2:**
* **Time Complexity**: O(n), where n is the size of the array.
* **Space Complexity**: O(1), as no additional space is required.## Question:
remove-duplicates-in-place-from-sorted-array/: Problem Statement: Given an integer array sorted in non-decreasing order, remove the duplicates in place such that each unique element appears only once. The relative order of the elements should be kept the same.

## Approach 1: Using Two Pointers (Sliding Window Technique)
**Explanation:**
This approach uses two pointers, `slow` and `fast`, to iterate through the array. The `slow` pointer keeps track of the unique elements, and the `fast` pointer scans the array to find duplicates. When a duplicate is found, the elements between the `slow` and `fast` pointers are shifted left to overwrite the duplicate element.

**Approach 1 Code:**
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0;
        
        int slow = 0;
        int fast = 1;
        
        while (fast < nums.size()) {
            if (nums[slow] == nums[fast]) {
                fast++;
            } else {
                slow++;
                nums[slow] = nums[fast];
                fast++;
            }
        }
        
        return slow + 1;
    }
};
```
**Time Complexity:** O(n), where n is the length of the input array.
**Space Complexity:** O(1), as we are modifying the input array in place.

## Approach 2: Using a Hash Set (Mathematical Techniques)
**Explanation:**
This approach uses a hash set to keep track of unique elements. We iterate through the array, adding each element to the hash set. If an element is already in the hash set, we skip it. The unique elements are then copied back to the input array.

**Approach 2 Code:**
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        unordered_set<int> uniqueElements;
        
        int idx = 0;
        
        for (int num : nums) {
            if (uniqueElements.find(num) == uniqueElements.end()) {
                uniqueElements.insert(num);
                nums[idx++] = num;
            }
        }
        
        return idx;
    }
};
```
**Time Complexity:** O(n), where n is the length of the input array.
**Space Complexity:** O(n), as we are using a hash set to store the unique elements.

## Approach 3: Using a Trie Data Structure (Trie Data Structure)
**Explanation:**
This approach uses a trie data structure to represent the unique elements in the array. We insert each element into the trie. If an element is already in the trie, we ignore it. The trie nodes keep track of the count of each element. We then traverse the trie and copy the elements with a count of 1 back to the input array.

**TrieNode Structure:**
```cpp
struct TrieNode {
    int count;
    unordered_map<int, TrieNode*> children;
};
```

**Approach 3 Code:**
```cpp
class Solution {
private:
    TrieNode* root;
    
public:
    Solution() {
        root = new TrieNode();
    }
    
    int removeDuplicates(vector<int>& nums) {
        int idx = 0;
        
        for (int num : nums) {
            if (insert(root, num)) {
                nums[idx++] = num;
            }
        }
        
        return idx;
    }
    
    bool insert(TrieNode* node, int num) {
        if (node->children.find(num) == node->children.end()) {
            node->children[num] = new TrieNode();
            node->children[num]->count = 1;
            return true;
        } else {
            node->children[num]->count++;
            return false;
        }
    }
};
```
**Time Complexity:** O(n log n), where n is the length of the input array. The log n factor comes from the insertion and deletion operations in the trie.
**Space Complexity:** O(n), as we are using a trie to store the unique elements.

---

**Note:** The other algorithms mentioned (Bitwise Operations, Sweep Line Techniques, Graph Algorithms, and Dynamic Programming) are not applicable to this problem.