**Question**: rotate-image-by-90-degree/: Problem Statement: Given a matrix, your task is to rotate the matrix 90 degrees clockwise.

**Approach 1: Brute Force**

**Explanation:**
In this approach, we rotate the matrix one element at a time. We start by considering the top-left element and move it to the bottom-right corner. Then, we move the element from the top-right corner to the top-left corner, and so on. We continue this process until all the elements have been moved.

**Approach 1 Code:**
```cpp
void rotateMatrix(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < n / 2; i++) {
        for (int j = i; j < n - 1 - i; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[n - 1 - j][i];
            matrix[n - 1 - j][i] = matrix[n - 1 - i][n - 1 - j];
            matrix[n - 1 - i][n - 1 - j] = matrix[j][n - 1 - i];
            matrix[j][n - 1 - i] = temp;
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 1:**
* **Time Complexity:** O(n^2)
* **Space Complexity:** O(1)

**Approach 2: Optimal Approach using Transpose and Reverse**

**Explanation:**
This approach is more efficient than the brute force approach. We first transpose the matrix, which means we swap the rows and columns. Then, we reverse each row of the transposed matrix. This effectively rotates the matrix 90 degrees clockwise.

**Approach 2 Code:**
```cpp
void rotateMatrix(int[][] matrix) {
    int n = matrix.length;
    // Transpose the matrix
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
    // Reverse each row of the transposed matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n / 2; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[i][n - 1 - j];
            matrix[i][n - 1 - j] = temp;
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 2:**
* **Time Complexity:** O(n^2)
* **Space Complexity:** O(1)

**Approach 3: Using Cyclic Replacements**

**Explanation:**
This approach is also known as the "in-place" rotation algorithm. We start by considering the top-left element of the matrix. We then move this element to the top-right corner, and the element from the top-right corner to the bottom-right corner, and so on. We continue this process until the element reaches its original position. We then repeat this process for the next element in the top row, and so on.

**Approach 3 Code:**
```cpp
void rotateMatrix(int[][] matrix) {
    int n = matrix.length;
    for (int i = 0; i < n / 2; i++) {
        for (int j = i; j < n - 1 - i; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[n - 1 - j][i];
            matrix[n - 1 - j][i] = matrix[n - 1 - i][n - 1 - j];
            matrix[n - 1 - i][n - 1 - j] = matrix[j][n - 1 - i];
            matrix[j][n - 1 - i] = temp;
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 3:**
* **Time Complexity:** O(n^2)
* **Space Complexity:** O(1)**Question**: rotate-image-by-90-degree/: Problem Statement: Given a matrix, your task is to rotate the matrix 90 degrees clockwise.

**Approach 1**: Transpose and Reverse

**Explanation**: This approach involves two steps:
1. Transposing the matrix: Swapping the elements of the matrix along the diagonal.
2. Reversing each row of the transposed matrix.

**Approach 1 Code**:

```cpp
void rotate(vector<vector<int>>& matrix) {
    // Transpose the matrix
    for (int i = 0; i < matrix.size(); i++) {
        for (int j = i; j < matrix[0].size(); j++) {
            swap(matrix[i][j], matrix[j][i]);
        }
    }
    
    // Reverse each row
    for (int i = 0; i < matrix.size(); i++) {
        reverse(matrix[i].begin(), matrix[i].end());
    }
}
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(n^2), where n is the size of the matrix.
- Space Complexity: O(1), as the operation is performed in place without using any additional data structures.

**Approach 2**: Cyclic Rotation

**Explanation**: This approach uses cyclic rotation to move elements in a circular manner, effectively rotating the matrix by 90 degrees. It starts from the top-left corner and moves elements in a clockwise direction until all elements have been rotated.

**Approach 2 Code**:

```cpp
void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size();
    
    for (int layer = 0; layer < n / 2; layer++) {
        for (int i = layer; i < n - layer - 1; i++) {
            int temp = matrix[layer][i];
            
            matrix[layer][i] = matrix[n - i - 1][layer];
            matrix[n - i - 1][layer] = matrix[n - layer - 1][n - i - 1];
            matrix[n - layer - 1][n - i - 1] = matrix[i][n - layer - 1];
            matrix[i][n - layer - 1] = temp;
        }
    }
}
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(n^2), where n is the size of the matrix.
- Space Complexity: O(1), as the operation is performed in place without using any additional data structures.