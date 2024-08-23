**Question**: merge-overlapping-sub-intervals/: Problem Statement: Given an array of intervals, merge all the overlapping intervals and return an array of non-overlapping intervals.

**Approach 1: Brute Force**

**Explanation:**
This approach uses a brute-force strategy by comparing each interval with every other interval in the array. If two intervals overlap, they are merged into a single interval. The merged interval replaces the original intervals in the array. This process is repeated until there are no more overlapping intervals in the array.

**Approach 1 Code:**
```cpp
#include <vector>

using namespace std;

struct Interval {
    int start;
    int end;
};

vector<Interval> mergeIntervals(vector<Interval>& intervals) {
    vector<Interval> mergedIntervals;

    for (Interval& interval1 : intervals) {
        // Check if the current interval overlaps with any existing merged interval
        bool overlapped = false;
        for (Interval& mergedInterval : mergedIntervals) {
            if (interval1.start <= mergedInterval.end && interval1.end >= mergedInterval.start) {
                // Update the start and end of the merged interval
                mergedInterval.start = min(mergedInterval.start, interval1.start);
                mergedInterval.end = max(mergedInterval.end, interval1.end);
                overlapped = true;
                break;
            }
        }

        // If the current interval does not overlap with any merged interval, add it to the result
        if (!overlapped) {
            mergedIntervals.push_back(interval1);
        }
    }

    return mergedIntervals;
}
```

**Time and Space Complexity Analysis for Approach 1:**
The time complexity of the brute-force approach is O(n^2), where n is the number of intervals in the array. This is because each interval is compared with every other interval in the array. The space complexity is O(n), as the number of intervals in the result can be at most n.

**Approach 2: Optimized Approach using Sorting and Merging**

**Explanation:**
This approach uses sorting to optimize the brute-force approach. The intervals are first sorted by their start times. Then, the intervals are merged one by one, starting from the first interval. The process continues until all intervals are merged.

**Approach 2 Code:**
```cpp
#include <vector>
#include <algorithm>

using namespace std;

struct Interval {
    int start;
    int end;
};

bool compareIntervals(Interval& interval1, Interval& interval2) {
    return interval1.start < interval2.start;
}

vector<Interval> mergeIntervals(vector<Interval>& intervals) {
    // Sort the intervals by their start times
    sort(intervals.begin(), intervals.end(), compareIntervals);

    vector<Interval> mergedIntervals;
    mergedIntervals.push_back(intervals[0]);

    for (int i = 1; i < intervals.size(); i++) {
        Interval& currentInterval = intervals[i];

        // Check if the current interval overlaps with the last merged interval
        Interval& lastMergedInterval = mergedIntervals.back();
        if (currentInterval.start <= lastMergedInterval.end) {
            // Update the end of the last merged interval
            lastMergedInterval.end = max(lastMergedInterval.end, currentInterval.end);
        } else {
            // Add the current interval to the merged intervals
            mergedIntervals.push_back(currentInterval);
        }
    }

    return mergedIntervals;
}
```

**Time and Space Complexity Analysis for Approach 2:**
The time complexity of the optimized approach is O(n log n), where n is the number of intervals in the array. This is because sorting the intervals takes O(n log n) time. The space complexity is still O(n), as the number of intervals in the result can be at most n.

**Approach 3: Greedy Algorithm using Priority Queue**

**Explanation:**
This approach uses a greedy algorithm and a priority queue to merge the intervals. The intervals are sorted by their start times. Then, the intervals are processed one by one. At each step, the interval with the smallest start time is merged with the current overlapping interval (if any).

**Approach 3 Code:**
```cpp
#include <vector>
#include <queue>

using namespace std;

struct Interval {
    int start;
    int end;
};

bool compareIntervals(Interval& interval1, Interval& interval2) {
    return interval1.start < interval2.start;
}

vector<Interval> mergeIntervals(vector<Interval>& intervals) {
    // Sort the intervals by their start times
    sort(intervals.begin(), intervals.end(), compareIntervals);

    // Create a priority queue to store the overlapping intervals
    priority_queue<Interval, vector<Interval>, compareIntervals> pq;

    vector<Interval> mergedIntervals;

    for (Interval& interval : intervals) {
        // If the current interval overlaps with the top of the priority queue, merge them
        if (!pq.empty() && interval.start <= pq.top().end) {
            Interval& top = pq.top();
            top.end = max(top.end, interval.end);
        } else {
            // Otherwise, add the current interval to the priority queue
            pq.push(interval);
        }
    }

    // Extract the merged intervals from the priority queue
    while (!pq.empty()) {
        mergedIntervals.push_back(pq.top());
        pq.pop();
    }

    return mergedIntervals;
}
```

