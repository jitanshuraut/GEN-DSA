## Question:
**sort-an-array-of-0s-1s-and-2s/:**
Problem Statement: Given an array consisting of only 0s, 1s, and 2s. Write a program to in-place sort the array without using inbuilt sort functions. ( Expected: Single pass-O(N) and constant space)

## Approach 1: Brute Force

**Explanation:**
This approach uses nested loops to compare each element with every other element. For each pair of elements, if they are in the wrong order, they are swapped.

**Approach 1 Code:**
```cpp
void bruteForceSort(int arr[], int n) {
  for (int i = 0; i < n - 1; i++) {
    for (int j = i + 1; j < n; j++) {
      if (arr[i] > arr[j]) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 1:**
* Time Complexity: O(N^2), where N is the length of the array. The nested loops iterate over all pairs of elements in the array.
* Space Complexity: O(1), as no additional space is allocated.

## Approach 2: Optimized using Two Pointers

**Explanation:**
This approach uses two pointers, one to track the current position in the array and one to track the position where the 2s should start. The algorithm iterates through the array, moving the first pointer to the next unprocessed element. If the element is a 2, it is swapped with the element at the position pointed to by the second pointer, and the second pointer is advanced. This process continues until all the 2s are grouped together at the end of the array.

**Approach 2 Code:**
```cpp
void twoPointersSort(int arr[], int n) {
  int zero = 0, two = n - 1, i = 0;

  while (i <= two) {
    if (arr[i] == 0) {
      swap(arr[i], arr[zero]);
      zero++;
      i++;
    } else if (arr[i] == 2) {
      swap(arr[i], arr[two]);
      two--;
    } else {
      i++;
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 2:**
* Time Complexity: O(N), where N is the length of the array. The algorithm iterates through the array once.
* Space Complexity: O(1), as no additional space is allocated.

## Approach 3: Optimized using Dutch National Flag Algorithm

**Explanation:**
This approach, also known as the three-way partitioning algorithm, works by dividing the array into three partitions: elements less than 1, elements equal to 1, and elements greater than 1. The algorithm uses three pointers to keep track of the boundaries of each partition. It then iterates through the array, moving the pointers to ensure that each element is in the correct partition.

**Approach 3 Code:**
```cpp
void dutchNationalFlagSort(int arr[], int n) {
  int low = 0, mid = 0, high = n - 1;

  while (mid <= high) {
    switch (arr[mid]) {
      case 0:
        swap(arr[low], arr[mid]);
        low++;
        mid++;
        break;

      case 1:
        mid++;
        break;

      case 2:
        swap(arr[mid], arr[high]);
        high--;
        break;
    }
  }
}
```

**Time and Space Complexity Analysis for Approach 3:**
* Time Complexity: O(N), where N is the length of the array. The algorithm iterates through the array once.
* Space Complexity: O(1), as no additional space is allocated.**Question**: Given an array consisting of only 0s, 1s, and 2s. Write a program to in-place sort the array without using inbuilt sort functions. ( Expected: Single pass-O(N) and constant space) 

**Approach 1: Dutch National Flag Algorithm**
* **Explanation**:
  * Initialize three pointers: low to point to the start of the array, mid to point to the current index, and high to point to the end of the array.
  * Iterate through the array using the mid pointer.
  * If the element pointed to by mid is 0, swap it with the element pointed to by low and increment both low and mid.
  * If the element pointed to by mid is 2, swap it with the element pointed to by high and decrement high.
  * If the element pointed to by mid is 1, just increment mid.
  * Repeat steps 2-4 until mid reaches the end of the array.

**Approach 1 Code**:
```cpp
void sort012(int arr[], int n) 
{ 
    int low = 0;
    int mid = 0; 
    int high = n - 1; 
  
    while (mid <= high) { 
        switch (arr[mid]) { 
 
        case 0: 
            swap(arr[low++], arr[mid++]); 
            break; 
  
        case 1: 
            mid++; 
            break; 
  
        case 2: 
            swap(arr[mid], arr[high--]); 
            break; 
        } 
    } 
} 
```

**Time and Space Complexity Analysis for Approach 1**:
* **Time Complexity**: O(N), where N is the size of the array. It performs a single pass through the array and constant time operations for each element.
* **Space Complexity**: O(1). It uses three pointers and a constant amount of extra space.

**Approach 2: Counting Sort**
* **Explanation**:
  * Count the number of 0s, 1s, and 2s in the array.
  * Replace the first count[0] elements with 0s.
  * Replace the next count[1] elements with 1s.
  * Replace the remaining elements with 2s.

**Approach 2 Code**:
```cpp
void sort012(int arr[], int n) 
{ 
    int count[3] = {0, 0, 0};
    for (int i = 0; i < n; i++) 
        count[arr[i]]++; 
    int j = 0; 
    for (int i = 0; i < count[0]; i++) 
        arr[j++] = 0; 
    for (int i = 0; i < count[1]; i++) 
        arr[j++] = 1; 
    for (int i = 0; i < count[2]; i++) 
        arr[j++] = 2; 
} 
```

**Time and Space Complexity Analysis for Approach 2**:
* **Time Complexity**: O(N), where N is the size of the array. It performs a single pass through the array and constant time operations for each element.
* **Space Complexity**: O(1). It uses an array of size 3 to store counts and a constant amount of extra space.

**Approach 3: Radix Sort**
* **Explanation**:
  * Radix sort works by sorting the array based on individual digits or bits.
  * In this case, we can radix sort the array based on the 0s, 1s, and 2s.
  * Create three empty lists: one for 0s, one for 1s, and one for 2s.
  * Iterate through the array and add each element to the corresponding list.
  * Concatenate the three lists to obtain the sorted array.

**Approach 3 Code**:
```cpp
void sort012(int arr[], int n) 
{ 
    vector<int> zero, one, two;
    for (int i = 0; i < n; i++) { 
        if (arr[i] == 0) 
            zero.push_back(arr[i]); 
        else if (arr[i] == 1) 
            one.push_back(arr[i]); 
        else if (arr[i] == 2) 
            two.push_back(arr[i]); 
    } 
    int k = 0; 
    for (auto x : zero) 
        arr[k++] = x; 
    for (auto x : one) 
        arr[k++] = x; 
    for (auto x : two) 
        arr[k++] = x; 
} 
```

**Time and Space Complexity Analysis for Approach 3**:
* **Time Complexity**: O(N), where N is the size of the array. It performs a single pass through the array and constant time operations for each element.
* **Space Complexity**: O(N), as it requires extra space to store the three lists.