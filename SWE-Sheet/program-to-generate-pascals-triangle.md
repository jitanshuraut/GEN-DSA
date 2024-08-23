**Question**: program-to-generate-pascals-triangle/: Problem Statement: This problem has 3 variations. They are stated below:

**Approach 1: Brute Force**

**Explanation**: A brute force approach involves calculating each element of the Pascal's triangle from scratch.

**Approach 1 Code**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
  int n;
  cout << "Enter the number of rows: ";
  cin >> n;

  // Create a 2D vector to store the Pascal's triangle
  vector<vector<int>> pascalTriangle(n);

  // Iterate over each row
  for (int i = 0; i < n; i++) {
    pascalTriangle[i].resize(i + 1);  // Resize the current row to i+1 elements

    // Iterate over each column
    for (int j = 0; j <= i; j++) {
      // If it is the first or last column, the value is 1
      if (j == 0 || j == i) {
        pascalTriangle[i][j] = 1;
      } else {
        // Otherwise, calculate the value using the values from the previous row
        pascalTriangle[i][j] = pascalTriangle[i - 1][j - 1] + pascalTriangle[i - 1][j];
      }
    }
  }

  // Display the Pascal's triangle
  cout << "Pascal's Triangle: \n";
  for (int i = 0; i < n; i++) {
    for (int j = 0; j <= i; j++) {
      cout << pascalTriangle[i][j] << " ";
    }
    cout << endl;
  }

  return 0;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(n^2), as it calculates each element of the Pascal's triangle from scratch. The space complexity is also O(n^2), as it stores all the elements of the triangle in a 2D vector.

**Approach 2: Optimized using Maps**

**Explanation**: This approach uses a map to store the calculated values of the Pascal's triangle. When a value is needed, it is checked if the map already contains it. If not, it is calculated and added to the map.

**Approach 2 Code**:

```cpp
#include <iostream>
#include <map>

using namespace std;

// Function to calculate the value of a cell in Pascal's triangle
int pascal(int row, int col) {
  if (row == col || col == 0) {  // Base cases
    return 1;
  }
  // Check if the value is already calculated
  auto it = memo.find(make_pair(row, col));
  if (it != memo.end()) {
    return it->second;  // Return the cached value
  }
  // Calculate the value and add it to the map
  int value = pascal(row - 1, col - 1) + pascal(row - 1, col);
  memo[make_pair(row, col)] = value;  // Store the value in the map
  return value;
}

int main() {
  int n;
  cout << "Enter the number of rows: ";
  cin >> n;

  // Display the Pascal's triangle
  cout << "Pascal's Triangle: \n";
  for (int i = 0; i < n; i++) {
    for (int j = 0; j <= i; j++) {
      cout << pascal(i, j) << " ";
    }
    cout << endl;
  }

  return 0;
}
```

**Time and Space Complexity Analysis**: This approach has a time complexity of O(n^2), as it checks the map for each cell in the Pascal's triangle. However, it has a space complexity of O(n), as it only stores the calculated values in the map.

**Approach 3: Optimized using Multisets**

**Explanation**: This approach uses a multiset to store the values of the previous row in the Pascal's triangle. When a value is needed, it is calculated using the values from the multiset.

**Approach 3 Code**:

```cpp
#include <iostream>
#include <set>

using namespace std;

int main() {
  int n;
  cout << "Enter the number of rows: ";
  cin >> n;

  // Create a multiset to store the values of the previous row
  multiset<int> prevRow;
  prevRow.insert(1);  // Initialize the first row

  // Display the Pascal's triangle
  cout << "Pascal's Triangle: \n";
  for (int i = 0; i < n; i++) {
    multiset<int> currentRow;  // Create a multiset for the current row
    currentRow.insert(1);  // Add the first element

    // Iterate over the previous row and calculate the values for the current row
    for (auto it = prevRow.begin(); it != prevRow.end(); it++) {
      int value = *it;
      it++;  // Move to the next element in the previous row
      if (it != prevRow.end()) {
        value += *it;  // Calculate the value for the current row
      }
      currentRow.insert(value);  // Add the value to the current row
    }

    // Display the current row
    for (auto it = currentRow.begin(); it != currentRow.end(); it++) {
      cout << *it << " ";
    }
    cout << endl;

    // Update the previous row for the next iteration
    prevRow = currentRow;
  }

  return 0;
}
```

**Time and Space Complexity Analysis**: This approach has a time complexity of O(n^2), as it calculates each value in the Pascal's triangle using the values from the previous row. The space complexity is also O(n), as it stores the values of the previous row in the multiset.

**Approach 4: Optimized using Binary Search**

**Explanation**: This approach uses binary search to find the values in the Pascal's triangle. The binary search is performed on the previous row to find the two values that are adjacent to the desired value.