**Time and Space Complexity Analysis for Approach 3:**
The time complexity of the greedy algorithm is O(n log n), where n is the number of intervals in the array. This is because sorting the intervals takes O(n log n) time, and processing each interval takes O(log n) time. The space complexity is O(n), as the priority queue can store at most n intervals.

**Approach 4: Union-Find Algorithm**

**Explanation:**
This approach uses the union-find algorithm to find the connected components of the intervals. The intervals are represented as nodes in a graph, and the edges between the nodes represent the overlaps between the intervals. The union-find algorithm is used to merge the connected components, which corresponds to merging the overlapping intervals.

**Approach 4 Code:**
```cpp
#include <vector>
#include <map>

using namespace std;

struct Interval {
    int start;
    int end;
};

struct UnionFind {
    map<int, int> parents;
    map<int, int> ranks;

    UnionFind() {}

    void makeSet(int x) {
        parents[x] = x;
        ranks[x] = 0;
    }

    int find(int x) {
        if (parents[x] != x) {
            parents[x] = find(parents[x]);
        }
        return parents[x];
    }

    void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            if (ranks[rootX] > ranks[rootY]) {
                parents[rootY] = rootX;
            } else if (ranks[rootX] < ranks[rootY]) {
                parents[rootX] = rootY;
            } else {
                parents[rootY] = rootX;
                ranks[rootX]++;
            }
        }
    }
};

vector<Interval> mergeIntervals(vector<Interval>& intervals) {
    // Create a union-find data structure
    UnionFind uf;

    // Create a map to store the interval endpoints and their corresponding intervals
    map<int, Interval> endpoints;

    // Add all interval endpoints to the union-find data structure and the map
    for (Interval& interval : intervals) {
        uf.makeSet(interval.start);
        uf.makeSet(interval.end);
        endpoints[interval.start] = interval;
        endpoints[interval.end] = interval;
    }

    // Merge overlapping intervals using the union-find data structure
    for (Interval& interval : intervals) {
        int startRoot = uf.find(interval.start);
        int endRoot = uf.find(interval.end);

        if (startRoot != endRoot) {
            uf.union(startRoot, endRoot);
        }
    }

    // Collect the merged intervals from the endpoints map
    vector<Interval> mergedIntervals;
    for (auto& endpoint : endpoints) {
        int root = uf.find(endpoint.first);

        if (endpoints[root].start == endpoint.first) {
            mergedIntervals.push_back(endpoints[root]);
        }
    }

    return mergedIntervals;
}
```

**Time and Space Complexity Analysis for Approach 4:**
The time complexity of the union-find algorithm is O(n log n), where n is the number of intervals in the array. This is because finding the root of a**Question**: merge-overlapping-sub-intervals/: Problem Statement: Given an array of intervals, merge all the overlapping intervals and return an array of non-overlapping intervals.

**Approach 1: Brute Force**

**Explanation:**
This approach involves iterating through all pairs of intervals and checking if they overlap. If they do, merge them and remove the overlapping intervals from the original array. Repeat the process until there are no more overlapping intervals.

