**Question**: next_permutation-find-next-lexicographically-greater-permutation/: Problem Statement: Given an array Arr[] of integers, rearrange the numbers of the given array into the lexicographically next greater permutation of numbers.

**Approach 1: Brute Force**

**Explanation**: This approach involves generating all possible permutations of the given array and finding the lexicographically next greater permutation among them.

**Approach 1 Code**:

```cpp
#include <bits/stdc++.h>

using namespace std;

bool nextPermutation(vector<int>& nums) {
  // Find the largest index i where nums[i] < nums[i+1]
  int i = nums.size() - 2;
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If there is no such index, then this is the last permutation
  if (i < 0) {
    return false;
  }

  // Find the largest index j where nums[j] > nums[i]
  int j = nums.size() - 1;
  while (nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Reverse the sub-array nums[i+1:]
  reverse(nums.begin() + i + 1, nums.end());

  // Return true to indicate that the next permutation was found
  return true;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* Time Complexity: O(n!), where n is the size of the input array.
* Space Complexity: O(n), since we need to store a copy of the input array.

**Approach 2: Optimized Approach Using Two Pointers**

**Explanation**: This optimized approach uses two pointers to find the next greater permutation in linear time.

**Approach 2 Code**:

```cpp
#include <bits/stdc++.h>

using namespace std;

