**Question**: n-meetings-in-one-room/: Problem Statement: There is one meeting room in a firm. You are given two arrays, start and end each of size N.For an index ‘i’, start[i] denotes the starting time of the ith meeting while end[i]  will denote the ending time of the ith meeting. Find the maximum number of meetings that can be accommodated if only one meeting can happen in the room at a  particular time. Print the order in which these meetings will be performed.

**Approach 1: Brute Force**
* Create a 2D array of size N x N to store the overlap between every pair of meetings.
* Iterate over the 2D array and find the maximum overlap.
* The maximum overlap will correspond to the maximum number of meetings that can be accommodated.

**Approach 1 Code:**
```cpp
#include<bits/stdc++.h>

using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> start(n), end(n);
  for (int i = 0; i < n; i++) {
    cin >> start[i] >> end[i];
  }
  int overlap[n][n];
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
      overlap[i][j] = max(0, min(end[i], end[j]) - max(start[i], start[j]));
    }
  }
  int max_overlap = 0;
  for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
      max_overlap = max(max_overlap, overlap[i][j]);
    }
  }
  cout << max_overlap << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1:**
* Time Complexity: O(N^2).
* Space Complexity: O(N^2).

**Approach 2: Optimized Approaches using Maps**
* Create a map to store the start and end times of each meeting.
* Sort the map by the start times of the meetings.
* Iterate over the sorted map and find the maximum number of meetings that can be accommodated.

**Approach 2 Code:**
```cpp
#include<bits/stdc++.h>

using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> start(n), end(n);
  for (int i = 0; i < n; i++) {
    cin >> start[i] >> end[i];
  }
  map<int, int> meetings;
  for (int i = 0; i < n; i++) {
    meetings.insert({start[i], end[i]});
  }
  map<int, int>::iterator it = meetings.begin();
  int max_meetings = 0;
  int end_time = 0;
  while (it != meetings.end()) {
    if (it->first >= end_time) {
      max_meetings++;
      end_time = it->second;
    }
    it++;
  }
  cout << max_meetings << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2:**
* Time Complexity: O(N log N).
* Space Complexity: O(N).

**Approach 3: Optimized Approaches using Multisets**
* Create a multiset to store the end times of the meetings.
* Sort the multiset in ascending order.
* Iterate over the sorted multiset and find the maximum number of meetings that can be accommodated.

**Approach 3 Code:**
```cpp
#include<bits/stdc++.h>

using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> start(n), end(n);
  for (int i = 0; i < n; i++) {
    cin >> start[i] >> end[i];
  }
  multiset<int> end_times;
  for (int i = 0; i < n; i++) {
    end_times.insert(end[i]);
  }
  int max_meetings = 0;
  int end_time = 0;
  for (multiset<int>::iterator it = end_times.begin(); it != end_times.end(); it++) {
    if (*it >= end_time) {
      max_meetings++;
      end_time = *it;
    }
  }
  cout << max_meetings << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 3:**
* Time Complexity: O(N log N).
* Space Complexity: O(N).

**Approach 4: Optimized Approaches using Binary Search**
* Sort the start and end times of the meetings in ascending order.
* Perform a binary search on the sorted end times to find the minimum end time that is greater than or equal to the start time of the current meeting.
* If the binary search is successful, then increment the count of meetings and update the end time to the minimum end time found.

**Approach 4 Code:**
```cpp
#include<bits/stdc++.h>

using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> start(n), end(n);
  for (int i = 0; i < n; i++) {
    cin >> start[i] >> end[i];
  }
  sort(start.begin(), start.end());
  sort(end.begin(), end.end());
  int max_meetings = 0;
  int end_time = 0;
  for (int i = 0; i < n; i++) {
    int index = lower_bound(end.begin(), end.end(), start[i]) - end.begin();
    if (index < n && end[index] >= start[i]) {
      max_meetings++;
      end_time = end[index];
    }
  }
  cout << max_meetings << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 4:**
* Time Complexity: O(N log N).
* Space Complexity: O(N).

**Approach 5: Optimized Approaches using Two Pointers**
* Sort the start and end times of the meetings in ascending order.
* Two pointers, i and j, are used to keep track of the current meeting and the next meeting, respectively.
* If the start time of the next meeting is greater than or equal to the end time of the current meeting, then the current meeting is included in the maximum number of meetings.
* Otherwise, the next meeting becomes the current meeting, and the process is repeated.

**Approach 5 Code:**
```cpp
#include<bits/stdc++.h>

using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> start(n), end(n);
  for (int i = 0; i < n; i++) {
    cin >> start[i] >> end[i];
  }
  sort(start.begin(), start.end());
  sort(end.begin(), end.end());
  int i = 0, j = 0;
  int max_meetings = 0;
  while (i < n && j < n) {
    if (start[j] >= end[i]) {
      max_meetings++;
      i++;
      j++;
    } else {
      j++;
    }
  }
  cout << max_meetings << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 5:**
* Time Complexity: O(N log N).
* Space Complexity: O(N).

**Approach 6: Greedy Algorithms**
* Sort the meetings by their end times.
* Select the meeting with the earliest end time.
* Remove all meetings that overlap with the selected meeting.
* Repeat the process until no more meetings are left.

**Approach 6 Code:**
```cpp
#include<bits/stdc++.h>