**C++ Code:**
```cpp
vector<Interval> merge(vector<Interval>& intervals) {
  vector<Interval> result;
  for (int i = 0; i < intervals.size(); i++) {
    bool merged = false;
    for (int j = i + 1; j < intervals.size(); j++) {
      if (intervals[i].overlaps(intervals[j])) {
        intervals[i].merge(intervals[j]);
        intervals.erase(intervals.begin() + j);
        j--;
        merged = true;
        break;
      }
    }
    if (!merged) {
      result.push_back(intervals[i]);
    }
  }
  return result;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(n^2), where n is the number of intervals. The outer loop iterates over all intervals, and the inner loop checks for overlaps with all subsequent intervals.
* Space Complexity: O(n), since the result vector can contain up to n merged intervals.

**Approach 2: Sorting and Merging**

**Explanation:**
This approach involves sorting the intervals based on their start times and then iterating through the sorted array. For each interval, check if it overlaps with the previous interval. If it does, merge them and update the previous interval. Keep track of the merged intervals in a result array.

**C++ Code:**
```cpp
vector<Interval> merge(vector<Interval>& intervals) {
  sort(intervals.begin(), intervals.end(), [](Interval& a, Interval& b) { return a.start < b.start; });
  vector<Interval> result;

  for (const auto& interval : intervals) {
    if (result.empty() || result.back().end < interval.start) {
      result.push_back(interval);
    } else {
      result.back().end = max(result.back().end, interval.end);
    }
  }
  return result;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(n log n), where n is the number of intervals. Sorting the intervals takes O(n log n) time, and the merging process takes O(n) time.
* Space Complexity: O(n), since the result vector can contain up to n merged intervals.

**Approach 3: Using a Priority Queue (Min Heap)**

**Explanation:**
This approach involves using a min-heap to store the intervals sorted by their start times. Continuously pop the intervals from the heap and merge them with the previous interval if they overlap. Repeat this process until the heap is empty.

**C++ Code:**
```cpp
vector<Interval> merge(vector<Interval>& intervals) {
  priority_queue<Interval, vector<Interval>, greater<Interval>> minHeap(intervals.begin(), intervals.end());
  vector<Interval> result;

  while (!minHeap.empty()) {
    Interval curr = minHeap.top();
    minHeap.pop();

    if (result.empty() || result.back().end < curr.start) {
      result.push_back(curr);
    } else {
      result.back().end = max(result.back().end, curr.end);
    }
  }
  return result;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(n log n), where n is the number of intervals. Inserting all intervals into the min-heap takes O(n log n) time, and merging the intervals takes O(n) time.
* Space Complexity: O(n), since the min-heap can contain up to n intervals.

**Approach 4: Using a Disjoint Set Union (DSU) Data Structure**

**Explanation:**
This approach involves using a DSU data structure to represent the disjoint intervals. Each interval is represented by a node in the DSU, and they are initially disjoint. As we process the intervals, we merge overlapping intervals by connecting their representative nodes in the DSU. The result will be a set of disjoint sets, each representing a non-overlapping interval.

**C++ Code:**
```cpp
struct DSU {
  vector<int> parent, size;

  DSU(int n) {
    parent.resize(n);
    size.resize(n, 1);
    for (int i = 0; i < n; i++) {
      parent[i] = i;
    }
  }

  int find(int node) {
    if (parent[node] != node) {
      parent[node] = find(parent[node]);
    }
    return parent[node];
  }

  void merge(int a, int b) {
    int rootA = find(a);
    int rootB = find(b);
    if (rootA != rootB) {
      if (size[rootA] > size[rootB]) {
        parent[rootB] = rootA;
        size[rootA] += size[rootB];
      } else {
        parent[rootA] = rootB;
        size[rootB] += size[rootA];
      }
    }
  }
};

vector<Interval> merge(vector<Interval>& intervals) {
  DSU dsu(intervals.size());
  unordered_map<int, int> intervalMap;

  for (int i = 0; i < intervals.size(); i++) {
    intervalMap[intervals[i].start] = i;
    intervalMap[intervals[i].end] = i;
  }

  vector<int> events;
  for (auto [key, value] : intervalMap) {
    events.push_back(key);
  }
  sort(events.begin(), events.end());

  vector<Interval> result;
  for (int event : events) {
    int intervalIdx = intervalMap[event];
    int root = dsu.find(intervalIdx);
    Interval interval = intervals[root];
    if (interval.start > event) {
      interval.start = event;
    }
    if (interval.end < event) {
      interval.end = event;
    }
    result.push_back(interval);
    dsu.merge(intervalIdx, intervalMap[intervals[root].start]);
    dsu.merge(intervalIdx, intervalMap[intervals[root].end]);
  }

  return result;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(n log n), where n is the number of intervals. Creating the DSU, finding and merging intervals, and sorting the events take O(n log n) time.
* Space Complexity: O(n), since the DSU, map, and result vector can all contain up to n elements.