bool nextPermutation(vector<int>& nums) {
  // Find the longest decreasing suffix from the right
  int i = nums.size() - 2;
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If there is no such suffix, then this is the last permutation
  if (i < 0) {
    return false;
  }

  // Find the smallest number in the suffix that is greater than nums[i]
  int j = nums.size() - 1;
  while (nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Reverse the suffix
  reverse(nums.begin() + i + 1, nums.end());

  // Return true to indicate that the next permutation was found
  return true;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* Time Complexity: O(n), where n is the size of the input array.
* Space Complexity: O(1), as no additional space is required.

**Approach 3: Recursive Approach**

**Explanation**: This recursive approach involves finding the next permutation by recursively generating all possible permutations.

**Approach 3 Code**:

```cpp
#include <bits/stdc++.h>

using namespace std;

void nextPermutation(vector<int>& nums) {
  // If the array is empty or has only one element, return
  if (nums.empty() || nums.size() == 1) {
    return;
  }

  // Find the pivot element
  int i = nums.size() - 2;
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If there is no pivot element, then this is the last permutation
  if (i < 0) {
    reverse(nums.begin(), nums.end());
    return;
  }

  // Find the smallest number in the suffix that is greater than nums[i]
  int j = nums.size() - 1;
  while (nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Reverse the suffix
  reverse(nums.begin() + i + 1, nums.end());

  // Recursively find the next permutation for the sub-array nums[i+1:]
  nextPermutation(nums.begin() + i + 1, nums.end());
}
```

**Time and Space Complexity Analysis for Approach 3**:

* Time Complexity: O(n!), where n is the size of the input array.
* Space Complexity: O(n), as we need to store a copy of the input array.

**Approach 4: Greedy Approach**

**Explanation**: This greedy approach involves finding the next permutation by greedily swapping elements to maximize the value of the array.

**Approach 4 Code**:

```cpp
#include <bits/stdc++.h>

using namespace std;

bool nextPermutation(vector<int>& nums) {
  // Find the largest index i where nums[i] < nums[i+1]
  int i = nums.size() - 2;
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If there is no such index, then this is the last permutation
  if (i < 0) {
    return false;
  }

  // Find the smallest number in the suffix that is greater than nums[i]
  int j = nums.size() - 1;
  while (nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Sort the suffix in ascending order
  sort(nums.begin() + i + 1, nums.end());

  // Return true to indicate that the next permutation was found
  return true;
}
```

**Time and Space Complexity Analysis for Approach 4**:

* Time Complexity: O(nlogn), where n is the size of the input array.
* Space Complexity: O(1), as no additional space is required.

**Approach 5: Backtracking Approach**

**Explanation**: This backtracking approach involves recursively generating all possible permutations and finding the next greater permutation among them.

**Approach 5 Code**:

```cpp
#include <bits/stdc++.h>

using namespace std;

void nextPermutation(vector<int>& nums) {
  // If the array is empty or has only one element, return
  if (nums.empty() || nums.size() == 1) {
    return;
  }

  // Find the pivot element
  int i = nums.size() - 2;
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If there is no pivot element, then this is the last permutation
  if (i < 0) {
    reverse(nums.begin(), nums.end());
    return;
  }

  // Find the smallest number in the suffix that is greater than nums[i]
  int j = nums.size() - 1;
  while (nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Recursively find the next permutation for the sub-array nums[i+1:]
  nextPermutation(nums.begin() + i + 1, nums.end());
}
```

**Time and Space Complexity Analysis for Approach 5**:

* Time Complexity: O(n!), where n is the size of the input array.
* Space Complexity: O(n), as we need to store a copy of the input array.**Question**: next_permutation-find-next-lexicographically-greater-permutation/: Problem Statement: Given an array Arr[] of integers, rearrange the numbers of the given array into the lexicographically next greater permutation of numbers.

**Approach 1: Brute Force**
**Explanation:**
The brute force approach involves generating all possible permutations of the given array and finding the one that is lexicographically greater than the original array.

**Approach 1 Code:**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to find all permutations of a given array
vector<vector<int>> permute(vector<int>& nums) {
  vector<vector<int>> result;
  sort(nums.begin(), nums.end());

  do {
    result.push_back(nums);
  } while (next_permutation(nums.begin(), nums.end()));

  return result;
}

// Function to find the next lexicographically greater permutation
vector<int> nextPermutation(vector<int>& nums) {
  int n = nums.size();
  int i = n - 2;

  // Find the first decreasing element from the right
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If no decreasing element is found, the array is in the last permutation
  if (i < 0) {
    reverse(nums.begin(), nums.end());
    return nums;
  }

  // Find the first element from the right that is greater than nums[i]
  int j = n - 1;
  while (j >= 0 && nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Reverse the elements from i+1 to the end of the array
  reverse(nums.begin() + i + 1, nums.end());

  return nums;
}

int main() {
  vector<int> nums = {1, 2, 3};
  vector<vector<int>> permutations = permute(nums);

  for (vector<int> permutation : permutations) {
    for (int num : permutation) {
      cout << num << " ";
    }
    cout << endl;
  }

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1:**
Time complexity: O(n!), where n is the size of the input array.
Space complexity: O(n), since we need to store the permutations in a vector.

**Approach 2: Sliding Window Technique**
**Explanation:**
The sliding window technique involves maintaining a sliding window of size 2. We move the window from right to left until we find a decreasing pair. We then swap the second element of the decreasing pair with the first element that is greater than it from the right. Finally, we reverse the elements from the second element of the decreasing pair to the end of the array.

**Approach 2 Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

// Function to find the next lexicographically greater permutation
vector<int> nextPermutation(vector<int>& nums) {
  int n = nums.size();

  // Find the first decreasing element from the right
  int i = n - 2;
  while (i >= 0 && nums[i] >= nums[i + 1]) {
    i--;
  }

  // If no decreasing element is found, the array is in the last permutation
  if (i < 0) {
    reverse(nums.begin(), nums.end());
    return nums;
  }

  // Find the first element from the right that is greater than nums[i]
  int j = n - 1;
  while (j >= 0 && nums[j] <= nums[i]) {
    j--;
  }

  // Swap nums[i] and nums[j]
  swap(nums[i], nums[j]);

  // Reverse the elements from i+1 to the end of the array
  reverse(nums.begin() + i + 1, nums.end());

  return nums;
}

int main() {
  vector<int> nums = {1, 2, 3};
  vector<int> result = nextPermutation(nums);

  for (int num : result) {
    cout << num << " ";
  }
  cout << endl;

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2:**
Time complexity: O(n), where n is the size of the input array.
Space complexity: O(1), since we don't need to store any additional data structures.