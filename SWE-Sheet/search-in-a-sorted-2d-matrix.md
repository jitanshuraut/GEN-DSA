**Question**: Search in a Sorted 2D Matrix

**Problem Statement**: Given a 2D matrix with elements in non-decreasing order in each row and every first element of a row is greater than the last element in the previous row, we are required to find if a given integer target exists in the matrix.

**Approach 1: Brute Force**

* **Explanation**: This approach involves iterating over each element of the matrix and checking if it equals the target.

* **C++ Code**:
```cpp
bool findTarget(vector<vector<int>>& matrix, int target) {
  for (int i = 0; i < matrix.size(); i++) {
    for (int j = 0; j < matrix[0].size(); j++) {
      if (matrix[i][j] == target) {
        return true;
      }
    }
  }
  return false;
}
```

* **Time Complexity**: O(N * M), where N is the number of rows and M is the number of columns in the matrix.
* **Space Complexity**: O(1), as no additional space is required.

**Approach 2: Optimized using Binary Search**

* **Explanation**: Since each row is sorted, we can apply binary search on each row to find the target. We start from the top-right corner and move either left or down based on the comparison with the target.

* **C++ Code**:
```cpp
bool findTarget(vector<vector<int>>& matrix, int target) {
  int rows = matrix.size(), cols = matrix[0].size();
  int i = 0, j = cols - 1;
  
  while (i < rows && j >= 0) {
    if (matrix[i][j] == target) {
      return true;
    } else if (matrix[i][j] < target) {
      i++;
    } else {
      j--;
    }
  }
  return false;
}
```

* **Time Complexity**: O(N + M), where N is the number of rows and M is the number of columns in the matrix.
* **Space Complexity**: O(1), as no additional space is required.

**Approach 3: Using Maps**

* **Explanation**: We can create a map that stores the elements of each row as keys and their corresponding indices as values. For each row, we can search for the target value in the map in O(logN) time.

* **C++ Code**:
```cpp
bool findTarget(vector<vector<int>>& matrix, int target) {
  unordered_map<int, vector<int>> rowMap;
  
  for (int i = 0; i < matrix.size(); i++) {
    for (int j = 0; j < matrix[0].size(); j++) {
      rowMap[matrix[i][j]].push_back(i);
    }
  }

  auto it = rowMap.find(target);
  if (it != rowMap.end()) {
    return true;
  }
  return false;
}
```

* **Time Complexity**: O(N * M * logN) in the worst case when the target is not present in the matrix.
* **Space Complexity**: O(N * M), as we need to store all the elements of the matrix in the map.

**Approach 4: Using Multisets**

* **Explanation**: Similar to using maps, we can use multisets to store the elements of each row. Multisets allow us to search for elements and count their occurrences in O(logN) time.

* **C++ Code**:
```cpp
bool findTarget(vector<vector<int>>& matrix, int target) {
  multiset<int> rowSet;
  
  for (const auto& row : matrix) {
    rowSet.insert(row.begin(), row.end());
  }

  return (rowSet.find(target) != rowSet.end());
}
```

* **Time Complexity**: O(N * M * logN) in the worst case when the target is not present in the matrix.
* **Space Complexity**: O(N * M), as we need to store all the elements of the matrix in the multiset.

**Approach 5: Using Two Pointers**

* **Explanation**: We can use two pointers, one for the row and one for the column, to traverse the matrix. We start from the top-right corner and move either left or down based on the comparison with the target.

* **C++ Code**:
```cpp
bool findTarget(vector<vector<int>>& matrix, int target) {
  int rows = matrix.size(), cols = matrix[0].size();
  int i = 0, j = cols - 1;
  
  while (i >= 0 && j >= 0) {
    if (matrix[i][j] == target) {
      return true;
    } else if (matrix[i][j] < target) {
      i++;
    } else {
      j--;
    }
  }
  return false;
}
```

* **Time Complexity**: O(N + M), where N is the number of rows and M is the number of columns in the matrix.
* **Space Complexity**: O(1), as no additional space is required.### Question:

"search-in-a-sorted-2d-matrix/: Problem Statement: You have been given a 2-D array 'mat' of size 'N x M' where 'N' and 'M' denote the number of rows and columns, respectively. The elements of each row are sorted in non-decreasing order. Moreover, the first element of a row is greater than the last element of the previous row (if it exists). You are given an integer ‘target’, and your task is to find if it exists in the given 'mat' or not."

