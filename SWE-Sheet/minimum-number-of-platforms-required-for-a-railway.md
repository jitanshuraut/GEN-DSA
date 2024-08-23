**Question**: Find the minimum number of platforms required at a railway station such that no train has to wait.

**Approach 1: Brute Force**

This approach involves considering all possible combinations of arrival and departure times and determining the maximum number of trains present at any given time.

**Approach 1 Code**:
```cpp
int findPlatform(int arr[], int dep[], int n) {
    int maxPlatforms = 0;
    for (int i = 0; i < n; i++) {
        int platforms = 0;
        for (int j = 0; j < n; j++) {
            if ((arr[i] <= arr[j] && dep[i] >= arr[j]) ||
                (arr[i] >= arr[j] && dep[i] <= dep[j]))
                platforms++;
        }
        maxPlatforms = max(maxPlatforms, platforms);
    }
    return maxPlatforms;
}
```

**Time and Space Complexity Analysis for Approach 1**:
Time Complexity: O(N^2), where N is the number of trains.
Space Complexity: O(1).

**Approach 2: Optimized using Multisets**

This approach leverages multisets to store the arrival and departure times of trains. It iterates through the two multisets simultaneously, maintaining a count of currently present trains.

**Approach 2 Code**:
```cpp
#include<bits/stdc++.h>
using namespace std;
 
int findPlatform(int arr[], int dep[], int n) {
    multiset<int> arrival(arr, arr + n);
    multiset<int> departure(dep, dep + n);
 
    int platforms = 0;
    int maxPlatforms = 0;
 
    while (!arrival.empty()) {
        if (*arrival.begin() <= *departure.begin()) {
            platforms++;
            arrival.erase(arrival.begin());
        } else {
            platforms--;
            departure.erase(departure.begin());
        }
        maxPlatforms = max(maxPlatforms, platforms);
    }
 
    return maxPlatforms;
}
```

**Time and Space Complexity Analysis for Approach 2**:
Time Complexity: O(N log N), where N is the number of trains.
Space Complexity: O(N).

**Approach 3: Optimized using Sorting and Two Pointers**

This approach sorts the arrival and departure times and then uses two pointers to simulate the platform utilization.

**Approach 3 Code**:
```cpp
int findPlatform(int arr[], int dep[], int n) {
    sort(arr, arr + n);
    sort(dep, dep + n);
 
    int platforms = 0, maxPlatforms = 0;
    int i = 0, j = 0;
 
    while (i < n && j < n) {
        if (arr[i] <= dep[j]) {
            platforms++;
            i++;
        } else {
            platforms--;
            j++;
        }
        maxPlatforms = max(maxPlatforms, platforms);
    }
 
    return maxPlatforms;
}
```

**Time and Space Complexity Analysis for Approach 3**:
Time Complexity: O(N log N), where N is the number of trains.
Space Complexity: O(1).

**Additional Notes:**

* Other approaches include using a greedy algorithm, a recursive approach, or backtracking.
* The choice of approach depends on factors such as the size of the input and the desired time/space trade-off.**Question**: Minimum Number of Platforms Required for a Railway

**Problem Statement**: Given two arrays that represent the arrival and departure times of trains that stop at the platform, find the minimum number of platforms needed at the railway station so that no train has to wait.

### Approach 1: Sorting and Two Pointers

**Explanation**:
Sort the arrival and departure times in ascending order. Use two pointers, one pointing to the arrival times and the other to the departure times. Keep track of the maximum number of trains simultaneously present on the platform `max_trains`. Update `max_trains` as the pointers move forward to identify the maximum number of platforms required.

**C++ Code**:
```cpp
#include <algorithm>

int findMinPlatforms(int arrival[], int departure[], int n) {
  sort(arrival, arrival + n);
  sort(departure, departure + n);

  int i = 0, j = 0, max_trains = 0, current_trains = 0;
  while (i < n) {
    if (arrival[i] < departure[j]) {
      current_trains++;
      max_trains = max(max_trains, current_trains);
      i++;
    } else {
      current_trains--;
      j++;
    }
  }

  return max_trains;
}
```

**Time and Space Complexity**:
* Time complexity: O(N*log(N)) for sorting.
* Space complexity: O(1), as constant space is used.

### Approach 2: Priority Queue

**Explanation**:
Insert arrival and departure times into a priority queue, sorted based on departure times. For each arrival time, increment the count of currently active trains. For each departure time, decrement the count and check if it's the last departure time. If so, also decrement the count of minimum platforms required.

**C++ Code**:
```cpp
#include <queue>

int findMinPlatforms(int arrival[], int departure[], int n) {
  priority_queue<int, vector<int>, greater<int>> pq;
  sort(departure, departure + n);

  int min_platforms = 0, current_trains = 0;

  for (int i = 0, j = 0; i < n; i++) {
    current_trains++;
    pq.push(departure[j]);
    min_platforms = max(min_platforms, current_trains);

    while (!pq.empty() && pq.top() <= arrival[i]) {
      pq.pop();
      current_trains--;
    }
  }

  return min_platforms;
}
```

**Time and Space Complexity**:
* Time complexity: O(N*log(N)) for priority queue operations.
* Space complexity: O(N) for storing departure times.