using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> start(n), end(n);
  for (int i = 0; i < n; i++) {
    cin >> start[i] >> end[i];
  }
  sort(end.begin(), end.end());
  int max_meetings = 0;
  int end_time = 0;
  for (int i = 0; i < n; i++) {
    if (start[i] >= end_time) {
      max_meetings++;
      end_time = end[i];
    }
  }**Question**: n-meetings-in-one-room/: Problem Statement: There is one meeting room in a firm. You are given two arrays, start and end each of size N.For an index ‘i’, start[i] denotes the starting time of the ith meeting while end[i] will denote the ending time of the ith meeting. Find the maximum number of meetings that can be accommodated if only one meeting can happen in the room at a particular time. Print the order in which these meetings will be performed.

**Approach 1: Sorting of Meetings**
**Explanation**: This approach involves sorting the meetings based on their ending times, and then iterating over the sorted list to find the maximum number of meetings that can be accommodated in the room.
**Code**:
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Meeting {
  int start;
  int end;
};

bool compare(Meeting m1, Meeting m2) {
  return m1.end < m2.end;
}

int main() {
  int n;
  cin >> n;

  Meeting meetings[n];
  for (int i = 0; i < n; i++) {
    cin >> meetings[i].start >> meetings[i].end;
  }

  sort(meetings, meetings + n, compare);

  int count = 1;
  int ending_time = meetings[0].end;

  for (int i = 1; i < n; i++) {
    if (meetings[i].start >= ending_time) {
      count++;
      ending_time = meetings[i].end;
    }
  }

  cout << count << endl;
  for (int i = 0; i < n; i++) {
    if (meetings[i].start >= ending_time) {
      cout << i + 1 << " ";
      ending_time = meetings[i].end;
    }
  }

  return 0;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N log N), where N is the number of meetings.
* Space Complexity: O(N), for sorting the meetings.

**Approach 2: Priority Queue**
**Explanation**: This approach uses a priority queue to store the meetings, which are sorted based on their ending times. The priority queue is then used to select the meeting with the earliest ending time, and the process is repeated until all meetings are processed.
**Code**:
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Meeting {
  int start;
  int end;
};

bool compare(Meeting m1, Meeting m2) {
  return m1.end < m2.end;
}

int main() {
  int n;
  cin >> n;

  Meeting meetings[n];
  for (int i = 0; i < n; i++) {
    cin >> meetings[i].start >> meetings[i].end;
  }

  sort(meetings, meetings + n, compare);

  priority_queue<Meeting, vector<Meeting>, compare> pq;
  pq.push(meetings[0]);

  int count = 1;

  for (int i = 1; i < n; i++) {
    if (meetings[i].start >= pq.top().end) {
      pq.pop();
      pq.push(meetings[i]);
      count++;
    }
  }

  cout << count << endl;
  while (!pq.empty()) {
    cout << pq.top().start << " " << pq.top().end << endl;
    pq.pop();
  }

  return 0;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N log N), where N is the number of meetings.
* Space Complexity: O(N), for sorting the meetings and using the priority queue.

**Approach 3: Disjoint Set Union (DSU)**
**Explanation**: This approach uses DSU to create a set of non-overlapping intervals, which represent the time slots when meetings can be held. The DSU operations are used to merge overlapping intervals and find the maximum number of non-overlapping intervals.
**Code**:
```cpp
#include <bits/stdc++.h>
using namespace std;

struct Meeting {
  int start;
  int end;
};

struct DSU {
  vector<int> parent;
  vector<int> size;

  DSU(int n) {
    parent.resize(n);
    size.resize(n);
    for (int i = 0; i < n; i++) {
      parent[i] = i;
      size[i] = 1;
    }
  }

  int find_parent(int node) {
    if (parent[node] == node) {
      return node;
    }
    return parent[node] = find_parent(parent[node]);
  }

  void merge(int a, int b) {
    int root_a = find_parent(a);
    int root_b = find_parent(b);
    if (root_a != root_b) {
      if (size[root_a] > size[root_b]) {
        parent[root_b] = root_a;
        size[root_a] += size[root_b];
      } else {
        parent[root_a] = root_b;
        size[root_b] += size[root_a];
      }
    }
  }
};

int main() {
  int n;
  cin >> n;

  Meeting meetings[n];
  for (int i = 0; i < n; i++) {
    cin >> meetings[i].start >> meetings[i].end;
  }

  DSU dsu(n);

  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      if (meetings[i].end <= meetings[j].start) {
        dsu.merge(i, j);
      }
    }
  }

  int max_size = 0;
  for (int i = 0; i < n; i++) {
    max_size = max(max_size, dsu.size[dsu.find_parent(i)]);
  }

  cout << max_size << endl;
  for (int i = 0; i < n; i++) {
    if (dsu.find_parent(i) == i) {
      cout << i + 1 << " ";
    }
  }

  return 0;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N^2), where N is the number of meetings.
* Space Complexity: O(N), for the DSU data structure.