### Approach 1: Brute Force

**Explanation:**
This is the most straightforward approach. We simply iterate through each element of the matrix and check if it is equal to the target. If we find a match, we return true. Otherwise, we return false.

**Approach 1 Code:**

```cpp
bool findTarget(vector<vector<int>>& mat, int target) {
  for (int i = 0; i < mat.size(); i++) {
    for (int j = 0; j < mat[i].size(); j++) {
      if (mat[i][j] == target) {
        return true;
      }
    }
  }
  return false;
}
```

**Time and Space Complexity Analysis for Approach 1:**

* **Time Complexity:** O(NM), where N is the number of rows and M is the number of columns in the matrix.
* **Space Complexity:** O(1), as we are not using any additional space.

### Approach 2: Binary Search

**Explanation:**
This approach uses binary search to find the target in the matrix. We start by finding the row that contains the target. Once we have found the row, we can use binary search to find the target in that row.

**Approach 2 Code:**

```cpp
bool findTarget(vector<vector<int>>& mat, int target) {
  int n = mat.size();
  int m = mat[0].size();

  // Find the row that contains the target
  int left = 0;
  int right = n - 1;
  while (left <= right) {
    int mid = (left + right) / 2;
    if (mat[mid][0] == target) {
      return true;
    } else if (mat[mid][0] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  // The target is not in the first row
  int row = right;

  // Find the target in the row using binary search
  left = 0;
  right = m - 1;
  while (left <= right) {
    int mid = (left + right) / 2;
    if (mat[row][mid] == target) {
      return true;
    } else if (mat[row][mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return false;
}
```

**Time and Space Complexity Analysis for Approach 2:**

* **Time Complexity:** O(log(N) + log(M)), where N is the number of rows and M is the number of columns in the matrix.
* **Space Complexity:** O(1), as we are not using any additional space.

### Approach 3: Sliding Window

**Explanation:**
This approach uses a sliding window to find the target in the matrix. We start by creating a window of size 1x1. We then move the window from left to right and from top to bottom. For each window, we check if the target is present in it. If we find a match, we return true. Otherwise, we move the window to the next position.

**Approach 3 Code:**

```cpp
bool findTarget(vector<vector<int>>& mat, int target) {
  int n = mat.size();
  int m = mat[0].size();

  for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
      if (mat[i][j] == target) {
        return true;
      } else if (mat[i][j] > target) {
        break;
      }
    }
  }

  return false;
}
```

**Time and Space Complexity Analysis for Approach 3:**

* **Time Complexity:** O(NM), where N is the number of rows and M is the number of columns in the matrix.
* **Space Complexity:** O(1), as we are not using any additional space.

### Approach 4: Trie Data Structure

**Explanation:**
This approach uses a trie data structure to find the target in the matrix. We construct a trie from the matrix. Once the trie is constructed, we can search for the target in the trie.

**Approach 4 Code:**

```cpp
struct TrieNode {
  bool isEndOfWord;
  unordered_map<int, TrieNode*> children;
};

class Trie {
public:
  TrieNode* root;

  Trie() {
    root = new TrieNode();
  }

  void insert(vector<vector<int>>& mat) {
    TrieNode* curr = root;
    for (int i = 0; i < mat.size(); i++) {
      for (int j = 0; j < mat[i].size(); j++) {
        if (curr->children.find(mat[i][j]) == curr->children.end()) {
          curr->children[mat[i][j]] = new TrieNode();
        }
        curr = curr->children[mat[i][j]];
      }
      curr->isEndOfWord = true;
      curr = root;
    }
  }

  bool search(int target) {
    TrieNode* curr = root;
    while (target > 0) {
      int digit = target % 10;
      if (curr->children.find(digit) == curr->children.end()) {
        return false;
      }
      curr = curr->children[digit];
      target /= 10;
    }
    return curr->isEndOfWord;
  }
};

bool findTarget(vector<vector<int>>& mat, int target) {
  Trie trie;
  trie.insert(mat);
  return trie.search(target);
}
```

**Time and Space Complexity Analysis for Approach 4:**

* **Time Complexity:** O(NM + H), where N is the number of rows, M is the number of columns, and H is the height of the trie.
* **Space Complexity:** O(NM), as we are storing the entire matrix in the trie.