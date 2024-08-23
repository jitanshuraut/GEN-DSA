**Question**: "length-of-the-longest-subarray-with-zero-sum/: Problem Statement: Given an array containing both positive and negative integers, we have to find the length of the longest subarray with the sum of all elements equal to zero."

**Approach 1: Brute Force**

**Explanation:**
In the brute force approach, we consider every subarray of the given array and check if the sum of elements equals zero. The time complexity of this approach is O(N^2), where N is the length of the array.

**Approach 1 Code:**

```cpp
int findLongestSubarrayWithZeroSum(int arr[], int n) {
    int maxLen = 0;
    for (int i = 0; i < n; i++) {
        int sum = 0;
        for (int j = i; j < n; j++) {
            sum += arr[j];
            if (sum == 0) {
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }
    return maxLen;
}
```

**Time and Space Complexity Analysis for Approach 1:**

* Time Complexity: O(N^2)
* Space Complexity: O(1)

**Approach 2: Optimized approach using Maps**

**Explanation:**
In this approach, we store the prefix sum of the array and the index where the prefix sum occurs for the first time in a map. If we encounter a prefix sum that has already occurred, we calculate the difference between the current index and the index stored in the map. This difference gives us the length of the subarray with zero sum. The time complexity of this approach is O(N), where N is the length of the array.

**Approach 2 Code:**

```cpp
int findLongestSubarrayWithZeroSum(int arr[], int n) {
    int maxLen = 0;
    unordered_map<int, int> prefixSumIdx;
    int prefixSum = 0;
    for (int i = 0; i < n; i++) {
        prefixSum += arr[i];
        if (prefixSum == 0) {
            maxLen = max(maxLen, i + 1);
        } else if (prefixSumIdx.find(prefixSum) != prefixSumIdx.end()) {
            maxLen = max(maxLen, i - prefixSumIdx[prefixSum]);
        } else {
            prefixSumIdx[prefixSum] = i;
        }
    }
    return maxLen;
}
```

**Time and Space Complexity Analysis for Approach 2:**

* Time Complexity: O(N)
* Space Complexity: O(N)

**Approach 3: Optimized approach using Two Pointers**

**Explanation:**
In this approach, we maintain two pointers, one at the start of the subarray and one at the end of the subarray. We move the right pointer forward and if the sum of the subarray becomes greater than zero, we move the left pointer forward to adjust the sum. This process is repeated until the sum of the subarray becomes zero. The maximum length of the subarray is then updated. The time complexity of this approach is O(N), where N is the length of the array.

**Approach 3 Code:**

```cpp
int findLongestSubarrayWithZeroSum(int arr[], int n) {
    int maxLen = 0;
    int left = 0, right = 0;
    int sum = 0;
    while (right < n) {
        sum += arr[right];
        while (sum > 0) {
            sum -= arr[left];
            left++;
        }
        maxLen = max(maxLen, right - left + 1);
        right++;
    }
    return maxLen;
}
```

**Time and Space Complexity Analysis for Approach 3:**

* Time Complexity: O(N)
* Space Complexity: O(1)## Question

**Problem Statement:** Given an array containing both positive and negative integers, we have to find the length of the longest subarray with the sum of all elements equal to zero.

## Approach 1: Brute Force

**Explanation:** This intuitive approach involves iterating through all possible subarrays of the given array and checking if their sum is equal to zero. The length of the longest such subarray is then tracked.

**Approach 1 Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int longestSubarrayWithZeroSum(vector<int>& arr) {
    int maxLength = 0;
    for (int start = 0; start < arr.size(); start++) {
        int sum = 0;
        for (int end = start; end < arr.size(); end++) {
            sum += arr[end];
            if (sum == 0) {
                maxLength = max(maxLength, end - start + 1);
            }
        }
    }
    return maxLength;
}
```

**Time and Space Complexity Analysis:**

* **Time Complexity:** O(n^3), where n is the length of the input array. For each possible starting index, the algorithm considers all possible ending indices, leading to a cubic time complexity.
* **Space Complexity:** O(1), as the algorithm only uses a few variables for tracking the current sum and maximum length.

## Approach 2: Prefix Sum with HashMap

**Explanation:** This approach leverages the concept of prefix sum, where the prefix sum at index i represents the sum of the elements in the subarray from 0 to i. The key idea is to store these prefix sums in a hash map, along with their corresponding indices. We then iterate through the prefix sums and check if the current prefix sum minus a previous prefix sum equals zero. If so, the length of the corresponding subarray is calculated and updated as the maximum length if it is larger than the previous maximum.

**Approach 2 Code:**

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int longestSubarrayWithZeroSum(vector<int>& arr) {
    int maxLength = 0;
    unordered_map<int, int> prefixSumIndices;
    int prefixSum = 0;
    for (int i = 0; i < arr.size(); i++) {
        prefixSum += arr[i];
        if (prefixSum == 0) {
            maxLength = i + 1;
        } else if (prefixSumIndices.find(prefixSum) != prefixSumIndices.end()) {
            maxLength = max(maxLength, i - prefixSumIndices[prefixSum]);
        } else {
            prefixSumIndices[prefixSum] = i;
        }
    }
    return maxLength;
}
```

**Time and Space Complexity Analysis:**

* **Time Complexity:** O(n), where n is the length of the input array. The algorithm iterates through the array once, calculating and updating prefix sums and checking for subarray sums equal to zero.
* **Space Complexity:** O(n), as the hash map can store up to n key-value pairs for each unique prefix sum.

## Approach 3: Sliding Window

**Explanation:** This approach uses a sliding window to maintain a subarray with a sum equal to zero. The window expands and contracts as the algorithm iterates through the input array. If the sum of the current window is zero, the length of the window is tracked as the maximum length.

**Approach 3 Code:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

int longestSubarrayWithZeroSum(vector<int>& arr) {
    int maxLength = 0;
    int windowSum = 0;
    int windowStart = 0;
    for (int windowEnd = 0; windowEnd < arr.size(); windowEnd++) {
        windowSum += arr[windowEnd];
        while (windowSum != 0) {
            windowSum -= arr[windowStart];
            windowStart++;
        }
        maxLength = max(maxLength, windowEnd - windowStart + 1);
    }
    return maxLength;
}
```

**Time and Space Complexity Analysis:**

* **Time Complexity:** O(n), where n is the length of the input array. The algorithm iterates through the array only once, adjusting the sliding window as needed.
* **Space Complexity:** O(1), as only a few variables are used for tracking the window sum, window start and end indices, and maximum length.