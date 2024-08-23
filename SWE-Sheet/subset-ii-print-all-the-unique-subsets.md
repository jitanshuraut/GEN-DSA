**Question**: subset-ii-print-all-the-unique-subsets/: Problem Statement: Given an array of integers that may contain duplicates the task is to return all possible subsets. Return only unique subsets and they can be in any order.

**Approach 1: Brute Force**

**Explanation**: The brute force approach is to generate all possible subsets of the given array and then check for duplicates. To generate all possible subsets, we can use a recursive function that takes two parameters: the current subset and the index of the next element in the array. The function will then call itself recursively to generate all possible subsets of the remaining elements in the array, and it will add the current element to each of these subsets. The function will then return the list of all possible subsets.
To check for duplicates, we can use a set. We will add each subset to the set, and if the subset is already in the set, then we will skip it.

**Approach 1 Code**:

```cpp
#include <vector>
#include <set>
#include <iostream>
using namespace std;

void generateSubsets(vector<int>& nums, set<vector<int>>& subsets, vector<int>& currentSubset, int index) {
    if (index == nums.size()) {
        subsets.insert(currentSubset);
        return;
    }
    currentSubset.push_back(nums[index]);
    generateSubsets(nums, subsets, currentSubset, index + 1);
    currentSubset.pop_back();
    generateSubsets(nums, subsets, currentSubset, index + 1);
}

vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    set<vector<int>> subsets;
    vector<int> currentSubset;
    generateSubsets(nums, subsets, currentSubset, 0);
    return vector<vector<int>>(subsets.begin(), subsets.end());
}

int main() {
    vector<int> nums = {1, 2, 2};
    vector<vector<int>> subsets = subsetsWithDup(nums);
    for (auto& subset : subsets) {
        for (auto& element : subset) {
            cout << element << " ";
        }
        cout << endl;
    }
    return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* Time complexity: O(2^n), where n is the size of the input array. This is because we need to generate all possible subsets of the array, and there are 2^n possible subsets.
* Space complexity: O(n), where n is the size of the input array. This is because we need to store the current subset and the index of the next element in the array.

**Approach 2: Optimized Approaches using Maps, Multisets, Binary Search, Two Pointers**

**Explanation**: We can use a map to store the frequency of each element in the array. Then, we can use this map to generate all possible subsets of the array, taking care to avoid duplicates. To generate all possible subsets, we can use a recursive function that takes two parameters: the current subset and the map of element frequencies. The function will then call itself recursively to generate all possible subsets of the remaining elements in the array, and it will add the current element to each of these subsets. The function will then return the list of all possible subsets.
To avoid duplicates, we can check the frequency of the current element in the map. If the frequency is greater than 1, then we can add the current element to the current subset multiple times. The function will then return the list of all possible subsets, taking care to avoid duplicates.

**Approach 2 Code**:

```cpp
#include <vector>
#include <map>
#include <set>
#include <iostream>
using namespace std;

void generateSubsets(map<int, int>& elementFrequencies, set<vector<int>>& subsets, vector<int>& currentSubset, int index) {
    if (index == elementFrequencies.size()) {
        subsets.insert(currentSubset);
        return;
    }
    int element = elementFrequencies.begin()->first;
    int frequency = elementFrequencies.begin()->second;
    elementFrequencies.erase(elementFrequencies.begin());
    for (int i = 0; i <= frequency; i++) {
        for (int j = 0; j < i; j++) {
            currentSubset.push_back(element);
        }
        generateSubsets(elementFrequencies, subsets, currentSubset, index + 1);
        for (int j = 0; j < i; j++) {
            currentSubset.pop_back();
        }
    }
    elementFrequencies[element] = frequency;
}

vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    map<int, int> elementFrequencies;
    for (auto& num : nums) {
        elementFrequencies[num]++;
    }
    set<vector<int>> subsets;
    vector<int> currentSubset;
    generateSubsets(elementFrequencies, subsets, currentSubset, 0);
    return vector<vector<int>>(subsets.begin(), subsets.end());
}

int main() {
    vector<int> nums = {1, 2, 2};
    vector<vector<int>> subsets = subsetsWithDup(nums);
    for (auto& subset : subsets) {
        for (auto& element : subset) {
            cout << element << " ";
        }
        cout << endl;
    }
    return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* Time complexity: O(2^n), where n is the size of the input array. This is because we need to generate all possible subsets of the array, and there are 2^n possible subsets.
* Space complexity: O(n), where n is the size of the input array. This is because we need to store the map of element frequencies, the current subset, and the index of the next element in the array.

**Approach 3: Greedy Algorithms**

**Explanation**: We can use a greedy algorithm to generate all possible subsets of the array. The greedy algorithm will start with the empty subset and then iteratively add elements to the subset. At each step, the algorithm will add the element that is most likely to## Question

Given an array of integers that may contain duplicates the task is to return all possible subsets. Return only unique subsets and they can be in any order.

## Approach 1: Bitwise Operations

### Explanation

We can use bitwise operations to generate all possible subsets of a given set. Each subset is represented by a bitmask, where each bit corresponds to an element in the set. If the bit is set, then the corresponding element is included in the subset.

To generate all possible subsets, we can start with a bitmask of all 0s, and then iteratively set each bit to 1. For each bitmask, we can then extract the corresponding subset by finding the elements that correspond to the set bits.

To avoid generating duplicate subsets, we can use a set to store the already generated subsets. Whenever we generate a new subset, we can check if it is already in the set. If it is, then we can discard it.

### Code

```cpp
#include <bits/stdc++.h>

using namespace std;

vector<vector<int>> subsetsWithDup(vector<int>& nums) {
  set<vector<int>> subsets;
  int n = nums.size();
  int totalSubsets = (1 << n);

  for (int i = 0; i < totalSubsets; i++) {
    vector<int> subset;
    for (int j = 0; j < n; j++) {
      if (i & (1 << j)) {
        subset.push_back(nums[j]);
      }
    }
    subsets.insert(subset);
  }

  return vector<vector<int>>(subsets.begin(), subsets.end());
}
```

### Time and Space Complexity Analysis

* **Time Complexity**: O(2^n), where n is the length of the given array.
* **Space Complexity**: O(2^n), to store the generated subsets.

## Approach 2: Backtracking

### Explanation

We can use backtracking to generate all possible subsets of a given set. The basic idea of backtracking is to generate a candidate solution, and then recursively explore all possible extensions of that candidate solution.

To generate a candidate solution, we can start with an empty subset. Then, we can iteratively add each element of the set to the subset, and recursively explore all possible extensions of that subset.

To avoid generating duplicate subsets, we can use a set to store the already generated subsets. Whenever we generate a new subset, we can check if it is already in the set. If it is, then we can discard it.

### Code

```cpp
#include <bits/stdc++.h>

using namespace std;

vector<vector<int>> subsetsWithDup(vector<int>& nums) {
  set<vector<int>> subsets;
  vector<int> subset;
  backtrack(nums, 0, subset, subsets);
  return vector<vector<int>>(subsets.begin(), subsets.end());
}

void backtrack(vector<int>& nums, int start, vector<int>& subset, set<vector<int>>& subsets) {
  subsets.insert(subset);

  for (int i = start; i < nums.size(); i++) {
    subset.push_back(nums[i]);
    backtrack(nums, i + 1, subset, subsets);
    subset.pop_back();
  }
}
```

### Time and Space Complexity Analysis

* **Time Complexity**: O(2^n), where n is the length of the given array.
* **Space Complexity**: O(n + 2^n), to store the generated subsets and the current subset.