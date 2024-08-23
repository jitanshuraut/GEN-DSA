## Question:

4-sum-find-quads-that-add-up-to-a-target-value/: Problem Statement: Given an array of N integers, your task is to find unique quads that add up to give a target value. In short, you need to return an array of all the unique quadruplets [arr[a], arr[b], arr[c], arr[d]] such that their sum is equal to a given target.

## Approach 1: Brute Force

**Explanation:**

This is the most straightforward approach. We can generate all possible combinations of four elements from the array and check if their sum matches the target.

**Code:**

```cpp
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    vector<vector<int>> result;
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            for (int k = j + 1; k < nums.size(); k++) {
                for (int l = k + 1; l < nums.size(); l++) {
                    if (nums[i] + nums[j] + nums[k] + nums[l] == target) {
                        result.push_back({nums[i], nums[j], nums[k], nums[l]});
                    }
                }
            }
        }
    }
    return result;
}
```

**Time and Space Complexity Analysis:**

Time complexity: O(n^4), where n is the number of elements in the array.
Space complexity: O(1), no additional space is used.

## Approach 2: Optimized Approaches using Maps

**Explanation:**

Instead of brute-force, we can use a hash map to store the sum of pairs and their corresponding indices. For each element, we can check if the target minus the current element's value exists in the map and retrieve the corresponding indices. This reduces the time complexity to O(n^3).

**Code:**

```cpp
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    vector<vector<int>> result;
    unordered_map<int, vector<pair<int, int>>> sum_map;

    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            sum_map[nums[i] + nums[j]].push_back({i, j});
        }
    }

    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            int complement = target - nums[i] - nums[j];
            if (sum_map.count(complement)) {
                for (auto pair : sum_map[complement]) {
                    if (pair.first != i && pair.first != j && pair.second != i && pair.second != j) {
                        result.push_back({nums[i], nums[j], nums[pair.first], nums[pair.second]});
                    }
                }
            }
        }
    }
    return result;
}
```

**Time and Space Complexity Analysis:**

Time complexity: O(n^3), where n is the number of elements in the array.
Space complexity: O(n^2), for storing the sum of pairs in the hash map.

## Approach 3: Optimized Approaches using Two Pointers

**Explanation:**

We can sort the array and use two pointers starting from the first and last elements. We can move the pointers towards the center or away from the center based on the sum of the current four elements. This reduces the time complexity to O(n^3).

**Code:**

```cpp
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    vector<vector<int>> result;
    sort(nums.begin(), nums.end());

    for (int i = 0; i < nums.size(); i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        for (int j = nums.size() - 1; j >= 0; j--) {
            if (j < nums.size() - 1 && nums[j] == nums[j + 1]) continue;
            int left = i + 1, right = j - 1;
            while (left < right) {
                int sum = nums[i] + nums[j] + nums[left] + nums[right];
                if (sum == target) {
                    result.push_back({nums[i], nums[left], nums[right], nums[j]});
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                } else if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
    }
    return result;
}
```

**Time and Space Complexity Analysis:**

Time complexity: O(n^3), where n is the number of elements in the array.
Space complexity: O(1), no additional space is used.**Question**: 4-sum-find-quads-that-add-up-to-a-target-value/: Problem Statement: Given an array of N integers, your task is to find unique quads that add up to give a target value. In short, you need to return an array of all the unique quadruplets [arr[a], arr[b], arr[c], arr[d]] such that their sum is equal to a given target.

**Approach 1: Brute Force**

**Explanation**: This is the most straightforward approach, where we generate all possible subsets of 4 elements and check if their sum equals the target.

**Approach 1 Code**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<vector<int>> fourSum(vector<int>& nums, int target) {
  // Sort the array to easily find combinations
  sort(nums.begin(), nums.end());

  // Initialize the result vector
  vector<vector<int>> res;

  for(int i = 0; i < nums.size() - 3; i++){
    for(int j = i + 1; j < nums.size() - 2; j++){
      for(int k = j + 1; k < nums.size() - 1; k++){
        for(int l = k + 1; l < nums.size(); l++){
          if(nums[i] + nums[j] + nums[k] + nums[l] == target){
            // Check if the quadruplet is unique
            bool unique = true;
            for(int m = 0; m < res.size(); m++){
              if(res[m][0] == nums[i] && res[m][1] == nums[j] && res[m][2] == nums[k] && res[m][3] == nums[l]){
                unique = false;
                break;
              }
            }
            if(unique) res.push_back({nums[i], nums[j], nums[k], nums[l]});
          }
        }
      }
    }
  }
  return res;
}

