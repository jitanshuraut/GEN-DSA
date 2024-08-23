**Question**: Count Reverse Pairs: Given an array of numbers, you need to return the count of reverse pairs. Reverse Pairs are those pairs where i<j and arr[i]>2*arr[j].

**Approach 1: Brute Force**

**Explanation**: This approach involves checking every possible pair in the array to identify reverse pairs.

**C++ Code**:
```cpp
int countReversePairsBruteForce(vector<int>& nums) {
    int count = 0;
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            if (nums[i] > 2 * nums[j]) {
                count++;
            }
        }
    }
    return count;
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: O(n^2), where n is the size of the input array.
* Space Complexity: O(1), as no additional space is required.

**Approach 2: Using Merge Sort**

**Explanation**: This approach utilizes the merge sort algorithm to count reverse pairs efficiently.

**C++ Code**:
```cpp
int merge(vector<int>& nums, int low, int mid, int high) {
    int i = low, j = mid + 1, count = 0;
    vector<int> merged;
    
    while (i <= mid && j <= high) {
        if (nums[i] <= 2 * nums[j]) {
            merged.push_back(nums[i++]);
        } else {
            merged.push_back(nums[j++]);
            count += mid - i + 1;
        }
    }
    
    while (i <= mid) merged.push_back(nums[i++]);
    while (j <= high) merged.push_back(nums[j++]);
    
    copy(merged.begin(), merged.end(), nums.begin() + low);
    
    return count;
}

int mergeSort(vector<int>& nums, int low, int high) {
    if (low == high) return 0;
    
    int mid = low + (high - low) / 2;
    
    return mergeSort(nums, low, mid) + mergeSort(nums, mid + 1, high) + merge(nums, low, mid, high);
}

int countReversePairsMergeSort(vector<int>& nums) {
    return mergeSort(nums, 0, nums.size() - 1);
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: O(n log n), where n is the size of the input array.
* Space Complexity: O(n), as additional space is required for the merged array during merge sort.

**Approach 3: Using Binary Indexed Tree (BIT)**

**Explanation**: This approach uses a Binary Indexed Tree to count reverse pairs efficiently. A BIT is a data structure that can efficiently answer range queries on an array.

**C++ Code**:
```cpp
class BIT {
    vector<int> tree;
public:
    BIT(int n) { tree.resize(n + 1, 0); }
    
    void update(int index, int value) {
        while (index < tree.size()) {
            tree[index] += value;
            index += index & -index;
        }
    }
    
    int query(int index) {
        int sum = 0;
        while (index > 0) {
            sum += tree[index];
            index -= index & -index;
        }
        return sum;
    }
};

int countReversePairsBIT(vector<int>& nums) {
    int n = nums.size();
    
    // Initialize BIT with frequencies of elements
    BIT bit(2 * n);
    for (int i = 0; i < n; i++) {
        bit.update(nums[i], 1);
    }
    
    int count = 0;
    for (int i = n - 1; i >= 0; i--) {
        count += bit.query(nums[i] / 2);
        bit.update(nums[i], -1);
    }
    
    return count;
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: O(n log n), where n is the size of the input array.
* Space Complexity: O(2n), as additional space is required for the BIT.**Question**: count-reverse-pairs/: Problem Statement: Given an array of numbers, you need to return the count of reverse pairs. Reverse Pairs are those pairs where i<j and arr[i]>2*arr[j].

**Approach 1: Brute Force**

**Explanation**: The brute force approach involves checking all possible pairs of elements in the array and determining if they constitute a reverse pair.

**Approach 1 Code**:

```cpp
int countReversePairs(vector<int>& nums) {
    int count = 0;
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i+1; j < nums.size(); j++) {
            if (nums[i] > 2 * nums[j]) {
                count++;
            }
        }
    }
    return count;
}
```

**Time and Space Complexity Analysis for Approach 1**:
Time Complexity: O(n^2), where n is the length of the array.
Space Complexity: O(1).

**Approach 2: Merge Sort with Modification**

**Explanation**: This approach leverages the divide-and-conquer paradigm of merge sort with a modification to count reverse pairs during the merge operation.

**Approach 2 Code**:

```cpp
int countReversePairs(vector<int>& nums) {
    int count = 0;
    mergeSort(nums, 0, nums.size()-1, count);
    return count;
}

