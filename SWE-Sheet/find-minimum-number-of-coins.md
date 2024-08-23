## Question: find-minimum-number-of-coins/
Problem Statement: Given a value V, if we want to make a change for V Rs, and we have an infinite supply of each of the denominations in Indian currency, i.e., we have an infinite supply of { 1, 2, 5, 10, 20, 50, 100, 500, 1000} valued coins/notes, what is the minimum number of coins and/or notes needed to make the change.

### Approach 1: Brute Force
**Explanation:**
This approach involves generating all possible combinations of coins and selecting the one with the minimum number of coins.

**Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(int V) {
  vector<int> coins = {1, 2, 5, 10, 20, 50, 100, 500, 1000};
  int min = INT_MAX;

  for (int i = 0; i < (1 << coins.size()); i++) {
    int sum = 0;
    int count = 0;
    for (int j = 0; j < coins.size(); j++) {
      if (i & (1 << j)) {
        sum += coins[j];
        count++;
      }
    }

    if (sum == V && count < min) {
      min = count;
    }
  }

  return min == INT_MAX ? -1 : min;
}

int main() {
  int V;
  cout << "Enter the value V: ";
  cin >> V;

  cout << "Minimum number of coins: " << minCoins(V) << endl;

  return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(2^n), where n is the number of coin denominations.
* Space Complexity: O(n), to store the current combination of coins.

### Approach 2: Optimized Approaches using Maps, Multisets, Binary Search, Two Pointers
**Explanation:**
This approach uses a multiset to keep track of the remaining amount and the number of coins used for each denomination. It iterates through the denominations in decreasing order and tries to use the highest denomination possible for the remaining amount.

**Code:**
```cpp
#include <iostream>
#include <map>

using namespace std;

int minCoins(int V) {
  map<int, int> coins;
  int denominations[] = {1, 2, 5, 10, 20, 50, 100, 500, 1000};

  for (int i = 8; i >= 0; i--) {
    while (V >= denominations[i]) {
      V -= denominations[i];
      coins[denominations[i]]++;
    }
  }

  if (V == 0) {
    int count = 0;
    for (auto coin : coins) {
      count += coin.second;
    }
    return count;
  }

  return -1;
}

int main() {
  int V;
  cout << "Enter the value V: ";
  cin >> V;

  cout << "Minimum number of coins: " << minCoins(V) << endl;

  return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(n), where n is the number of coin denominations.
* Space Complexity: O(n), to store the counts of each denomination.

### Approach 3: Greedy Algorithms
**Explanation:**
This approach uses a greedy algorithm to select the largest denomination possible at each step. It iterates through the denominations in decreasing order and subtracts the largest possible denomination from the remaining amount until the amount becomes zero.

**Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(int V) {
  vector<int> coins = {1, 2, 5, 10, 20, 50, 100, 500, 1000};
  int count = 0;

  for (int i = 8; i >= 0; i--) {
    while (V >= coins[i]) {
      V -= coins[i];
      count++;
    }
  }

  return V == 0 ? count : -1;
}

int main() {
  int V;
  cout << "Enter the value V: ";
  cin >> V;

  cout << "Minimum number of coins: " << minCoins(V) << endl;

  return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(n), where n is the number of coin denominations.
* Space Complexity: O(1), as a constant amount of space is used.

### Approach 4: Recursive
**Explanation:**
This approach uses a recursive function to explore all possible combinations of coins. It starts with the largest denomination and tries to use it as many times as possible. If the remaining amount is not divisible by the current denomination, it moves to the next smaller denomination.

**Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(vector<int> coins, int V, int index) {
  if (index >= coins.size() || V == 0) {
    return V == 0 ? 0 : INT_MAX;
  }

  int min = INT_MAX;
  for (int i = 0; i * coins[index] <= V; i++) {
    int sub_result = minCoins(coins, V - i * coins[index], index + 1);
    if (sub_result != INT_MAX) {
      min = min(min, i + sub_result);
    }
  }

  return min;
}

int main() {
  int V;
  cout << "Enter the value V: ";
  cin >> V;

  vector<int> coins = {1, 2, 5, 10, 20, 50, 100, 500, 1000};

  int result = minCoins(coins, V, 0);
  cout << "Minimum number of coins: " << result << endl;

  return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(2^n), where n is the number of coin denominations.
* Space Complexity: O(n), to store the recursion stack.

### Approach 5: Backtracking
**Explanation:**
This approach uses backtracking to explore all possible combinations of coins. It starts with the largest denomination and tries to use it as many times as possible. If the remaining amount is not divisible by the current denomination, it moves to the next smaller denomination and tries different combinations of coins for that denomination.

**Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(vector<int> coins, int V) {
  int n = coins.size();
  vector<int> result(n, 0);
  int min = INT_MAX;

  minCoins_helper(coins, V, result, 0, min);

  return min == INT_MAX ? -1 : min;
}

void minCoins_helper(vector<int> coins, int V, vector<int>& result, int index, int& min) {
  if (index >= coins.size() || V == 0) {
    if (V == 0) {
      int count = 0;
      for (int c : result) {
        count += c;
      }
      min = min(min, count);
    }
    return;
  }

  for (int i = 0; i * coins[index] <= V; i++) {
    result[index] = i;
    minCoins_helper(coins, V - i * coins[index], result, index + 1, min);
  }
}

int main() {
  int V;
  cout << "Enter the value V: ";
  cin >> V;

  vector<int> coins = {1, 2, 5, 10, 20, 50, 100, 500, 1000};

  int result = minCoins(coins, V);
  cout << "Minimum number of coins: " << result << endl;

  return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(2^n), where n is the number of coin denominations.
* Space Complexity: O(n), to store the recursion stack and the result vector.**Question**: find-minimum-number-of-coins/: Problem Statement: Given a value V, if we want to make a change for V Rs, and we have an infinite supply of each of the denominations in Indian currency, i.e., we have an infinite supply of { 1, 2, 5, 10, 20, 50, 100, 500, 1000} valued coins/notes, what is the minimum number of coins and/or notes needed to make the change.

**Approach 1: Brute Force**

**Explanation:** This approach involves generating all possible combinations of coins that add up to the given value V and selecting the combination with the minimum number of coins.

**C++ Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(int V) {
    // Initialize the minimum number of coins to a large value
    int min_coins = INT_MAX;

    // Generate all possible combinations of coins
    for (int i = 1; i <= V; i++) {
        for (int j = 1; j <= V; j++) {
            for (int k = 1; k <= V; k++) {
                if (i + j + k == V) {
                    // Update the minimum number of coins if the current combination has fewer coins
                    min_coins = min(min_coins, i + j + k);
                }
            }
        }
    }

    return min_coins;
}

int main() {
    int V;
    cout << "Enter the value V: ";
    cin >> V;

    int min_coins = minCoins(V);

    if (min_coins != INT_MAX) {
        cout << "The minimum number of coins is: " << min_coins << endl;
    } else {
        cout << "It is not possible to make change for the given value." << endl;
    }

    return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(V^3).
* Space Complexity: O(1).

**Approach 2: Greedy**

**Explanation:** This approach involves selecting the largest denomination coin that is less than or equal to the remaining amount and repeating the process until the remaining amount is zero.

**C++ Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(int V) {
    // Initialize the minimum number of coins to zero
    int min_coins = 0;

    // Denominations in descending order
    vector<int> denominations = {1000, 500, 100, 50, 20, 10, 5, 2, 1};

    // Iterate through the denominations
    for (int i = 0; i < denominations.size(); i++) {
        // While the remaining amount is greater than or equal to the current denomination
        while (V >= denominations[i]) {
            // Add the current denomination to the minimum number of coins
            min_coins++;

            // Subtract the current denomination from the remaining amount
            V -= denominations[i];
        }
    }

    return min_coins;
}

int main() {
    int V;
    cout << "Enter the value V: ";
    cin >> V;

    int min_coins = minCoins(V);

    if (min_coins != INT_MAX) {
        cout << "The minimum number of coins is: " << min_coins << endl;
    } else {
        cout << "It is not possible to make change for the given value." << endl;
    }

    return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(N), where N is the number of denominations.
* Space Complexity: O(1).

**Approach 3: Dynamic Programming**

**Explanation:** This approach involves creating a table where each cell represents the minimum number of coins required to make change for a given amount. The table is filled bottom-up, and the final cell contains the minimum number of coins required for the given value V.

**C++ Code:**
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minCoins(int V) {
    // Initialize the table to store the minimum number of coins
    vector<int> table(V + 1, INT_MAX);

    // Set the minimum number of coins for 0 to 0
    table[0] = 0;

    // Denominations in descending order
    vector<int> denominations = {1000, 500, 100, 50, 20, 10, 5, 2, 1};

    // Iterate through the denominations
    for (int i = 1; i <= V; i++) {
        // Iterate through the denominations
        for (int j = 0; j < denominations.size(); j++) {
            // If the current denomination is less than or equal to the remaining amount
            if (denominations[j] <= i) {
                // Update the minimum number of coins for the remaining amount
                table[i] = min(table[i], table[i - denominations[j]] + 1);
            }
        }
    }

    return table[V];
}

int main() {
    int V;
    cout << "Enter the value V: ";
    cin >> V;

    int min_coins = minCoins(V);

    if (min_coins != INT_MAX) {
        cout << "The minimum number of coins is: " << min_coins << endl;
    } else {
        cout << "It is not possible to make change for the given value." << endl;
    }

    return 0;
}
```

**Time and Space Complexity Analysis:**
* Time Complexity: O(V * N), where V is the given value and N is the number of denominations.
* Space Complexity: O(V).