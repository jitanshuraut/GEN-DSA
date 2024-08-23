## Question:

"longest-consecutive-sequence-in-an-array/: Problem Statement: You are given an array of ‘N’ integers. You need to find the length of the longest sequence which contains the consecutive elements."

## Approach 1: Brute Force

**Explanation:**
A straightforward approach is to check for every possible starting point in the array, if the next element exists, increment the length. Keep track of the maximum length encountered.

**Brute Force Code:**
```cpp
int longestConsecutive(vector<int>& nums) {
    int n = nums.size();
    int maxLength = 1;
    
    for (int i=0; i<n; i++) {
        int currLength = 1;
        int next = nums[i] + 1;
        
        while (find(nums.begin(), nums.end(), next) != nums.end()) {
            currLength++;
            next++;
        }
        
        maxLength = max(maxLength, currLength);
    }
    
    return maxLength;
}
```

**Time and Space Complexity Analysis:**
* **Time Complexity**: O(n^2), where n is the number of elements in the array. For each element, we search for the next element, which takes O(n) time.
* **Space Complexity**: O(1), as we don't use any additional space for data structures.

## Approach 2: Using a Set (Optimized)

**Explanation:**
We can use a set to store all the elements in the array. Since a set stores unique elements, we can check if an element exists in the set in O(1) time. This allows us to efficiently check for the presence of consecutive elements and update the maximum length accordingly.

**Optimized Code:**
```cpp
int longestConsecutive(vector<int>& nums) {
    set<int> numSet(nums.begin(), nums.end());
    int maxLength = 1;
    
    for (int num : numSet) {
        int currLength = 1;
        int next = num + 1;
        
        while (numSet.find(next) != numSet.end()) {
            currLength++;
            next++;
        }
        
        maxLength = max(maxLength, currLength);
    }
    
    return maxLength;
}
```

**Time and Space Complexity Analysis:**
* **Time Complexity**: O(n log n), where n is the number of elements in the array. We use a set to store the elements, which takes O(n log n) time.
* **Space Complexity**: O(n), as we store all the elements in the set.

## Approach 3: Using a Map (Optimized)

**Explanation:**
We can use a map to store the elements in the array along with their consecutive length. This allows us to quickly retrieve the consecutive length for each element and update it as we iterate over the sequence.

**Optimized Code:**
```cpp
int longestConsecutive(vector<int>& nums) {
    unordered_map<int, int> numMap;
    int maxLength = 1;
    
    for (int num : nums) {
        if (numMap.find(num) != numMap.end()) {
            continue;
        }
        
        int left = num - 1;
        int right = num + 1;
        
        while (numMap.find(left) != numMap.end()) {
            left--;
        }
        
        while (numMap.find(right) != numMap.end()) {
            right++;
        }
        
        int currLength = right - left - 1;
        maxLength = max(maxLength, currLength);
        numMap[num] = currLength;
        numMap[left] = currLength;
        numMap[right] = currLength;
    }
    
    return maxLength;
}
```

**Time and Space Complexity Analysis:**
* **Time Complexity**: O(n log n), where n is the number of elements in the array. We use a map to store the elements, which takes O(1) time for insertion and retrieval.
* **Space Complexity**: O(n), as we store all the elements in the map.

## Approach 4: Using a Sliding Window (Two Pointers)

**Explanation:**
We can use two pointers to define a sliding window that represents the current consecutive sequence. As we move the pointers, we update the length of the sequence and the maximum length encountered.

**Two Pointers Code:**
```cpp
int longestConsecutive(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    int maxLength = 1;
    int start = 0;
    
    for (int end=1; end<nums.size(); end++) {
        if (nums[end] == nums[end-1]) {
            continue;
        }
        
        if (nums[end] - nums[end-1] == 1) {
            maxLength = max(maxLength, end - start + 1);
        } else {
            start = end;
        }
    }
    
    return maxLength;
}
```

