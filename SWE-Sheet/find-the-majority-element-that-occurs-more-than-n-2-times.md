**Question**: Find the majority element that occurs more than N/2 times in a given array.

**Approach 1: Brute Force**

**Explanation**: Iterate over all elements of the array and count the number of occurrences of each element. Return the element with the highest frequency count.

**Code**:

```cpp
int findMajorityBrute(int arr[], int n) {
    int maxCount = 0;
    int majorityIndex = -1;

    for (int i = 0; i < n; i++) {
        int count = 0;
        for (int j = 0; j < n; j++) {
            if (arr[i] == arr[j]) {
                count++;
            }
        }

        if (count > maxCount) {
            maxCount = count;
            majorityIndex = i;
        }
    }

    return arr[majorityIndex];
}
```

**Time Complexity**: O(N^2)
**Space Complexity**: O(1)

**Approach 2: Optimized using HashMap**

**Explanation**: Use a HashMap to store element counts. Iterate over the array and update the count for each element. Return the element with the highest count.

**Code**:

```cpp
int findMajorityHashMap(int arr[], int n) {
    unordered_map<int, int> countMap;

    for (int i = 0; i < n; i++) {
        countMap[arr[i]]++;
    }

    int majorityElement = -1;
    int maxCount = 0;
    for (const auto& [element, count] : countMap) {
        if (count > maxCount) {
            maxCount = count;
            majorityElement = element;
        }
    }

    return majorityElement;
}
```

**Time Complexity**: O(N)
**Space Complexity**: O(N)

**Approach 3: Optimized using Moore's Voting Algorithm**

**Explanation**: The idea is to keep track of a candidate majority element and its count. Iterate over the array and update the candidate if the current element is the same as the candidate, or reset the candidate if the current element is different. Return the candidate if its count is greater than N/2.

**Code**:

```cpp
int findMajorityMoores(int arr[], int n) {
    int candidate = -1;
    int count = 0;

    for (int i = 0; i < n; i++) {
        if (count == 0) {
            candidate = arr[i];
            count = 1;
        } else {
            if (candidate == arr[i]) {
                count++;
            } else {
                count--;
            }
        }
    }

    // Verify if the candidate is actually the majority element
    count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == candidate) {
            count++;
        }
    }

    if (count > n / 2) {
        return candidate;
    } else {
        return -1;
    }
}
```

**Time Complexity**: O(N)
**Space Complexity**: O(1)

**Approach 4: Randomized Approach**

**Explanation**: Pick a random element from the array and count its occurrences. If the count is greater than N/2, return the element. Otherwise, repeat the process with another random element.

**Code**:

```cpp
int findMajorityRandomized(int arr[], int n) {
    srand(time(NULL));
    while (true) {
        int randomIndex = rand() % n;
        int candidate = arr[randomIndex];
        int count = 0;

        for (int i = 0; i < n; i++) {
            if (arr[i] == candidate) {
                count++;
            }
        }

        if (count > n / 2) {
            return candidate;
        }
    }
}
```

**Time Complexity**: O(N) on average
**Space Complexity**: O(1)

**Note**: The randomized approach is not deterministic and may fail in some rare cases where the majority element is not found. However, it has a very high probability of success.**Question**: "find-the-majority-element-that-occurs-more-than-n-2-times/: Problem Statement: Given an array of N integers, write a program to return an element that occurs more than N/2 times in the given array. You may consider that such an element always exists in the array."

**Approach 1: Boyer-Moore Majority Voting Algorithm**
**Explanation**: The Boyer-Moore Algorithm maintains two variables - a candidate and a counter. It iterates through the array, and if the candidate is the same as the current element, it increases the counter. Otherwise, if the counter is 0, it sets the candidate to the current element and sets the counter to 1. If the counter is greater than 0, it decreases the counter by 1. Finally, it returns the candidate, as it is guaranteed to be the majority element.

**Approach 1 Code**:
```cpp
int findMajorityElement(int arr[], int n)
{
    int candidate = -1;
    int votes = 0;

    for (int i = 0; i < n; i++)
    {
        if (arr[i] == candidate)
        {
            votes++;
        }
        else if (votes == 0)
        {
            candidate = arr[i];
            votes = 1;
        }
        else
        {
            votes--;
        }
    }

    // Verify if candidate appears more than N/2 times
    votes = 0;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == candidate)
        {
            votes++;
        }
    }

    if (votes > n / 2)
    {
        return candidate;
    }

    return -1;
}
```

