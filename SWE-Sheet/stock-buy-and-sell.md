**Question**: "stock-buy-and-sell/: Problem Statement: You are given an array of prices where prices[i] is the price of a given stock on an ith day."

**Approach 1: Brute Force**

**Explanation**: The brute force approach involves iterating through the array and comparing each element with every other element to find the maximum profit that can be obtained by buying and selling the stock.

**Brute Force Code**:
```cpp
int maxProfit(vector<int>& prices) {
    int max_profit = 0;
    for (int i = 0; i < prices.size() - 1; i++) {
        for (int j = i + 1; j < prices.size(); j++) {
            if (prices[j] - prices[i] > max_profit) {
                max_profit = prices[j] - prices[i];
            }
        }
    }
    return max_profit;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(n^2), where n is the length of the prices array. The space complexity is O(1).

**Approach 2: Optimized Approach using Two Pointers**

**Explanation**: The two pointers approach involves using two pointers, one to track the minimum price encountered so far, and the other to track the current price. The profit is calculated as the difference between the current price and the minimum price encountered so far.

**Two Pointers Code**:
```cpp
int maxProfit(vector<int>& prices) {
    int min_price = INT_MAX;
    int max_profit = 0;
    for (int i = 0; i < prices.size(); i++) {
        if (prices[i] < min_price) {
            min_price = prices[i];
        } else if (prices[i] - min_price > max_profit) {
            max_profit = prices[i] - min_price;
        }
    }
    return max_profit;
}
```

**Time and Space Complexity Analysis**: The time complexity of this approach is O(n), where n is the length of the prices array. The space complexity is O(1).

**Additional Approaches**:

* **Optimized Approach using Dynamic Programming**: This approach uses dynamic programming to store the maximum profit that can be obtained at each index. The time complexity of this approach is O(n) and the space complexity is O(n).
* **Optimized Approach using Kadane's Algorithm**: This approach uses Kadane's algorithm to find the maximum subarray sum. The time complexity of this approach is O(n) and the space complexity is O(1).
* **Greedy Approach**: This approach involves buying the stock at any price and selling it at a higher price. The time complexity of this approach is O(n) and the space complexity is O(1).**Question**: "stock-buy-and-sell/: Problem Statement: You are given an array of prices where `prices[i]` is the price of a given stock on an `i`th day."

**Approach 1: Brute Force**

**Explanation**: This approach checks all possible pairs of buying and selling days to find the maximum profit. It has a time complexity of O(N^2) and a space complexity of O(1).

**Approach 1 Code**:

```cpp
int max_profit(int prices[]) {
  int n = sizeof(prices) / sizeof(int);
  int max_profit = 0;
  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      int profit = prices[j] - prices[i];
      if (profit > max_profit) {
        max_profit = profit;
      }
    }
  }
  return max_profit;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time Complexity**: O(N^2) - The algorithm considers all possible pairs of buying and selling days, resulting in a time complexity of O(N^2).
* **Space Complexity**: O(1) - Constant space is required to store the variables `i`, `j`, `profit`, and `max_profit`.

**Approach 2: One Pass**

**Explanation**: This approach iterates over the array once to find the maximum profit. It keeps track of the minimum price seen so far and the maximum profit that could be obtained by selling the stock on the current day. It has a time complexity of O(N) and a space complexity of O(1).

**Approach 2 Code**:

```cpp
int max_profit(int prices[]) {
  int min_price = INT_MAX;
  int max_profit = 0;
  for (int i = 0; i < n; i++) {
    if (prices[i] < min_price) {
      min_price = prices[i];
    } else if (prices[i] - min_price > max_profit) {
      max_profit = prices[i] - min_price;
    }
  }
  return max_profit;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time Complexity**: O(N) - The algorithm iterates over the input array once, resulting in a time complexity of O(N).
* **Space Complexity**: O(1) - Constant space is required to store the variables `min_price` and `max_profit`.