**Time and Space Complexity Analysis:**
* **Time Complexity**: O(n log n), where n is the number of elements in the array. We sort the array, which takes O(n log n) time.
* **Space Complexity**: O(1), as we don't use any additional space for data structures.**Question**: longest-consecutive-sequence-in-an-array/: Problem Statement: You are given an array of ‘N’ integers. You need to find the length of the longest sequence which contains the consecutive elements.

**Approach 1: Brute Force**

**Explanation**: This approach involves iterating over the array and checking each element to see if it is a part of a consecutive sequence. If it is, we continue iterating until the sequence ends. The length of the longest sequence found is stored in a variable and updated as we iterate through the array.

**Approach 1 Code**:

```c++
int longestConsecutive(vector<int>& nums) {
    int maxLen = 0;
    unordered_set<int> numSet(nums.begin(), nums.end());
    
    for (int num : nums) {
        if (!numSet.count(num - 1)) {
            int currNum = num;
            int currLen = 1;
            
            while (numSet.count(currNum + 1)) {
                currNum++;
                currLen++;
            }
            
            maxLen = max(maxLen, currLen);
        }
    }
    
    return maxLen;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(N^2), where N is the number of elements in the array. The outer loop iterates over all elements in the array, and the inner loop checks for the consecutive sequence starting from each element.
* **Space Complexity**: O(N), as we store the elements in an unordered set to check for their presence efficiently.

**Approach 2: Sorting**

**Explanation**: This approach involves sorting the array first and then iterating over it to find the length of the longest consecutive sequence. We keep track of the current sequence length and update it as we iterate through the array.

**Approach 2 Code**:

```c++
int longestConsecutive(vector<int>& nums) {
    if (nums.empty()) {
        return 0;
    }
    
    sort(nums.begin(), nums.end());
    
    int currLen = 1;
    int maxLen = 1;
    
    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] == nums[i - 1]) {
            continue;
        }
        
        if (nums[i] == nums[i - 1] + 1) {
            currLen++;
        } else {
            maxLen = max(maxLen, currLen);
            currLen = 1;
        }
    }
    
    return max(maxLen, currLen);
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(N log N), where N is the number of elements in the array. Sorting the array dominates the time complexity.
* **Space Complexity**: O(1), as we do not use any additional data structures.

**Approach 3: Union-Find**

**Explanation**: This approach uses the Union-Find data structure to efficiently maintain connected components in the array. We treat each element as a node in a graph, and initialize each node as its own component. We then iterate over the array and for each element, we find its consecutive element (if it exists) and merge the components containing these elements. The length of the longest consecutive sequence is equal to the size of the largest component in the Union-Find data structure.

**Approach 3 Code**:

```c++
class UnionFind {
public:
    UnionFind(int n) {
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }
    
    int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }
    
    void unionSet(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (size[rootX] < size[rootY]) {
                parent[rootX] = rootY;
                size[rootY] += size[rootX];
            } else {
                parent[rootY] = rootX;
                size[rootX] += size[rootY];
            }
        }
    }
private:
    int parent[100001];
    int size[100001];
};

int longestConsecutive(vector<int>& nums) {
    unordered_map<int, int> numToIdx;
    for (int i = 0; i < nums.size(); i++) {
        numToIdx[nums[i]] = i;
    }
    
    UnionFind uf(nums.size());
    int maxLen = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (numToIdx.count(nums[i] - 1)) {
            uf.unionSet(numToIdx[nums[i]], numToIdx[nums[i] - 1]);
        }
        if (numToIdx.count(nums[i] + 1)) {
            uf.unionSet(numToIdx[nums[i]], numToIdx[nums[i] + 1]);
        }
        maxLen = max(maxLen, uf.size[uf.find(numToIdx[nums[i]])]);
    }
    
    return maxLen;
}
```

**Time and Space Complexity Analysis for Approach 3**:

* **Time Complexity**: O(N log N), where N is the number of elements in the array. The Union-Find operations dominate the time complexity.
* **Space Complexity**: O(N), as we use a map to store the elements and their indices.