**Time and Space Complexity Analysis for Approach 1**:
* Time Complexity: O(N), where N is the size of the array.
* Space Complexity: O(1), as it uses constant space.

**Approach 2: Hashing**
**Explanation**: The Hashing approach uses a hash table to keep track of the frequency of each element in the array. It iterates through the array, updating the frequency of each element in the hash table. After the first iteration, it finds the element with the highest frequency and returns it.

**Approach 2 Code**:
```cpp
#include<unordered_map>

int findMajorityElement(int arr[], int n)
{
    unordered_map<int, int> frequency;

    for (int i = 0; i < n; i++)
    {
        frequency[arr[i]]++;
    }

    int maxFreq = 0;
    int majorityElement;

    for (auto it : frequency)
    {
        if (it.second > maxFreq)
        {
            maxFreq = it.second;
            majorityElement = it.first;
        }
    }

    return majorityElement;
}
```

**Time and Space Complexity Analysis for Approach 2**:
* Time Complexity: O(N), where N is the size of the array.
* Space Complexity: O(N), as the hash table can potentially store all elements in the array.

**Approach 3: Divide and Conquer**
**Explanation**: The Divide and Conquer approach recursively divides the array into smaller subarrays until the subarrays have only one element. It then combines the majority elements of the subarrays to find the majority element of the entire array.

**Approach 3 Code**:
```cpp
int findMajorityElement(int arr[], int n)
{
    if (n == 1)
    {
        return arr[0];
    }

    int mid = n / 2;

    int leftMajority = findMajorityElement(arr, mid);
    int rightMajority = findMajorityElement(arr + mid, n - mid);

    if (leftMajority == rightMajority)
    {
        return leftMajority;
    }

    // Find the actual majority element
    int leftCount = 0;
    int rightCount = 0;

    for (int i = 0; i < n; i++)
    {
        if (arr[i] == leftMajority)
        {
            leftCount++;
        }
        else if (arr[i] == rightMajority)
        {
            rightCount++;
        }
    }

    if (leftCount > n / 2)
    {
        return leftMajority;
    }
    else if (rightCount > n / 2)
    {
        return rightMajority;
    }

    return -1;
}
```

**Time and Space Complexity Analysis for Approach 3**:
* Time Complexity: O(N log N), where N is the size of the array.
* Space Complexity: O(log N), as the recursion stack depth is O(log N).

**Approach 4: Linear Search**
**Explanation**: The Linear Search approach iterates through the array and keeps track of the majority element and its count. It updates the majority element and count if a different element is encountered more frequently than the current majority element.

**Approach 4 Code**:
```cpp
int findMajorityElement(int arr[], int n)
{
    int majorityElement = arr[0];
    int count = 1;

    for (int i = 1; i < n; i++)
    {
        if (arr[i] == majorityElement)
        {
            count++;
        }
        else
        {
            count--;
        }

        if (count == 0)
        {
            majorityElement = arr[i];
            count = 1;
        }
    }

    // Verify if majority element appears more than N/2 times
    count = 0;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == majorityElement)
        {
            count++;
        }
    }

    if (count > n / 2)
    {
        return majorityElement;
    }

    return -1;
}
```

**Time and Space Complexity Analysis for Approach 4**:
* Time Complexity: O(N), where N is the size of the array.
* Space Complexity: O(1), as it uses constant space.

**Approach 5: Sorting**
**Explanation**: The Sorting approach sorts the array and selects the middle element as the majority element. Since the majority element occurs more than N/2 times, it will be present at the middle index of the sorted array.

**Approach 5 Code**:
```cpp
int findMajorityElement(int arr[], int n)
{
    sort(arr, arr + n);
    return arr[n / 2];
}
```

**Time and Space Complexity Analysis for Approach 5**:
* Time Complexity: O(N log N), where N is the size of the array.
* Space Complexity: O(1), if the sorting algorithm is in-place; otherwise, O(N), if extra space is required for sorting.