int main() {
  vector<int> nums = {1, 0, -1, 0, 2, -2, 4, 5};
  int target = 8;
  vector<vector<int>> res = fourSum(nums, target);
  for(int i = 0; i < res.size(); i++){
    for(int j = 0; j < res[i].size(); j++){
      cout << res[i][j] << " ";
    }
    cout << endl;
  }
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(n^4), where n is the number of elements in the array.
* **Space Complexity**: O(1)

**Approach 2: Hash Table**

**Explanation**: This approach uses a hash table to store the pairs of elements that sum up to the target.

**Approach 2 Code**:

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

vector<vector<int>> fourSum(vector<int>& nums, int target) {
  // Initialize the result vector
  vector<vector<int>> res;

  // Create a hash table to store the pairs of elements that sum up to the target
  unordered_map<int, vector<pair<int, int>>> mp;
  for(int i = 0; i < nums.size(); i++){
    for(int j = i + 1; j < nums.size(); j++){
      int sum = nums[i] + nums[j];
      mp[sum].push_back({i, j});
    }
  }

  // Iterate over the hash table and check if the remaining sum is present in the hash table
  for(auto it = mp.begin(); it != mp.end(); it++){
    int sum = it->first;
    vector<pair<int, int>> pairs = it->second;
    for(int i = 0; i < pairs.size(); i++){
      int a = pairs[i].first;
      int b = pairs[i].second;
      int remaining = target - sum;
      if(mp.find(remaining) != mp.end()){
        vector<pair<int, int>> pairs2 = mp[remaining];
        for(int j = 0; j < pairs2.size(); j++){
          int c = pairs2[j].first;
          int d = pairs2[j].second;
          if(a != c && a != d && b != c && b != d){
            res.push_back({nums[a], nums[b], nums[c], nums[d]});
          }
        }
      }
    }
  }
  return res;
}

int main() {
  vector<int> nums = {1, 0, -1, 0, 2, -2, 4, 5};
  int target = 8;
  vector<vector<int>> res = fourSum(nums, target);
  for(int i = 0; i < res.size(); i++){
    for(int j = 0; j < res[i].size(); j++){
      cout << res[i][j] << " ";
    }
    cout << endl;
  }
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(n^2), where n is the number of elements in the array
* **Space Complexity**: O(n^2)

**Approach 3: Two Pointers**

**Explanation**: This approach uses two pointers to iterate over the array and find the pairs of elements that sum up to the target.

**Approach 3 Code**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<vector<int>> fourSum(vector<int>& nums, int target) {
  // Sort the array to easily find combinations
  sort(nums.begin(), nums.end());

  // Initialize the result vector
  vector<vector<int>> res;

  for(int i = 0; i < nums.size() - 3; i++){
    // Skip duplicate elements
    if(i > 0 && nums[i] == nums[i - 1]) continue;
    for(int j = i + 1; j < nums.size() - 2; j++){
      // Skip duplicate elements
      if(j > i + 1 && nums[j] == nums[j - 1]) continue;
      int left = j + 1;
      int right = nums.size() - 1;
      while(left < right){
        int sum = nums[i] + nums[j] + nums[left] + nums[right];
        if(sum == target){
          res.push_back({nums[i], nums[j], nums[left], nums[right]});
          // Skip duplicate elements
          while(left < right && nums[left] == nums[left + 1]) left++;
          while(left < right && nums[right] == nums[right - 1]) right--;
          left++;
          right--;
        } else if(sum < target){
          left++;
        } else {
          right--;
        }
      }
    }
  }
  return res;
}

int main() {
  vector<int> nums = {1, 0, -1, 0, 2, -2, 4, 5};
  int target = 8;
  vector<vector<int>> res = fourSum(nums, target);
  for(int i = 0; i < res.size(); i