**Approach 4 Code**:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
  int n;
  cout << "Enter the number of rows: ";
  cin >> n;

  // Create a vector to store the previous row
  vector<int> prevRow = {1};  // Initialize the first row

  // Display the Pascal's triangle
  cout << "Pascal's Triangle: \n";
  for (int i = 0; i < n; i++) {
    vector<int> currentRow;  // Create a vector for the current row
    currentRow.push_back(1);  // Add the first element

    // Iterate over the previous row and calculate the values for the current row
    for (int j = 0; j < prevRow.size() - 1; j++) {
      int value = prevRow[j] + prevRow[j + 1];  // Calculate the value for the current row
      currentRow.push_back(value);  // Add the value to the current row
    }

    // Add the last element to the current row
    currentRow.push_back(1);

    // Perform binary search on the previous row to find the two adjacent values
    for (int j = 0; j < currentRow.size(); j++) {
      int l = j;
      int r = prevRow.size() - 1;
      int left = -1, right = -1;
      while (l <= r) {
        int mid = (l + r) / 2;
        if (prevRow[mid] < currentRow[j]) {
          left = mid;
          l = mid + 1;
        } else if (prevRow[mid] > currentRow[j]) {
          right = mid;
          r = mid - 1;
        } else {
          left = mid;
          right = mid;
          break;
        }
      }
      cout << currentRow[j] << " ";  // Display the value
      if (left != -1 && right != -1) {  // If both adjacent values are found
        cout << "(" << prevRow[left] << ", " << prevRow[right] << ") ";  // Display the adjacent values
      }
    }
    cout << endl;

    // Update the previous row for the next iteration
    prevRow = currentRow;
  }

  return 0;
}
```

**Time and Space Complexity Analysis**: This approach has a time complexity of O(n log n), as it performs binary search on**Question:** program-to-generate-pascals-triangle/: Problem Statement: This problem has 3 variations. They are stated below:

**Approach 1: Dynamic Programming**

**Explanation:**
This approach uses dynamic programming to efficiently compute Pascal's triangle. We define a 2D array `pascal` where `pascal[i][j]` represents the value in the i-th row and j-th column of the triangle. We can populate the array using the following recurrence relation:

```
pascal[i][j] = pascal[i-1][j] + pascal[i-1][j-1]
```

where `i` is the row index and `j` is the column index. The base cases are:

```
pascal[0][0] = 1
pascal[i][0] = 1
pascal[i][i] = 1
```

This approach allows us to compute the entire Pascal's triangle in O(n^2) time and O(n^2) space.

**Approach 1 Code:**

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
  int n;
  cin >> n;

  // Initialize the Pascal's triangle array
  vector<vector<int>> pascal(n+1, vector<int>(n+1, 0));

  // Populate the array using dynamic programming
  for (int i = 0; i <= n; i++) {
    for (int j = 0; j <= i; j++) {
      if (i == 0 || j == 0 || j == i) {
        pascal[i][j] = 1;
      } else {
        pascal[i][j] = pascal[i-1][j] + pascal[i-1][j-1];
      }
    }
  }

  // Print the Pascal's triangle
  for (int i = 0; i <= n; i++) {
    for (int j = 0; j <= i; j++) {
      cout << pascal[i][j] << " ";
    }
    cout << endl;
  }

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1:**

* **Time Complexity:** O(n^2)
* **Space Complexity:** O(n^2)

**Approach 2: Mathematical Formula**

**Explanation:**
We can use the following mathematical formula to compute the value in the i-th row and j-th column of Pascal's triangle:

```
pascal[i][j] = n! / (i! * (n-i)!)
```

where `n` is the row number and `i` is the column number. This formula can be implemented as follows:

**Approach 2 Code:**

```cpp
#include <iostream>

using namespace std;

int main() {
  int n;
  cin >> n;

  // Compute the values in Pascal's triangle using the mathematical formula
  for (int i = 0; i <= n; i++) {
    for (int j = 0; j <= i; j++) {
      cout << n! / (i! * (n-i)!) << " ";
    }
    cout << endl;
  }

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2:**

* **Time Complexity:** O(n^3)
* **Space Complexity:** O(1)

**Approach 3: Recursive**

**Explanation:**
We can use recursion to generate Pascal's triangle. The recurrence relation is as follows:

```
pascal[i][j] = pascal[i-1][j] + pascal[i-1][j-1]
```

where `i` is the row index and `j` is the column index. The base cases are:

```
pascal[0][0] = 1
pascal[i][0] = 1
pascal[i][i] = 1
```

**Approach 3 Code:**

```cpp
#include <iostream>

using namespace std;

int pascal(int i, int j) {
  if (i == 0 || j == 0 || j == i) {
    return 1;
  } else {
    return pascal(i-1, j) + pascal(i-1, j-1);
  }
}

int main() {
  int n;
  cin >> n;

  // Compute the values in Pascal's triangle using recursion
  for (int i = 0; i <= n; i++) {
    for (int j = 0; j <= i; j++) {
      cout << pascal(i, j) << " ";
    }
    cout << endl;
  }

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 3:**

* **Time Complexity:** O(2^n)
* **Space Complexity:** O(n)