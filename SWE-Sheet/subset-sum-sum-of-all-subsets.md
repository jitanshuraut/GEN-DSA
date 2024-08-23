**Question**: subset-sum-sum-of-all-subsets/: Problem Statement: Given an array print all the sum of the subset generated from it, in the increasing order.

**Approach 1: Brute Force**

**Explanation**: This approach involves generating all possible subsets of the given array and calculating their sums. The time complexity of this approach is exponential, as it is O(2^n), where n is the size of the array.

**Approach 1 Code**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void printSubsets(vector<int>& arr, int n) {
  for (int i = 0; i < (1 << n); i++) {
    int sum = 0;
    for (int j = 0; j < n; j++) {
      if (i & (1 << j)) {
        sum += arr[j];
      }
    }
    cout << sum << " ";
  }
}

int main() {
  vector<int> arr = {1, 2, 3};
  int n = arr.size();
  printSubsets(arr, n);
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:
* Time Complexity: O(2^n), where n is the size of the array.
* Space Complexity: O(1).

**Approach 2: Optimized Approach using Dynamic Programming**

**Explanation**: This approach uses dynamic programming to calculate the sum of all subsets of the given array in O(n * 2^n) time and space complexity. The idea is to create a table of size n * 2^n, where n is the size of the array and 2^n is the number of possible subsets. Each entry in the table represents the sum of the subset corresponding to that particular bitmask.

**Approach 2 Code**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void printSubsets(vector<int>& arr, int n) {
  int dp[n + 1][1 << n];
  
  // Initializing the table
  for (int i = 0; i < n + 1; i++) {
    for (int j = 0; j < (1 << n); j++) {
      dp[i][j] = 0;
    }
  }
  
  // Calculating the sum of all subsets
  for (int i = 1; i <= n; i++) {
    for (int j = 0; j < (1 << n); j++) {
      dp[i][j] = dp[i - 1][j];
      if (j & (1 << (i - 1))) {
        dp[i][j] += arr[i - 1];
      }
    }
  }
  
  // Printing the sum of all subsets
  for (int j = 0; j < (1 << n); j++) {
    cout << dp[n][j] << " ";
  }
}

int main() {
  vector<int> arr = {1, 2, 3};
  int n = arr.size();
  printSubsets(arr, n);
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:
* Time Complexity: O(n * 2^n), where n is the size of the array.
* Space Complexity: O(n * 2^n).

**Approach 3: Recursive Approach**

**Explanation**: This approach uses recursion to generate all possible subsets of the given array and calculate their sums. The time complexity of this approach is O(2^n), where n is the size of the array.

**Approach 3 Code**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void printSubsets(vector<int>& arr, int n, int sum, int index) {
  if (index == n) {
    cout << sum << " ";
    return;
  }
  
  printSubsets(arr, n, sum + arr[index], index + 1);
  printSubsets(arr, n, sum, index + 1);
}

int main() {
  vector<int> arr = {1, 2, 3};
  int n = arr.size();
  printSubsets(arr, n, 0, 0);
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 3**:
* Time Complexity: O(2^n), where n is the size of the array.
* Space Complexity: O(n).

**Approach 4: Backtracking Approach**

**Explanation**: This approach uses backtracking to generate all possible subsets of the given array and calculate their sums. The time complexity of this approach is O(2^n), where n is the size of the array.

**Approach 4 Code**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

void printSubsets(vector<int>& arr, int n, vector<int>& subset, int sum) {
  if (n == 0) {
    cout << sum << " ";
    return;
  }
  
  printSubsets(arr, n - 1, subset, sum + arr[n - 1]);
  printSubsets(arr, n - 1, subset, sum);
}

int main() {
  vector<int> arr = {1, 2, 3};
  int n = arr.size();
  vector<int> subset;
  printSubsets(arr, n, subset, 0);
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 4**:
* Time Complexity: O(2^n), where n is the size of the array.
* Space Complexity: O(n).**Question**: subset-sum-sum-of-all-subsets/: Problem Statement: Given an array print all the sum of the subset generated from it, in the increasing order.

**Approach 1: Brut Force**

**Explanation:**
This approach is straightforward Iterate through each subset and calculate their sum. Push the sum into a set to avoid duplicates. Finally, print all the distinct sums in the set.

**Approach 1 Code**:
```cpp
#include<bits/stdc++.h>
using namespace std;

// Function to print all the subset of a set
void subset(int arr[], int n)
{
	// Run a loop for all the subsets
	for (int i = 0; i < (1 << n); i++)
	{
		// Set to store the sum of the subset
		set<int> s;
	
		// Run a loop for all the elements in the set
		for (int j = 0; j < n; j++)
		{
			// Check if the jth bit is set
			if (i & (1 << j))
			{
				// If the jth bit is set, add the value of the jth element to the sum
				s.insert(arr[j]);
			}
		}
	
		// Print the sum of the subset
		for (int val : s)
			cout << val << " ";
		cout << endl;
	}
}

int main()
{
	int arr[] = {1, 2, 3};
	int n = sizeof(arr) / sizeof(arr[0]);
	subset(arr, n);
	return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:
* **Time Complexity**: O(N * 2^N), where N is the size of the array.
* **Space Complexity**: O(N * 2^N), since we are storing all the subsets.

**Approach 2: Dynamic Programming**

**Explanation**:
We can use dynamic programming to solve this problem in more efficient way. We define a dp array of size (N+1) x (sum+1), where N is the size of the array and sum is the maximum possible sum of the subset. We initialize the dp array to 0.

Now, we iterate through the array and for each element, we iterate through all the possible sums from 0 to sum. For each sum, we check if the sum is less than or equal to the current element, then we can update the dp[i][j] to max(dp[i-1][j], dp[i-1][j - arr[i]] + arr[i]).

Finally, we can print all the sums that are greater than 0.

**Approach 2 Code**:
```cpp
#include<bits/stdc++.h>
using namespace std;

// Function to print all the subset of a set
void subset(int arr[], int n)
{
	// Find the maximum possible sum of the subset
	int sum = 0;
	for (int i = 0; i < n; i++)
	{
		sum += arr[i];
	}
	
	// Create a dp array of size (N+1) x (sum+1)
	int dp[n+1][sum+1];
	
	// Initialize the dp array to 0
	memset(dp, 0, sizeof(dp));
	
	// Iterate through the array
	for (int i = 1; i <= n; i++)
	{
		// Iterate through all the possible sums from 0 to sum
		for (int j = 1; j <= sum; j++)
		{
			// If the sum is less than or equal to the current element, then we can update the dp[i][j] to max(dp[i-1][j], dp[i-1][j - arr[i]] + arr[i])
			if (j >= arr[i-1])
			{
				dp[i][j] = max(dp[i-1][j], dp[i-1][j - arr[i-1]] + arr[i-1]);
			}
			else
			{
				dp[i][j] = dp[i-1][j];
			}
		}
	}
	
	// Print all the sums that are greater than 0
	for (int j = 1; j <= sum; j++)
	{
		if (dp[n][j] > 0)
		{
			cout << dp[n][j] << " ";
		}
	}
	cout << endl;
}

int main()
{
	int arr[] = {1, 2, 3};
	int n = sizeof(arr) / sizeof(arr[0]);
	subset(arr, n);
	return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:
* **Time Complexity**: O(N * sum), where N is the size of the array and sum is the maximum possible sum of the subset.
* **Space Complexity**: O(N * sum), since we are using a dp array of size (N+1) x (sum+1).