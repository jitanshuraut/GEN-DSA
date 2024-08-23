**Question**: count-inversions-in-an-array/: Problem Statement: Given an array of N integers, count the inversion of the array (using merge-sort).

**Approach 1: Brute Force**

**Explanation:** This approach involves nested loops to compare each pair of elements and count inversions.

**Brute Force Code:**

```cpp
#include <iostream>
#include <vector>

using namespace std;

int countInversions(vector<int> arr) {
    int n = arr.size();
    int cnt = 0;
    
    for (int i = 0; i < n; ++i) {
        for (int j = i + 1; j < n; ++j) {
            if (arr[i] > arr[j]) {
                cnt += 1;
            }
        }
    }
    
    return cnt;
}

int main() {
    vector<int> arr = {1, 5, 3, 2, 4};

    int inversion_count = countInversions(arr);
    cout << "Inversion Count: " << inversion_count << endl;

    return 0;
}
```

**Time and Space Complexity Analysis:**

* Time Complexity: O(N^2)
* Space Complexity: O(1)

**Approach 2: Merge Sort**

**Explanation:** Merge sort inherently counts inversions while merging the sorted sub-arrays. This approach is efficient for large arrays.

**Merge Sort Code:**

```cpp
#include <iostream>
#include <vector>

using namespace std;

int merge(vector<int>& arr, int low, int mid, int high) {
    int n1 = mid - low + 1;
    int n2 = high - mid;
    
    vector<int> left(n1);
    vector<int> right(n2);
    
    for (int i = 0; i < n1; ++i) {
        left[i] = arr[low + i];
    }
    
    for (int i = 0; i < n2; ++i) {
        right[i] = arr[mid + 1 + i];
    }
    
    int i = 0, j = 0, k = low, inv_count = 0;
    
    while (i < n1 && j < n2) {
        if (left[i] <= right[j]) {
            arr[k++] = left[i++];
        } else {
            arr[k++] = right[j++];
            inv_count += (n1 - i);
        }
    }
    
    while (i < n1) {
        arr[k++] = left[i++];
    }
    
    while (j < n2) {
        arr[k++] = right[j++];
    }
    
    return inv_count;
}

int mergeSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int mid = (low + high) / 2;
        int inv_count = mergeSort(arr, low, mid);
        inv_count += mergeSort(arr, mid + 1, high);
        inv_count += merge(arr, low, mid, high);
        return inv_count;
    }
    
    return 0;
}

int countInversions(vector<int> arr) {
    return mergeSort(arr, 0, arr.size() - 1);
}

int main() {
    vector<int> arr = {1, 5, 3, 2, 4};

    int inversion_count = countInversions(arr);
    cout << "Inversion Count: " << inversion_count << endl;

    return 0;
}
```

**Time and Space Complexity Analysis:**

* Time Complexity: O(N log N)
* Space Complexity: O(N)**Question:** count-inversions-in-an-array/: Problem Statement: Given an array of N integers, count the inversion of the array (using merge-sort).

**Approach 1: Brute Force Approach**

**Explanation:**
This approach involves checking every pair of elements in the array and incrementing the inversion count whenever a smaller element appears after a larger element.

**Approach 1 Code:**

```cpp
int countInversions(int arr[], int n) {
  int inversion_count = 0;
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      if (arr[i] > arr[j]) {
        inversion_count++;
      }
    }
  }
  return inversion_count;
}
```

**Time and Space Complexity Analysis for Approach 1:**

* **Time Complexity:** O(n^2), where n is the number of elements in the array.
* **Space Complexity:** O(1)

**Approach 2: Merge Sort**

**Explanation:**
This approach uses the divide-and-conquer strategy of merge sort to count inversions efficiently. During the merge step, when merging two sorted subarrays, we count inversions by keeping track of elements in the left subarray that are larger than elements in the right subarray.

**Approach 2 Code:**

```cpp
int merge(int arr[], int low, int mid, int high) {
  int n1 = mid - low + 1;
  int n2 = high - mid;

  int left[n1], right[n2];

  for (int i = 0; i < n1; i++) {
    left[i] = arr[low + i];
  }

  for (int i = 0; i < n2; i++) {
    right[i] = arr[mid + 1 + i];
  }

  int i = 0, j = 0, k = low, inversion_count = 0;

  while (i < n1 && j < n2) {
    if (left[i] <= right[j]) {
      arr[k++] = left[i++];
    } else {
      arr[k++] = right[j++];
      inversion_count += n1 - i;
    }
  }

  while (i < n1) {
    arr[k++] = left[i++];
  }

  while (j < n2) {
    arr[k++] = right[j++];
  }

  return inversion_count;
}

int mergeSortAndCountInversions(int arr[], int low, int high) {
  if (low < high) {
    int mid = low + (high - low) / 2;

    int left_count = mergeSortAndCountInversions(arr, low, mid);
    int right_count = mergeSortAndCountInversions(arr, mid + 1, high);
    int merge_count = merge(arr, low, mid, high);

    return left_count + right_count + merge_count;
  }

  return 0;
}

int countInversions(int arr[], int n) {
  return mergeSortAndCountInversions(arr, 0, n - 1);
}
```

**Time and Space Complexity Analysis for Approach 2:**

* **Time Complexity:** O(n log n), where n is the number of elements in the array.
* **Space Complexity:** O(n), as additional space is required for the temporary arrays used during merging.

**Note:**

The merge sort approach is generally preferred over the brute force approach due to its better time complexity.