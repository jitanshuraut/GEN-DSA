**Question**: Two Sum: Check if a Pair with Given Sum Exists in Array
**Problem Statement**: Given an array of integers `arr[]` and an integer `target`. Determine if there exists a pair of elements in the array whose sum equals the target.

**Approach 1: Brute Force**
* Iterate through each pair of elements in the array and check if their sum is equal to the target.

```cpp
#include <vector>
#include <iostream>

bool twoSumBruteForce(std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); i++) {
        for (int j = i + 1; j < arr.size(); j++) {
            if (arr[i] + arr[j] == target) {
                return true;
            }
        }
    }
    return false;
}
```

**Time Complexity**: O(n^2), where n is the number of elements in the array.
**Space Complexity**: O(1), as no additional space is required.

**Approach 2: Optimized using an unordered map**
* Create an unordered map that stores the elements of the array as keys and their indices as values.
* Iterate through the array and for each element, check if the (target - element) is present in the map.
* If present, the pair exists.

```cpp
#include <unordered_map>
#include <vector>
#include <iostream>

bool twoSumOptimized(std::vector<int>& arr, int target) {
    std::unordered_map<int, int> map;
    for (int i = 0; i < arr.size(); i++) {
        int complement = target - arr[i];
        if (map.find(complement) != map.end()) {
            return true;
        }
        map[arr[i]] = i;
    }
    return false;
}
```

**Time Complexity**: O(n), where n is the number of elements in the array.
**Space Complexity**: O(n), as we create an unordered map of size n.

**Approach 3: Optimized using a sorted array and two pointers**
* Sort the array in ascending order.
* Start with two pointers, one at the beginning and one at the end.
* Check if the sum of the pointers equals the target.
* If it's less, move the left pointer to the right.
* If it's greater, move the right pointer to the left.

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

bool twoSumTwoPointers(std::vector<int>& arr, int target) {
    std::sort(arr.begin(), arr.end());
    int left = 0;
    int right = arr.size() - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) {
            return true;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return false;
}
```

**Time Complexity**: O(n log n), where n is the number of elements in the array.
**Space Complexity**: O(1), as no additional space is required.**Question**: Two Sum: Check if a pair with a given sum exists in an array.
**Problem Statement**: Given an array of integers `arr[]` and an integer `target`, determine whether there exists a pair of elements in the array that sum up to the target value.

**Approach 1: Brute Force**

* **Explanation**: Iterate over each element in the array and compare it to all subsequent elements to check if their sum equals the target.
* **Code**:
```cpp
bool twoSumBruteForce(int arr[], int n, int target) {
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      if (arr[i] + arr[j] == target) {
        return true;
      }
    }
  }
  return false;
}
```
* **Time and Space Complexity Analysis**: The time complexity is O(n^2) since it performs nested iterations over the array. The space complexity is O(1) as it uses constant extra space.

**Approach 2: Sorting and Linear Search**

* **Explanation**: Sort the array in ascending order and then use binary search to find the complement of the target value for each element.
* **Code**:
```cpp
bool twoSumSortedLinearSearch(int arr[], int n, int target) {
  std::sort(arr, arr + n);

  for (int i = 0; i < n; i++) {
    int complement = target - arr[i];
    int index = std::binary_search(arr, arr + n, complement);
    if (index != -1 && index != i) {
      return true;
    }
  }
  return false;
}
```
* **Time and Space Complexity Analysis**: The time complexity is O(n log n) due to sorting and O(log n) for binary search, totaling to O(n log n). The space complexity is O(1).

**Approach 3: Hash Table**

* **Explanation**: Create a hash table to store the elements of the array as keys. For each element, check if its complement exists in the hash table.
* **Code**:
```cpp
bool twoSumHashTable(int arr[], int n, int target) {
  std::unordered_map<int, bool> hashTable;

  for (int i = 0; i < n; i++) {
    int complement = target - arr[i];
    if (hashTable.find(complement) != hashTable.end()) {
      return true;
    }
    hashTable[arr[i]] = true;
  }
  return false;
}
```
* **Time and Space Complexity Analysis**: The time complexity is O(n) as it iterates over the array once and performs constant-time hash table operations. The space complexity is O(n) since it stores the elements in the hash table.

**Approach 4: Two-Pointer Technique**

* **Explanation**: Use two pointers, one starting at the beginning and one at the end of the array. Move the pointers towards each other while comparing their sum to the target and adjust accordingly.
* **Code**:
```cpp
bool twoSumTwoPointers(int arr[], int n, int target) {
  int left = 0, right = n - 1;

  while (left < right) {
    int sum = arr[left] + arr[right];
    if (sum == target) {
      return true;
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }
  return false;
}
```
* **Time and Space Complexity Analysis**: The time complexity is O(n) since it iterates over the array once. The space complexity is O(1).