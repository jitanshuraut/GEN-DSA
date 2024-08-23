**Question:** kadanes-algorithm-maximum-subarray-sum-in-an-array/: Problem Statement: Given an integer array arr, find the contiguous subarray (containing at least one number) which has the largest sum and returns its sum and prints the subarray.

**Approach 1: Brute Force**

**Explanation:**
The brute force approach involves checking all possible subarrays and finding the one with the maximum sum.

**Approach 1 Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
  vector<int> arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };
  int max_sum = INT_MIN;
  int start = 0, end = 0;

  for (int i = 0; i < arr.size(); i++) {
    int sum = 0;
    for (int j = i; j < arr.size(); j++) {
      sum += arr[j];
      if (sum > max_sum) {
        max_sum = sum;
        start = i;
        end = j;
      }
    }
  }

  cout << "Maximum subarray sum: " << max_sum << endl;
  cout << "Subarray: ";
  for (int i = start; i <= end; i++) {
    cout << arr[i] << " ";
  }
  cout << endl;

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1:**
* **Time Complexity:** O(N^2), where N is the size of the input array. This is because it checks all possible subarrays, resulting in a nested loop.
* **Space Complexity:** O(1), as no additional space is required beyond the input array.

**Approach 2: Kadane's Algorithm**

**Explanation:**
Kadane's algorithm greedily builds the maximum subarray sum by iterating through the input array and keeping track of the current maximum subarray sum and the maximum overall subarray sum.

**Approach 2 Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
  vector<int> arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };
  int max_so_far = 0, max_ending_here = 0, start = 0, end = 0, s = 0;

  for (int i = 0; i < arr.size(); i++) {
    max_ending_here += arr[i];
    if (max_so_far < max_ending_here) {
      max_so_far = max_ending_here;
      start = s;
      end = i;
    }
    if (max_ending_here < 0) {
      max_ending_here = 0;
      s = i + 1;
    }
  }

  cout << "Maximum subarray sum: " << max_so_far << endl;
  cout << "Subarray: ";
  for (int i = start; i <= end; i++) {
    cout << arr[i] << " ";
  }
  cout << endl;

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2:**
* **Time Complexity:** O(N), where N is the size of the input array. This is because it traverses the input array only once.
* **Space Complexity:** O(1), as no additional space is required beyond the input array.**Question**: Given an integer array arr, find the contiguous subarray (containing at least one number) which has the largest sum and returns its sum and prints the subarray.

**Approach 1: Brute Force**

**Explanation**: This approach involves exhaustively checking all possible subarrays of the given array and calculating their sums. The subarray with the largest sum is then returned.

**Approach 1 Code**:

```cpp
#include <iostream>
#include <climits>
using namespace std;

int maxSubarraySumBruteForce(int arr[], int n) {
  int maxSum = INT_MIN;
  for (int i = 0; i < n; i++) {
    int sum = 0;
    for (int j = i; j < n; j++) {
      sum += arr[j];
      maxSum = max(maxSum, sum);
    }
  }
  return maxSum;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(n^2), where n is the length of the array. This is because for each element in the array, the sum of all subsequent elements needs to be calculated.
* **Space Complexity**: O(1), as no additional data structures are used.

**Approach 2: Kadane's Algorithm (Sliding Window Technique)**

**Explanation**: Kadane's algorithm is a greedy algorithm that maintains a running sum of elements in a sliding window. The running sum is updated at each step by adding the current element to the previous sum. If the running sum becomes negative, it is reset to zero. The maximum running sum encountered so far is returned as the maximum subarray sum.

**Approach 2 Code**:

```cpp
#include <iostream>
#include <climits>
using namespace std;

