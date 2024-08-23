## Question

**grid-unique-paths-count-paths-from-left-top-to-the-right-bottom-of-a-matrix**: Problem Statement: Given a matrix m X n, count paths from left-top to the right bottom of a matrix with the constraints that from each cell you can either only move to the rightward direction or the downward direction.

### Approach 1: Brute Force

**Explanation**: This approach involves a simple recursive function that explores all possible paths from the top-left corner to the bottom-right corner. For each cell, it recursively calls itself for the cell below and the cell to the right. The number of paths to the current cell is the sum of the number of paths from the cell below and the number of paths from the cell to the right.

**C++ Code**:
```cpp
int countPaths(int m, int n) {
  if (m == 1 && n == 1) {
    return 1;
  }
  if (m == 0 || n == 0) {
    return 0;
  }
  return countPaths(m - 1, n) + countPaths(m, n - 1);
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: Exponential, O(2^(m+n)).
* Space Complexity: Linear, O(m+n).

### Approach 2: Dynamic Programming with Memoization

**Explanation**: This approach utilizes a memoization table to store the number of paths to each cell to avoid redundant calculations. The function checks if the number of paths for the current cell has already been calculated. If not, it recursively computes the number of paths to the cell below and the cell to the right and adds them to get the total number of paths to the current cell.

**C++ Code**:
```cpp
int countPaths(int m, int n, vector<vector<int>>& memo) {
  if (memo[m][n] != -1) {
    return memo[m][n];
  }
  if (m == 1 && n == 1) {
    return 1;
  }
  if (m == 0 || n == 0) {
    return 0;
  }
  memo[m][n] = countPaths(m - 1, n, memo) + countPaths(m, n - 1, memo);
  return memo[m][n];
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: Quadratic, O(mn).
* Space Complexity: Quadratic, O(mn).

### Approach 3: Dynamic Programming with Tabulation

**Explanation**: This approach builds the solution bottom-up by filling in the memoization table from the bottom-left corner to the top-right corner. It starts by initializing the bottom row and the rightmost column to 1 as there is only one path to reach these cells. Then, it iterates over the remaining cells in the table and calculates the number of paths to each cell based on the number of paths to the cell below and the cell to the right.

**C++ Code**:
```cpp
int countPaths(int m, int n) {
  vector<vector<int>> memo(m, vector<int>(n, 0));

  for (int i = 0; i < m; i++) {
    memo[i][0] = 1;
  }
  for (int j = 0; j < n; j++) {
    memo[0][j] = 1;
  }

  for (int i = 1; i < m; i++) {
    for (int j = 1; j < n; j++) {
      memo[i][j] = memo[i - 1][j] + memo[i][j - 1];
    }
  }

  return memo[m - 1][n - 1];
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: Quadratic, O(mn).
* Space Complexity: Quadratic, O(mn).

### Approach 4: Mathematical Approach

**Explanation**: This approach derives a mathematical formula to calculate the number of paths. The total number of paths from the top-left corner to the bottom-right corner is the number of combinations of (m-1) moves to the right and (n-1) moves to the bottom. This can be calculated using the binomial coefficient formula: C(m+n-2, m-1).

**C++ Code**:
```cpp
int countPaths(int m, int n) {
  long long result = 1;
  for (int i = 1; i <= m - 1; i++) {
    result *= (m + n - i) / i;
  }
  return result;
}
```

**Time and Space Complexity Analysis**:
* Time Complexity: Linear, O(mn).
* Space Complexity: Constant, O(1).**Question:** grid-unique-paths-count-paths-from-left-top-to-the-right-bottom-of-a-matrix/: Problem Statement: Given a matrix m X n, count paths from left-top to the right bottom of a matrix with the constraints that from each cell you can either only move to the rightward direction or the downward direction.

**Approach 1: Dynamic Programming**

**Explanation:**
In this approach, we use dynamic programming to store the number of paths from (0, 0) to (i, j) in a 2D array. We initialize the first row and first column to 1 (since there is only one path from (0, 0) to (i, 0) and (0, j) to (0, j)). For each cell (i, j), we calculate the number of paths as the sum of paths from (i-1, j) (moving down) and (i, j-1) (moving right).

**C++ Code:**
```cpp
int uniquePaths(int m, int n) {
  int dp[m][n];
  
  // Initialize first row and column to 1
  for (int i = 0; i < m; ++i) dp[i][0] = 1;
  for (int j = 0; j < n; ++j) dp[0][j] = 1;
  
  // Calculate the number of paths for each cell
  for (int i = 1; i < m; ++i) {
    for (int j = 1; j < n; ++j) {
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    }
  }
  
  return dp[m - 1][n - 1];
}
```

**Time and Space Complexity Analysis:**

Time Complexity: O(m * n), where m and n are the number of rows and columns in the matrix.
Space Complexity: O(m * n), since we use a 2D array to store the number of paths.

**Approach 2: Combinatorics**

**Explanation:**
This approach uses combinatorics to calculate the number of paths. We can treat the movement as choosing "downward" moves from a total of (m + n - 2) moves (m-1 downward moves and n-1 rightward moves). Therefore, the number of paths is given by the formula:

```
C(m + n - 2, m - 1)
```

where C(n, k) represents the binomial coefficient (n choose k).

**C++ Code:**
```cpp
int uniquePaths(int m, int n) {
  // Calculate the binomial coefficient
  long long paths = 1;
  for (int i = 1; i <= m - 1; ++i) {
    paths *= (m + n - i) / i;
  }
  
  return paths;
}
```

**Time and Space Complexity Analysis:**

Time Complexity: O(m + n), since we perform a linear number of operations to calculate the binomial coefficient.
Space Complexity: O(1), since we do not use any additional data structures.