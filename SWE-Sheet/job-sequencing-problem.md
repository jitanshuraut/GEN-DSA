**Question**: **Job Sequencing Problem**
**Problem Statement**: You are given a set of N jobs where each job comes with a deadline and profit. The profit can only be earned upon completing the job within its deadline. Find the number of jobs done and the maximum profit that can be obtained. Each job takes a single unit of time and only one job can be performed at a time.

## **Approach 1: Brute Force**

**Explanation**: A brute-force approach would be to try all possible combinations of jobs and check if they can be completed within their deadlines. The combination that yields the maximum profit is the optimal solution.

**Approach 1 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxProfit(vector<pair<int, int>> jobs, int n) {
    int max_profit = 0;
    vector<bool> visited(n, false);

    // Try all possible combinations of jobs
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            int profit = jobs[i].second;
            int deadline = jobs[i].first;
            visited[i] = true;

            // Check if the current job can be scheduled
            for (int j = i + 1; j < n; j++) {
                if (!visited[j] && deadline > jobs[j].first) {
                    profit += jobs[j].second;
                    deadline = jobs[j].first;
                    visited[j] = true;
                }
            }

            max_profit = max(max_profit, profit);
        }
    }

    return max_profit;
}

int main() {
    int n;
    cin >> n;
    vector<pair<int, int>> jobs(n);

    for (int i = 0; i < n; i++) {
        int deadline, profit;
        cin >> deadline >> profit;
        jobs[i] = {deadline, profit};
    }

    cout << maxProfit(jobs, n) << endl;
    return 0;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(2^n), where n is the number of jobs. The space complexity is O(n).

## **Approach 2: Optimized Approach using Maps**

**Explanation**: Instead of trying all possible combinations, we can use a map to store the jobs sorted by their deadlines. This allows us to quickly find the next job that can be scheduled within a given deadline.

**Approach 2 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxProfit(vector<pair<int, int>> jobs, int n) {
    map<int, int> jobMap;

    // Sort the jobs by their deadlines
    sort(jobs.begin(), jobs.end());

    // Initialize the maximum profit
    int max_profit = 0;

    // Iterate over the jobs
    for (auto job : jobs) {
        int deadline = job.first;
        int profit = job.second;

        // Find the next available time slot
        auto it = jobMap.upper_bound(deadline);

        // If a time slot is available, schedule the job
        if (it != jobMap.begin()) {
            it--;
            max_profit += profit;
            jobMap[deadline] = profit;
        }
    }

    return max_profit;
}

int main() {
    int n;
    cin >> n;
    vector<pair<int, int>> jobs(n);

    for (int i = 0; i < n; i++) {
        int deadline, profit;
        cin >> deadline >> profit;
        jobs[i] = {deadline, profit};
    }

    cout << maxProfit(jobs, n) << endl;
    return 0;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(n log n). The space complexity is O(n).

## **Approach 3: Optimized Approach using Multisets**

**Explanation**: Similar to the previous approach, we can use a multiset to store the jobs sorted by their profits. This allows us to quickly find the job with the highest profit that can be scheduled within a given deadline.

**Approach 3 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxProfit(vector<pair<int, int>> jobs, int n) {
    multiset<int> profitSet;

    // Initialize the maximum profit
    int max_profit = 0;

    // Iterate over the jobs
    for (auto job : jobs) {
        int deadline = job.first;
        int profit = job.second;

        // Find the next available time slot
        auto it = profitSet.upper_bound(deadline);

        // If a time slot is available, schedule the job
        if (it != profitSet.begin()) {
            it--;
            max_profit += profit;
            profitSet.erase(it);
            profitSet.insert(profit);
        } else {
            profitSet.insert(profit);
        }
    }

    return max_profit;
}

int main() {
    int n;
    cin >> n;
    vector<pair<int, int>> jobs(n);

    for (int i = 0; i < n; i++) {
        int deadline, profit;
        cin >> deadline >> profit;
        jobs[i] = {deadline, profit};
    }

    cout << maxProfit(jobs, n) << endl;
    return 0;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(n log n). The space complexity is O(n).

## **Approach 4: Optimized Approach using Binary Search**

**Explanation**: We can use binary search to find the latest job that can be scheduled within a given deadline. This allows us to reduce the search time from O(n) to O(log n) per job.

**Approach 4 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxProfit(vector<pair<int, int>> jobs, int n) {
    sort(jobs.begin(), jobs.end());

    // Initialize the maximum profit
    int max_profit = 0;

    // Iterate over the jobs
    for (auto job : jobs) {
        int deadline = job.first;
        int profit = job.second;

        // Find the latest job that can be scheduled within the deadline
        int left = 0;
        int right = deadline - 1;
        int latest_job = -1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (jobs[mid].first <= deadline) {
                latest_job = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        // If a job was found, schedule it
        if (latest_job != -1) {
            max_profit += profit;
        }
    }

    return max_profit;
}

int main() {
    int n;
    cin >> n;
    vector<pair<int, int>> jobs(n);

    for (int i = 0; i < n; i++) {
        int deadline, profit;
        cin >> deadline >> profit;
        jobs[i] = {deadline, profit};
    }

    cout << maxProfit(jobs, n) << endl;
    return 0;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(n log n). The space complexity is O(n).

## **Approach 5: Optimized Approach using Two Pointers**

**Explanation**: We can use two pointers to track the current job and the next available time slot. This allows us to reduce the search time from O(n^2) to O(n).

**Approach 5 Code**:

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxProfit(vector<pair<int, int>> jobs, int n) {
    sort(jobs.begin(), jobs.end());

    // Initialize the maximum profit and the pointers
    int max_profit = 0;
    int current_job = 0;
    int next_slot = 0;

    // Iterate until all jobs are scheduled
    while (current_job < n) {
        // Find the next available time slot
        while (next_slot < n && jobs[next_slot].first <= current_job) {
            next_slot++;
        }

        // If a time slot is available, schedule the job
        if (next_slot < n) {
            max_profit += jobs[next_slot].second;
            current_job++;
            next_slot++;
        } else {
            current_job++;
        }
    }## Question
**job-sequencing-problem**: Problem Statement: You are given a set of N jobs where each job comes with a deadline and profit. The profit can only be earned upon completing the job within its deadline. Find the number of jobs done and the maximum profit that can be obtained. Each job takes a single unit of time and only one job can be performed at a time.

## Approach 1: Sorting
**Explanation:** Sort the jobs in decreasing order of profit. Then, iterate through the sorted jobs and assign them to the earliest available time slot. If a time slot is already occupied, move on to the next job.

**Approach 1 Code:**
```cpp
#include<iostream>
#include<vector>
#include<algorithm>

using namespace std;

struct Job {
    int profit;
    int deadline;
};

bool compareProfit(Job a, Job b) {
    return a.profit > b.profit;
}

int jobSequencing(vector<Job> jobs, int n) {
    sort(jobs.begin(), jobs.end(), compareProfit);

    int maxProfit = 0;
    int timeSlots[n] = {0};

    for (int i = 0; i < n; i++) {
        for (int j = min(jobs[i].deadline - 1, n - 1); j >= 0; j--) {
            if (timeSlots[j] == 0) {
                timeSlots[j] = 1;
                maxProfit += jobs[i].profit;
                break;
            }
        }
    }

    return maxProfit;
}

int main() {
    int n;
    cin >> n;

    vector<Job> jobs(n);
    for (int i = 0; i < n; i++) {
        cin >> jobs[i].profit >> jobs[i].deadline;
    }

    cout << jobSequencing(jobs, n) << endl;

    return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(N log N), where N is the number of jobs.
* Space Complexity: O(N), as we need an array to store the time slots.

## Approach 2: Priority Queue
**Explanation:** Use a priority queue to store the jobs in decreasing order of profit. Then, iterate through the jobs and assign them to the earliest available time slot. If a time slot is already occupied, move on to the next job.

**Approach 2 Code:**
```cpp
#include<iostream>
#include<vector>
#include<queue>

using namespace std;

struct Job {
    int profit;
    int deadline;
};

struct compareProfit {
    bool operator() (Job a, Job b) {
        return a.profit < b.profit;
    }
};

int jobSequencing(vector<Job> jobs, int n) {
    priority_queue<Job, vector<Job>, compareProfit> pq;

    for (int i = 0; i < n; i++) {
        pq.push(jobs[i]);
    }

    int maxProfit = 0;
    int timeSlots[n] = {0};

    while (!pq.empty()) {
        Job job = pq.top();
        pq.pop();

        for (int j = min(job.deadline - 1, n - 1); j >= 0; j--) {
            if (timeSlots[j] == 0) {
                timeSlots[j] = 1;
                maxProfit += job.profit;
                break;
            }
        }
    }

    return maxProfit;
}

int main() {
    int n;
    cin >> n;

    vector<Job> jobs(n);
    for (int i = 0; i < n; i++) {
        cin >> jobs[i].profit >> jobs[i].deadline;
    }

    cout << jobSequencing(jobs, n) << endl;

    return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(N log N), where N is the number of jobs.
* Space Complexity: O(N), as we need a priority queue to store the jobs.

## Other Approaches:
There are other approaches to solve this problem, but the above two approaches are the most efficient and commonly used.