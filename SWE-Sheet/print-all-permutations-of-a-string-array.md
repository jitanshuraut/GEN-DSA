**Question**: "print-all-permutations-of-a-string-array/: Problem Statement: Given an array arr of distinct integers, print all permutations of String/Array."

**Approach 1: Brute Force**

**Explanation**: This approach uses the brute force method to generate all possible permutations of the given array. It starts by fixing the first element of the array as the first element of each permutation and then generating all possible permutations of the remaining elements. The time complexity for this approach is O(n!), where n is the number of elements in the array.

**Approach 1 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to print all permutations of an array
void permute(int arr[], int n) {
    // Base case
    if (n == 0) {
        for (int i = 0; i < n; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
        return;
    }

    // Fix the first element of the array as the first element of each permutation
    for (int i = 0; i < n; i++) {
        // Swap the first element with the current element
        swap(arr[0], arr[i]);

        // Generate all permutations of the remaining elements
        permute(arr + 1, n - 1);

        // Swap the first element back to its original position
        swap(arr[0], arr[i]);
    }
}

int main() {
    int arr[] = {1, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    permute(arr, n);
    return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:

The time complexity for this approach is O(n!), where n is the number of elements in the array. This is because there are n choices for the first element of each permutation, and then n-1 choices for the second element, and so on. The total number of permutations is therefore n!. The space complexity for this approach is O(n), as it uses a stack of n elements to store the current permutation.

**Approach 2: Optimized Approaches using Maps, Multisets, Binary Search, Two Pointers**

**Explanation**: This approach uses a combination of maps, multisets, binary search, and two pointers to optimize the brute force approach. The map is used to store the frequency of each element in the array, the multiset is used to store the elements in sorted order, and the binary search and two pointers are used to find the next element in the permutation. The time complexity for this approach is O(n^2 log n), which is a significant improvement over the brute force approach.

**Approach 2 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to print all permutations of an array
void permute(int arr[], int n) {
    // Create a map to store the frequency of each element
    unordered_map<int, int> freq;
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Create a multiset to store the elements in sorted order
    multiset<int> elements;
    for (auto it : freq) {
        elements.insert(it.first);
    }

    // Create two pointers to track the current permutation
    auto it1 = elements.begin();
    auto it2 = elements.begin();

    // While the second pointer is not at the end of the multiset
    while (it2 != elements.end()) {
        // Print the current permutation
        for (int i = 0; i < n; i++) {
            cout << *it1 << " ";
            it1++;
        }
        cout << endl;

        // Find the next element in the permutation
        int next_element = *it2;
        it2++;
        freq[next_element]--;
        if (freq[next_element] == 0) {
            elements.erase(next_element);
        }
        it1 = elements.lower_bound(next_element);
    }
}

int main() {
    int arr[] = {1, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    permute(arr, n);
    return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:

The time complexity for this approach is O(n^2 log n), where n is the number of elements in the array. This is because it takes O(n) time to create the map and multiset, and O(n log n) time to find the next element in the permutation for each of the n permutations. The space complexity for this approach is O(n), as it uses a map, multiset, and two pointers to store the current permutation.

**Approach 3: Greedy Algorithms**

**Explanation**: This approach uses a greedy algorithm to generate all permutations of the given array. The greedy algorithm starts with the first element of the array and selects the smallest element from the remaining elements to be the next element in the permutation. This process is repeated until all elements have been selected. The time complexity for this approach is O(n^2), which is a significant improvement over the brute force approach.

**Approach 3 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to print all permutations of an array
void permute(int arr[], int n) {
    // Sort the array in ascending order
    sort(arr, arr + n);

    // Create a stack to store the current permutation
    stack<int> stack;

    // While the stack is not empty
    while (!stack.empty()) {
        // Pop the top element from the stack
        int top = stack.top();
        stack.pop();

        // Print the current permutation
        for (int i = 0; i < n; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;

        // Find the next element in the permutation
        int next_element = -1;
        for (int i = top + 1; i < n; i++) {
            if (arr[i] > arr[top]) {
                next_element = i;
                break;
            }
        }

        // If a next element is found, push it onto the stack
        if (next_element != -1) {
            stack.push(next_element);

            // Swap the next element with the top element
            swap(arr[top], arr[next_element]);
        }
    }
}

int main() {
    int arr[] = {1, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    permute(arr, n);
    return 0;
}
```

**Time and Space Complexity Analysis for Approach 3**:

The time complexity for this approach is O(n^2), where n is the number of elements in the array. This is because it takes O(n log n) time to sort the array and O(n^2) time to find the next element in the permutation for each of the n permutations. The space complexity for this approach is O(n), as it uses a stack to store the current permutation.

**Approach 4: Recursive**

**Explanation**: This approach uses recursion to generate all permutations of the given array. The recursive function starts with the first element of the array and generates all permutations of the remaining elements. The base case for the recursion is when there are no more elements in the array, in which case the current permutation is printed. The time complexity for this approach is O(n!), which is the same as the brute force approach.

**Approach 4 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

// Function to print all permutations of an array
void permute(int arr[], int n) {
    // Base case
    if (n == 0) {
        for (int i = 0; i < n; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
        return;
    }

    // For each element in the array
    for (int i = 0; i < n; i++) {
        // Swap the current element with the first element
        swap(arr[i], arr[0]);

        // Recursively generate all permutations of the remaining elements
        permute(arr + 1, n - 1);

        // Swap the current element back to its original position
        swap(arr[i], arr[0]);
    }
}

int main() {
    int arr[] = {1, 2, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    permute(arr, n);
    return 0;
}
```

**Time and Space Complexity Analysis for Approach 4**:

The time complexity for this approach is O(n!), where n is the## Question
print-all-permutations-of-a-string-array/: Problem Statement: Given an array arr of distinct integers, print all permutations of String/Array.

## Approach 1: Backtracking
The backtracking approach involves systematically exploring all possible combinations of elements in the array.
```cpp
#include <iostream>
#include <vector>

using namespace std;

void permute(vector<int> &arr, int l, int r) {
  if (l == r) {
    for (int i = 0; i <= r; i++) {
      cout << arr[i];
    }
    cout << endl;
  } else {
    for (int i = l; i <= r; i++) {
      swap(arr[l], arr[i]);
      permute(arr, l + 1, r);
      swap(arr[l], arr[i]);
    }
  }
}

int main() {
  vector<int> arr = {1, 2, 3};
  int n = arr.size();
  permute(arr, 0, n - 1);
  return 0;
}
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(n!) where n is the length of the array.
- Space Complexity: O(n) for the recursive stack space.

## Approach 2: Lexicographic Permutations
This approach uses the next_permutation function from the <algorithm> library to generate lexicographically sorted permutations of the array.
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
  vector<int> arr = {1, 2, 3};
  sort(arr.begin(), arr.end());

  do {
    for (int i : arr) {
      cout << i;
    }
    cout << endl;
  } while (next_permutation(arr.begin(), arr.end()));

  return 0;
}
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(n! * n) where n is the length of the array. This is because the next_permutation function takes O(n) time to generate each permutation, and there are a total of n! permutations.
- Space Complexity: O(1) as no extra space is required.