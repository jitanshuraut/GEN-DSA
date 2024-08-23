**Question:** 3-sum-find-triplets-that-add-up-to-a-zero/: Problem Statement: Given an array of N integers, your task is to find unique triplets that add up to give a sum of zero. In short, you need to return an array of all the unique triplets [arr[a], arr[b], arr[c]] such that i!=j, j!=k, k!=i, and their sum is equal to zero.

**Approach 1: Brute Force**

**Explanation:**

This approach involves iterating over all possible triplets in the array and checking if their sum equals zero. It has a time complexity of O(n^3), where n is the number of elements in the array.

**Approach 1 Code:**

```cpp
void findTriplets(int arr[], int n) {
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      for (int k = j + 1; k < n; k++) {
        if (arr[i] + arr[j] + arr[k] == 0) {
          cout << "[ " << arr[i] << ", " << arr[j] << ", " << arr[k] << " ]" << endl;
        }
      }
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 1:**

* Time Complexity: O(n^3)
* Space Complexity: O(1)

**Approach 2: Optimized Approaches using Maps**

**Explanation:**

This approach uses a hash map to track the elements seen in the array. For each element, it checks if the negative of the sum of the other two elements is present in the map. If so, it forms a triplet with those two elements. This approach has a time complexity of O(n^2), where n is the number of elements in the array.

**Approach 2 Code:**

```cpp
void findTriplets(int arr[], int n) {
  unordered_map<int, int> m;
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      int sum = -(arr[i] + arr[j]);
      if (m.find(sum) != m.end()) {
        cout << "[ " << arr[i] << ", " << arr[j] << ", " << m[sum] << " ]" << endl;
      } else {
        m[arr[j]] = arr[j];
      }
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 2:**

* Time Complexity: O(n^2)
* Space Complexity: O(n)

**Approach 3: Optimized Approaches using Binary Search**

**Explanation:**

This approach uses binary search to find the third element that completes the triplet. It first sorts the array and then, for each element, it uses binary search to find the negative of the sum of the other two elements. If found, it forms a triplet with those two elements. This approach has a time complexity of O(n^2 log n), where n is the number of elements in the array.

**Approach 3 Code:**

```cpp
void findTriplets(int arr[], int n) {
  sort(arr, arr + n);
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      int sum = -(arr[i] + arr[j]);
      int low = j + 1;
      int high = n - 1;
      while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == sum) {
          cout << "[ " << arr[i] << ", " << arr[j] << ", " << arr[mid] << " ]" << endl;
          break;
        } else if (arr[mid] < sum) {
          low = mid + 1;
        } else {
          high = mid - 1;
        }
      }
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 3:**

* Time Complexity: O(n^2 log n)
* Space Complexity: O(1)

**Approach 4: Optimized Approaches using Two Pointers**

**Explanation:**

This approach uses two pointers to find the third element that completes the triplet. It first sorts the array and then uses two pointers to traverse the sorted array. One pointer starts from the beginning, and the other pointer starts from the end. The pointers move towards each other until they find a triplet whose sum is zero. This approach has a time complexity of O(n^2), where n is the number of elements in the array.

**Approach 4 Code:**

```cpp
void findTriplets(int arr[], int n) {
  sort(arr, arr + n);
  for (int i = 0; i < n; i++) {
    int j = i + 1;
    int k = n - 1;
    while (j < k) {
      int sum = arr[i] + arr[j] + arr[k];
      if (sum == 0) {
        cout << "[ " << arr[i] << ", " << arr[j] << ", " << arr[k] << " ]" << endl;
        j++;
        k--;
      } else if (sum < 0) {
        j++;
      } else {
        k--;
      }
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 4:**

* Time Complexity: O(n^2)
* Space Complexity: O(1)

**Approach 5: Greedy Algorithms**

**Explanation:**

This approach uses a greedy algorithm to find the triplets that add up to zero. It starts by sorting the array and then iterates over the sorted array. For each element, it finds the two elements that complete the triplet by iterating over the remaining elements in the sorted array. This approach has a time complexity of O(n^2), where n is the number of elements in the array.

**Approach 5 Code:**

```cpp
void findTriplets(int arr[], int n) {
  sort(arr, arr + n);
  for (int i = 0; i < n; i++) {
    int j = i + 1;
    int k = n - 1;
    while (j < k) {
      int sum = arr[i] + arr[j] + arr[k];
      if (sum == 0) {
        cout << "[ " << arr[i] << ", " << arr[j] << ", " << arr[k] << " ]" << endl;
        j++;
        k--;
      } else if (sum < 0) {
        j++;
      } else {
        k--;
      }
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 5:**

* Time Complexity: O(n^2)
* Space Complexity: O(1)

**Approach 6: Recursive**

**Explanation:**

This approach uses a recursive algorithm to find the triplets that add up to zero. It starts by sorting the array and then calls a recursive function that takes three elements and their sum as parameters. The recursive function checks if the sum of the**Question:** 3-sum-find-triplets-that-add-up-to-a-zero/: Problem Statement: Given an array of N integers, your task is to find unique triplets that add up to give a sum of zero. In short, you need to return an array of all the unique triplets [arr[a], arr[b], arr[c]] such that i!=j, j!=k, k!=i, and their sum is equal to zero.

**Approach 1: Brute Force**
**Explanation:** This is the simplest approach to this problem. We can iterate over all possible triplets of elements in the array and check if their sum is equal to zero. If it is, we add the triplet to our result.

**Approach 1 Code:**
```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> res;
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            for (int k = j + 1; k < nums.size(); k++) {
                if (nums[i] + nums[j] + nums[k] == 0) {
                    res.push_back({nums[i], nums[j], nums[k]});
                }
            }
        }
    }
    return res;
}
```

**Time and Space Complexity Analysis for Approach 1:**
* **Time Complexity:** O(n^3), where n is the number of elements in the array. This is because we are iterating over all possible triplets of elements, which takes O(n^3) time.
* **Space Complexity:** O(1), as we are not using any additional data structures.

**Approach 2: Sorting and Two Pointers**
**Explanation:** This approach is more efficient than the brute force approach. We can first sort the array in O(n log n) time. Then, we can use two pointers to iterate through the sorted array in O(n^2) time. The two pointers will start at the beginning and end of the array, and they will move towards each other until they meet. At each step, we will check if the sum of the three elements pointed to by the two pointers is equal to zero. If it is, we will add the triplet to our result.

**Approach 2 Code:**
```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> res;
    sort(nums.begin(), nums.end());
    for (int i = 0; i < nums.size(); i++) {
        int j = i + 1, k = nums.size() - 1;
        while (j < k) {
            int sum = nums[i] + nums[j] + nums[k];
            if (sum == 0) {
                res.push_back({nums[i], nums[j], nums[k]});
                while (j < k && nums[j] == nums[j + 1]) j++;
                while (j < k && nums[k] == nums[k - 1]) k--;
                j++;
                k--;
            } else if (sum < 0) {
                j++;
            } else {
                k--;
            }
        }
    }
    return res;
}
```

**Time and Space Complexity Analysis for Approach 2:**
* **Time Complexity:** O(n^2), where n is the number of elements in the array. This is because we are sorting the array in O(n log n) time and then iterating through the sorted array in O(n^2) time.
* **Space Complexity:** O(1), as we are not using any additional data structures.

**Approach 3: Hashing**
**Explanation:** This approach is the most efficient of the three approaches. We can use a hash table to store the elements of the array, along with their indices. Then, for each element in the array, we can iterate through the hash table and check if the sum of the element and two other elements in the hash table is equal to zero. If it is, we add the triplet to our result.

**Approach 3 Code:**
```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> res;
    unordered_map<int, vector<int>> hash;
    for (int i = 0; i < nums.size(); i++) {
        hash[nums[i]].push_back(i);
    }
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            int complement = -(nums[i] + nums[j]);
            if (hash.count(complement) > 0) {
                for (int k = 0; k < hash[complement].size(); k++) {
                    if (hash[complement][k] != i && hash[complement][k] != j) {
                        res.push_back({nums[i], nums[j], nums[hash[complement][k]]});
                    }
                }
            }
        }
    }
    return res;
}
```

**Time and Space Complexity Analysis for Approach 3:**
* **Time Complexity:** O(n^2), where n is the number of elements in the array. This is because we are iterating through the array twice, and for each element, we are iterating through the hash table, which takes O(n) time.
* **Space Complexity:** O(n), as we are using a hash table to store the elements of the array.