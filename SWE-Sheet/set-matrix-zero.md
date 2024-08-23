## Question: set-matrix-zero/: Problem Statement: Given a matrix if an element in the matrix is 0 then you will have to set its entire column and row to 0 and then return the matrix.

## Approach 1: Brute Force

This approach is based on iterating over the complete matrix two times. In the first iteration, we can use a set to store the rows and columns that need to be set to 0. In the second iteration, we can update the values of the matrix accordingly.

### Approach 1 Code:

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    
    set<int> rows, cols;
    
    // Store the rows and columns with 0s in 'rows' and 'cols' sets
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0) {
                rows.insert(i);
                cols.insert(j);
            }
        }
    }
    
    // Set the rows to 0
    for (int row : rows) {
        for (int j = 0; j < n; j++) {
            matrix[row][j] = 0;
        }
    }
    
    // Set the columns to 0
    for (int col : cols) {
        for (int i = 0; i < m; i++) {
            matrix[i][col] = 0;
        }
    }
}
```

### Time and Space Complexity Analysis for Approach 1:

* Time Complexity: O(m * n)
* Space Complexity: O(m + n)

## Approach 2: Using Extra Space

This approach is based on using extra space to store the rows and columns that need to be set to 0. We will use two arrays, one to store the rows and the other to store the columns.

### Approach 2 Code:

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    
    bool row[m], col[n];
    memset(row, false, sizeof(row));
    memset(col, false, sizeof(col));
    
    // Store the rows and columns with 0s in 'rows' and 'cols' arrays
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0) {
                row[i] = true;
                col[j] = true;
            }
        }
    }
    
    // Set the rows to 0
    for (int i = 0; i < m; i++) {
        if (row[i]) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = 0;
            }
        }
    }
    
    // Set the columns to 0
    for (int j = 0; j < n; j++) {
        if (col[j]) {
            for (int i = 0; i < m; i++) {
                matrix[i][j] = 0;
            }
        }
    }
}
```

### Time and Space Complexity Analysis for Approach 2:

* Time Complexity: O(m * n)
* Space Complexity: O(m + n)

## Approach 3: Using the First Row and Column as Flags

This approach is based on using the first row and column of the matrix as flags to keep track of the rows and columns that need to be set to 0. We will use the first row to store the information about the rows and the first column to store the information about the columns.

### Approach 3 Code:

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix[0].size();
    
    bool firstRowZero = false, firstColZero = false;
    
    // Check if the first row and column have 0s
    for (int i = 0; i < m; i++) {
        if (matrix[i][0] == 0) {
            firstColZero = true;
            break;
        }
    }
    for (int j = 0; j < n; j++) {
        if (matrix[0][j] == 0) {
            firstRowZero = true;
            break;
        }
    }
    
    // Use the first row and column as flags to mark rows and columns with 0s
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }
    
    // Set the rows and columns to 0 based on the flags in the first row and column
    for (int i = 1; i < m; i++) {
        if (matrix[i][0] == 0) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = 0;
            }
        }
    }
    for (int j = 1; j < n; j++) {
        if (matrix[0][j] == 0) {
            for (int i = 0; i < m; i++) {
                matrix[i][j] = 0;
            }
        }
    }
    
    // Set the first row and column to 0 if necessary
    if (firstRowZero) {
        for (int j = 0; j < n; j++) {
            matrix[0][j] = 0;
        }
    }
    if (firstColZero) {
        for (int i = 0; i < m; i++) {
            matrix[i][0] = 0;
        }
    }
}
```

### Time and Space Complexity Analysis for Approach 3:

* Time Complexity: O(m * n)
* Space Complexity: O(1)## Question
"set-matrix-zero/: Problem Statement: Given a matrix if an element in the matrix is 0 then you will have to set its entire column and row to 0 and then return the matrix."

## Approach 1: Brute Force
**Explanation:**
This approach is the simplest one where we traverse through each element of the matrix. For each element, we check if it is 0. If it is 0, we iterate through the entire row and column and set all the elements to 0.

**Approach 1 Code:**
```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int n = matrix.size();
    int m = matrix[0].size();
    
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(matrix[i][j]==0){
                for(int k=0;k<m;k++){
                    matrix[i][k]=0;
                }
                for(int k=0;k<n;k++){
                    matrix[k][j]=0;
                }
            }
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 1:**
The time complexity of this approach is O(n^2 * m), where n is the number of rows and m is the number of columns in the matrix. The space complexity is O(1).

## Approach 2: Using Two Arrays
**Explanation:**
This approach is similar to the brute force approach, but it uses two arrays to keep track of which rows and columns need to be set to 0. We first iterate through the matrix and for each element, we check if it is 0. If it is 0, we set the corresponding element in the two arrays to 1. Then, we iterate through the two arrays and set all the elements in the corresponding rows and columns to 0.

**Approach 2 Code:**
```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int n = matrix.size();
    int m = matrix[0].size();
    vector<int> row(n,0);
    vector<int> col(m,0);
    
    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            if(matrix[i][j]==0){
                row[i]=1;
                col[j]=1;
            }
        }
    }
    
    for(int i=0;i<n;i++){
        if(row[i]==1){
            for(int j=0;j<m;j++){
                matrix[i][j]=0;
            }
        }
    }
    for(int j=0;j<m;j++){
        if(col[j]==1){
            for(int i=0;i<n;i++){
                matrix[i][j]=0;
            }
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 2:**
The time complexity of this approach is O(n^2), where n is the number of rows and m is the number of columns in the matrix. The space complexity is O(n + m).

## Approach 3: Using a Constant Space
**Explanation:**
This approach uses a constant space to solve the problem. We use the first row and first column of the matrix to keep track of which rows and columns need to be set to 0. We first iterate through the matrix and for each element, we check if it is 0. If it is 0, we set the corresponding element in the first row and first column to 1. Then, we iterate through the first row and first column and set all the elements in the corresponding rows and columns to 0.

**Approach 3 Code:**
```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int n = matrix.size();
    int m = matrix[0].size();
    
    bool firstRowZero = false;
    bool firstColZero = false;
    
    for(int i=0;i<n;i++){
        if(matrix[i][0]==0){
            firstColZero = true;
        }
    }
    for(int j=0;j<m;j++){
        if(matrix[0][j]==0){
            firstRowZero = true;
        }
    }
    
    for(int i=1;i<n;i++){
        for(int j=1;j<m;j++){
            if(matrix[i][j]==0){
                matrix[i][0]=0;
                matrix[0][j]=0;
            }
        }
    }
    
    for(int i=1;i<n;i++){
        if(matrix[i][0]==0){
            for(int j=0;j<m;j++){
                matrix[i][j]=0;
            }
        }
    }
    for(int j=1;j<m;j++){
        if(matrix[0][j]==0){
            for(int i=0;i<n;i++){
                matrix[i][j]=0;
            }
        }
    }
    
    if(firstRowZero){
        for(int j=0;j<m;j++){
            matrix[0][j]=0;
        }
    }
    if(firstColZero){
        for(int i=0;i<n;i++){
            matrix[i][0]=0;
        }
    }
}
```

**Time and Space Complexity Analysis for Approach 3:**
The time complexity of this approach is O(n^2), where n is the number of rows and m is the number of columns in the matrix. The space complexity is O(1).