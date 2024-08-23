**Question**: Fractional Knapsack Problem - Greedy Approach: Problem Statement: The weight of N items and their corresponding values are given. We have to put these items in a knapsack of weight W such that the total value obtained is maximized.

**Approach 1: Brute Force**

The brute force approach is to try all possible combinations of items and choose the combination that gives the maximum value. The time complexity of this approach is O(2^N), where N is the number of items, which is exponential and impractical for large values of N.

**Approach 2: Optimized Approach using Maps**

We can use a map to store the ratio of value to weight for each item. We then sort the items in decreasing order of this ratio. We start adding items to the knapsack in this order until the knapsack is full. 

**C++ Code for Approach 2(Optimized Approach using Maps):**

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<double, int> Item;

bool compare(Item a, Item b) {
    return (a.first > b.first);
}

double fractionalKnapsack(int W, vector<int> wt, vector<int> val, int n) {
    vector<Item> items;
    for (int i = 0; i < n; i++) {
        items.push_back({(double)val[i] / wt[i], i}); // Store item value / weight ratio
    }
    sort(items.begin(), items.end(), compare); // Sort items by decreasing value / weight ratio
    
    double totalValue = 0.0;
    int currentWeight = 0;
    for (auto &item : items) {
        int index = item.second;
        double weight = wt[index];
        double value = val[index];
        
        if (currentWeight + weight <= W) {
            totalValue += value;
            currentWeight += weight;
        } else {
            double fraction = (W - currentWeight) / weight;
            totalValue += fraction * value;
            break;
        }
    }
    return totalValue;
}
```

**Time and Space Complexity Analysis for Approach 2**: The time complexity of this approach is O(N log N) for sorting the items and O(N) for iterating through them, resulting in an overall complexity of O(N log N). The space complexity is O(N) for storing the items in the map.

**Approach 3: Greedy Algorithm**

The greedy algorithm for this problem involves selecting the item with the highest value to weight ratio and adding it to the knapsack until the knapsack is full. If the item's weight exceeds the remaining capacity of the knapsack, we add a fraction of the item to the knapsack.

**C++ Code for Approach 3 (Greedy Algorithm):**

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<double, int> Item;

bool compare(Item a, Item b) {
    return (a.first > b.first);
}

double fractionalKnapsack(int W, vector<int> wt, vector<int> val, int n) {
    vector<Item> items;
    for (int i = 0; i < n; i++) {
        items.push_back({(double)val[i] / wt[i], i}); // Store item value / weight ratio
    }
    sort(items.begin(), items.end(), compare); // Sort items by decreasing value / weight ratio
    
    double totalValue = 0.0;
    int currentWeight = 0;
    for (auto &item : items) {
        int index = item.second;
        double weight = wt[index];
        double value = val[index];
        
        if (currentWeight + weight <= W) {
            totalValue += value;
            currentWeight += weight;
        } else {
            double fraction = (W - currentWeight) / weight;
            totalValue += fraction * value;
            break;
        }
    }
    return totalValue;
}
```

**Time and Space Complexity Analysis for Approach 3**: The time complexity of the greedy algorithm is the same as that of Approach 2, which is O(N log N) for sorting the items and O(N) for iterating through them. The space complexity is also O(N) for storing the items in the vector.

**Approach 4: Recursive Approach**

The recursive approach for this problem involves recursively calling the function with different weights and checking if the current weight exceeds the knapsack capacity.

**C++ Code for Approach 4 (Recursive Approach):**

```cpp
#include <bits/stdc++.h>
using namespace std;

double fractionalKnapsack(int W, vector<int> wt, vector<int> val, int n, int currentWeight, double currentValue) {
    if (n == 0 || currentWeight >= W) {
        return currentValue;
    }
    
    double withoutItem = fractionalKnapsack(W, wt, val, n - 1, currentWeight, currentValue);
    double withItem = -1.0;
    if (currentWeight + wt[n - 1] <= W) {
        withItem = fractionalKnapsack(W, wt, val, n - 1, currentWeight + wt[n - 1], currentValue + val[n - 1]);
    } else {
        double fraction = (W - currentWeight) / wt[n - 1];
        withItem = fractionalKnapsack(W, wt, val, n - 1, W, currentValue + fraction * val[n - 1]);
    }
    
    return max(withoutItem, withItem);
}
```

**Time and Space Complexity Analysis for Approach 4**: The time complexity of the recursive approach is exponential, O(2^N), as it recursively explores all possible combinations of items. The space complexity is O(N) for the recursion stack.

**Approach 5: Backtracking Approach**

The backtracking approach for this problem involves iteratively trying different combinations of items and keeping track of the best combination found so far.