void mergeSort(vector<int>& nums, int left, int right, int& count) {
    if (left >= right) {
        return;
    }
    int mid = left + (right - left) / 2;
    mergeSort(nums, left, mid, count);
    mergeSort(nums, mid+1, right, count);
    merge(nums, left, mid, right, count);
}

void merge(vector<int>& nums, int left, int mid, int right, int& count) {
    vector<int> temp(right - left + 1);
    int i = left, j = mid+1, k = 0;
    while (i <= mid && j <= right) {
        if (nums[i] <= nums[j]) {
            temp[k++] = nums[i++];
        } else {
            count += (mid - i + 1);
            temp[k++] = nums[j++];
        }
    }
    while (i <= mid) {
        temp[k++] = nums[i++];
    }
    while (j <= right) {
        temp[k++] = nums[j++];
    }
    for (int i = left; i <= right; i++) {
        nums[i] = temp[i - left];
    }
}
```

**Time and Space Complexity Analysis for Approach 2**:
Time Complexity: O(nlogn), where n is the length of the array. This is due to the inherent time complexity of merge sort.
Space Complexity: O(n).

**Approach 3: Using Binary Indexed Tree (BIT)**

**Explanation**: This approach utilizes a Binary Indexed Tree (BIT) to count the number of elements in the array that are less than a given value. We process the array in reverse order, and for each element, we find the count of elements that are greater than 2 * arr[i] in the processed part of the array using BIT. This count gives the number of reverse pairs involving arr[i].

**Approach 3 Code**:

```cpp
int countReversePairs(vector<int>& nums) {
    int n = nums.size();
    vector<int> bit(n+1, 0);  // BIT to store count of elements in the array
    int count = 0;
    for (int i = n-1; i >= 0; i--) {
        count += query(bit, nums[i] / 2);  // Query for the count of elements > 2 * arr[i]
        update(bit, nums[i]);  // Update the BIT for the current element
    }
    return count;
}

int query(vector<int>& bit, int idx) {
    int sum = 0;
    while (idx > 0) {
        sum += bit[idx];
        idx -= (idx & -idx);
    }
    return sum;
}

void update(vector<int>& bit, int idx) {
    while (idx < bit.size()) {
        bit[idx]++;
        idx += (idx & -idx);
    }
}
```

**Time and Space Complexity Analysis for Approach 3**:
Time Complexity: O(nlogn), where n is the length of the array.
Space Complexity: O(n).

**Approach 4: Using Segment Tree**

**Explanation**: This approach uses a segment tree to maintain the count of elements in different ranges of the array. We process the array from left to right. For each element, we use the segment tree to find the count of elements that are greater than 2 * arr[i] in the processed part of the array. This count gives the number of reverse pairs involving arr[i].

**Approach 4 Code**:

```cpp
int countReversePairs(vector<int>& nums) {
    int n = nums.size();
    SegmentTree tree(0, n-1);  // Create a segment tree with range [0, n-1]
    int count = 0;
    for (int i = 0; i < n; i++) {
        count += tree.query(0, i-1, nums[i] / 2);  // Query for the count of elements > 2 * arr[i]
        tree.update(i, nums[i]);  // Update the segment tree for the current element
    }
    return count;
}

class SegmentTree {
public:
    SegmentTree(int start, int end) {
        this->start = start;
        this->end = end;
        this->count = 0;
        if (start == end) {
            return;
        }
        int mid = (start + end) / 2;
        leftChild = new SegmentTree(start, mid);
        rightChild = new SegmentTree(mid+1, end);
    }

    int query(int left, int right, int value) {
        if (left > right || right < start || end < left) {
            return 0;
        }
        if (left <= start && end <= right) {
            return count;
        }
        int mid = (start + end) / 2;
        return leftChild->query(left, right, value) + rightChild->query(left, right, value);
    }

    void update(int idx, int value) {
        if (idx < start || end < idx) {
            return;
        }
        if (start == end) {
            count++;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) {
            leftChild->update(idx, value);
        } else {
            rightChild->update(idx, value);
        }
        count = leftChild->count + rightChild->count;
    }

private:
    int start, end;
    int count;
    SegmentTree *leftChild, *rightChild;
};
```

**Time and Space Complexity Analysis for Approach 4**:
Time Complexity: O(nlogn), where n is the length of the array.
Space Complexity: O(n).