int maxSubarraySumKadanes(int arr[], int n) {
  int maxSum = INT_MIN;
  int runningSum = 0;
  for (int i = 0; i < n; i++) {
    runningSum += arr[i];
    maxSum = max(maxSum, runningSum);
    if (runningSum < 0) {
      runningSum = 0;
    }
  }
  return maxSum;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(n), as the algorithm iterates over the array once.
* **Space Complexity**: O(1), as no additional data structures are used.

**Approach 3: Divide and Conquer (Mathematical Techniques)**

**Explanation**: This approach divides the array into two halves repeatedly and finds the maximum subarray sum in each half. It then compares the maximum subarray sums of the left and right halves with the maximum subarray sum that crosses the midpoint of the array. The subarray with the largest sum is returned.

**Approach 3 Code**:

```cpp
#include <iostream>
#include <climits>
using namespace std;

int maxCrossingSum(int arr[], int low, int mid, int high) {
  int sum = 0;
  int leftSum = INT_MIN;
  for (int i = mid; i >= low; i--) {
    sum += arr[i];
    leftSum = max(leftSum, sum);
  }
  sum = 0;
  int rightSum = INT_MIN;
  for (int i = mid + 1; i <= high; i++) {
    sum += arr[i];
    rightSum = max(rightSum, sum);
  }
  return leftSum + rightSum;
}

int maxSubarraySumDivideAndConquer(int arr[], int low, int high) {
  if (low == high) {
    return arr[low];
  }
  int mid = (low + high) / 2;
  int leftSum = maxSubarraySumDivideAndConquer(arr, low, mid);
  int rightSum = maxSubarraySumDivideAndConquer(arr, mid + 1, high);
  int crossSum = maxCrossingSum(arr, low, mid, high);
  return max({leftSum, rightSum, crossSum});
}
```

**Time and Space Complexity Analysis for Approach 3**:

* **Time Complexity**: O(n log n), where n is the length of the array. This is because the array is divided into halves recursively.
* **Space Complexity**: O(log n), as the recursion stack can grow up to log n levels deep.

**Approach 4: Sweep Line Technique**

**Explanation**: This approach uses a sweep line to iterate over the array and maintain a running sum of elements inside a window. The window is expanded until the running sum becomes negative, at which point it is reset to zero. The maximum running sum encountered so far is returned as the maximum subarray sum.

**Approach 4 Code**:

```cpp
#include <iostream>
#include <climits>
using namespace std;

int maxSubarraySumSweepLine(int arr[], int n) {
  int maxSum = INT_MIN;
  int runningSum = 0;
  int left = 0;
  for (int right = 0; right < n; right++) {
    runningSum += arr[right];
    while (runningSum < 0) {
      runningSum -= arr[left];
      left++;
    }
    maxSum = max(maxSum, runningSum);
  }
  return maxSum;
}
```

**Time and Space Complexity Analysis for Approach 4**:

* **Time Complexity**: O(n), as the algorithm iterates over the array once.
* **Space Complexity**: O(1), as no additional data structures are used.

**Approach 5: Graph Algorithms**

**Explanation**: This approach represents the array as a directed graph, where nodes represent elements of the array and edges represent possible transitions between elements. The maximum subarray sum is then found by finding the longest path in the graph. This can be done using algorithms such as Dijkstra's or Bellman-Ford.

**Approach 5 Code**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Edge {
  int from;
  int to;
  int weight;
};

int maxSubarraySumGraph(int arr[], int n) {
  vector<vector<Edge>> graph(n);
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      graph[i].push_back({i, j, arr[j] - arr[i]});
    }
  }
  vector<int> distance(n, INT_MIN);
  distance[0] = 0;
  for (int i = 0; i < n - 1; i++) {
    for (Edge e : graph[i]) {
      distance[e.to] = max(distance[e.to], distance[e.from] + e.weight);
    }
  }
  return *max_element(distance.begin(), distance.end());
}
```

**Time and Space Complexity Analysis for Approach 5**:

* **Time Complexity**: O(n^2), as the graph has n nodes and n^2 edges, and the longest path algorithm takes O(n^2) time.
* **Space Complexity**: O(n^2), as the graph and distance arrays both have size n^2.

**Approach 6: Dynamic Programming**

**Explanation**: This approach uses dynamic programming to solve the problem. It creates a table dp such that dp[i] stores the maximum subarray sum ending at index i. The table is filled in a bottom-up manner, where the maximum subarray sum at each index is calculated based on the maximum subarray sum at the previous index. The maximum value in the dp table is returned as the maximum subarray sum.

**Approach 6 Code**:

```cpp
#include <iostream>
#include <climits>
using namespace std;

int maxSubarraySumDynamicProgramming(int arr[], int n) {
  int dp[n];
  dp[0] = arr[0];
  for (int i = 1; i < n; i++) {
    dp[i] = max(arr[i], dp[i - 1] + arr[i]);
  }
  return *max_element(dp, dp + n);
}
```

**Time and Space Complexity Analysis for Approach 6**:

* **Time Complexity**: O(n), as the table is filled in a single pass over the array.
* **Space Complexity**: O(n), as the table dp stores n values.

**Approach 7: Trie Data Structure**

**Explanation**: This approach uses a trie data structure to store the sums of all possible subarrays. The trie is constructed by inserting all possible subarray sums into it. The maximum subarray sum is then found by traversing the trie and finding the node with the largest sum.

**Approach 7 Code**:

```cpp
#include <iostream>
#include <vector>