**C++ Code for Approach 5 (Backtracking Approach):**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Item {
    int weight;
    int value;
};

double fractionalKnapsack(int W, vector<Item> items, int n) {
    double maxValue = 0.0;
    vector<bool> taken(n, false); // Track which items are taken
    
    function<void(int, int, double)> backtrack = [&](int currentWeight, int currentIndex, double currentValue) {
        if (currentIndex == n) {
            maxValue = max(maxValue, currentValue);
            return;
        }
        
        backtrack(currentWeight, currentIndex + 1, currentValue); // Skip current item
        
        if (currentWeight + items[currentIndex].weight <= W) {
            backtrack(currentWeight + items[currentIndex].weight, currentIndex + 1, currentValue + items[currentIndex].value); // Take current item
        } else {
            double fraction = (W - currentWeight) / items[currentIndex].weight;
            backtrack(W, currentIndex + 1, currentValue + fraction * items[currentIndex].value); // Take a fraction of the current item
        }
    };
    
    backtrack(0, 0, 0.0);
    return maxValue;
}
```

**Time and Space Complexity Analysis for Approach 5**: The time complexity of the backtracking approach is exponential, O(2^N), as it explores all possible combinations of items. The space complexity is O(N) for the recursion stack and O(N) for the taken array.**Question**: Fractional-Knapsack-Problem-Greedy-Approach
**Problem Statement**: The weight of N items and their corresponding values are given. We have to put these items in a knapsack of weight W such that the total value obtained is maximized.

**Approach 1: Naive/Brute Force Approach**
The most straightforward solution to the problem is to try all possible combinations of items and choose the one that results in the maximum total value. Here's a brute-force approach:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

using namespace std;

struct Item {
  int weight;
  int value;
};

double fractionalKnapsack(vector<Item> &items, int W) {
  int N = items.size(); 

  double maxValue = 0;

  // Iterate over all possible subsets of items
  for (int i = 0; i < (1 << N); i++) {
    double totalWeight = 0;
    double totalValue = 0;

    // Check if the current subset's total weight is less than or equal to the knapsack capacity
    for (int j = 0; j < N; j++) {
      if ((i & (1 << j)) > 0) {
        totalWeight += items[j].weight;
        totalValue += items[j].value;
      }
    }

    if (totalWeight <= W) {
      maxValue = max(maxValue, totalValue);
    }
  }

  return maxValue;
}

int main() {
  int N, W;
  cin >> N >> W;

  vector<Item> items(N);
  for (int i = 0; i < N; i++) {
    cin >> items[i].weight >> items[i].value;
  }

  double maxValue = fractionalKnapsack(items, W);
  cout << maxValue << endl;

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:
- **Time Complexity**: O(2^N), where N is the number of items. This is because we are trying all possible combinations of items.
- **Space Complexity**: O(N), for storing the items.

**Approach 2: Greedy Approach**
The greedy approach involves selecting the item with the highest value-to-weight ratio at each step and adding it to the knapsack until the knapsack is full or no more items are available. Here's a greedy approach:

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

using namespace std;

struct Item {
  int weight;
  int value;
  double valuePerWeight;
};

bool compareItems(Item &a, Item &b) {
  return a.valuePerWeight > b.valuePerWeight;
}

double fractionalKnapsack(vector<Item> &items, int W) {
  int N = items.size();

  // Sort items in decreasing order of value per weight
  sort(items.begin(), items.end(), compareItems);

  double totalWeight = 0;
  double totalValue = 0;

  // Iterate over the sorted items
  for (int i = 0; i < N; i++) {
    // If the current item's weight is less than or equal to the remaining capacity of the knapsack
    if (totalWeight + items[i].weight <= W) {
      // Add the entire item to the knapsack and update the total weight and value
      totalWeight += items[i].weight;
      totalValue += items[i].value;
    } else {
      // Add a fraction of the current item to the knapsack
      double remainingCapacity = W - totalWeight;
      double fraction = remainingCapacity / items[i].weight;
      totalWeight += items[i].weight * fraction;
      totalValue += items[i].value * fraction;
      break;
    }
  }

  return totalValue;
}

int main() {
  int N, W;
  cin >> N >> W;

  vector<Item> items(N);
  for (int i = 0; i < N; i++) {
    cin >> items[i].weight >> items[i].value;
    items[i].valuePerWeight = (double)items[i].value / items[i].weight;
  }

  double maxValue = fractionalKnapsack(items, W);
  cout << maxValue << endl;

  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:
- **Time Complexity**: O(N * logN), where N is the number of items, due to the sorting.
- **Space Complexity**: O(N), for storing the items.