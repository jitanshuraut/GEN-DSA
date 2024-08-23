**Question**: combination-sum-ii-find-all-unique-combinations/: Problem Statement: Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target. Each number in candidates may only be used once in the combination.

**Approach 1: Brute Force**

**Explanation:** A brute-force approach involves recursively generating all possible combinations of candidates and checking if their sum equals the target. If the sum matches the target, the combination is added to the result set. This approach explores all possible combinations, resulting in an exponential time complexity.

**Approach 1 Code:**
```cpp
void backtrack(vector<int>& candidates, int target, vector<int>& combination, vector<vector<int>>& result) {
  if (target == 0) {
    result.push_back(combination);
    return;
  }
  for (int i = 0; i < candidates.size(); i++) {
    if (i > 0 && candidates[i] == candidates[i - 1]) continue;  // Skip duplicates
    if (candidates[i] <= target) {
      combination.push_back(candidates[i]);
      backtrack(candidates, target - candidates[i], combination, result);
      combination.pop_back();
    }
  }
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
  sort(candidates.begin(), candidates.end());  // Sort to skip duplicates
  vector<vector<int>> result;
  vector<int> combination;
  backtrack(candidates, target, combination, result);
  return result;
}
```

**Time and Space Complexity Analysis for Approach 1:**

* **Time Complexity**: O(2^n), where n is the number of candidates.
* **Space Complexity**: O(n), as the call stack can grow up to n levels.

**Approach 2: Optimized Using Maps**

**Explanation:** This approach optimizes the brute-force approach by using a map to keep track of the remaining target and the combinations that lead to that target. It avoids revisiting the same combinations and significantly reduces the number of recursive calls.

**Approach 2 Code:**
```cpp
void backtrack(unordered_map<int, vector<vector<int>>>& target_combinations, vector<int>& candidates, int target, vector<int>& combination) {
  if (target == 0) {
    target_combinations[target].push_back(combination);
    return;
  }
  for (int i = 0; i < candidates.size(); i++) {
    if (candidates[i] <= target) {
      combination.push_back(candidates[i]);
      backtrack(target_combinations, candidates, target - candidates[i], combination);
      combination.pop_back();
    }
  }
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
  unordered_map<int, vector<vector<int>>> target_combinations;
  vector<int> combination;
  backtrack(target_combinations, candidates, target, combination);
  return target_combinations[target];
}
```

**Time and Space Complexity Analysis for Approach 2:**

* **Time Complexity**: O(n^2), where n is the number of candidates.
* **Space Complexity**: O(n^2), as the number of combinations can grow quadratically with the number of candidates.

**Approach 3: Optimized Using Multisets**

**Explanation:** This approach uses a multiset to keep track of the remaining candidates as it explores different combinations. Multisets allow the storage of duplicate elements, which is necessary when considering the uniqueness of combinations in this problem.

**Approach 3 Code:**
```cpp
void backtrack(multiset<int>& candidates, int target, vector<int>& combination, vector<vector<int>>& result) {
  if (target == 0) {
    result.push_back(combination);
    return;
  }
  for (auto it = candidates.begin(); it != candidates.end(); it++) {
    if (*it <= target) {
      candidates.erase(it);
      combination.push_back(*it);
      backtrack(candidates, target - *it, combination, result);
      combination.pop_back();
      it = candidates.insert(it);
    }
  }
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
  multiset<int> candidates_set(candidates.begin(), candidates.end());
  vector<vector<int>> result;
  vector<int> combination;
  backtrack(candidates_set, target, combination, result);
  return result;
}
```

**Time and Space Complexity Analysis for Approach 3:**

* **Time Complexity**: O(n^2), where n is the number of candidates.
* **Space Complexity**: O(n), as the multiset stores the candidates.

**Approach 4: Optimized Using Binary Search**

**Explanation:** This approach utilizes binary search to efficiently find candidate numbers that sum up to the target. It eliminates the need to iterate through all combinations, reducing the time complexity significantly.

**Approach 4 Code:**
```cpp
bool binarySearch(vector<int>& candidates, int left, int right, int target) {
  while (left <= right) {
    int mid = (left + right) / 2;
    if (candidates[mid] == target) {
      return true;
    } else if (candidates[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return false;
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
  sort(candidates.begin(), candidates.end());
  vector<vector<int>> result;
  vector<int> combination;
  for (int i = 0; i < candidates.size(); i++) {
    if (i > 0 && candidates[i] == candidates[i - 1]) continue;  // Skip duplicates
    if (binarySearch(candidates, i + 1, candidates.size() - 1, target - candidates[i])) {
      combination.push_back(candidates[i]);
      backtrack(candidates, target - candidates[i], combination, result);
      combination.pop_back();
    }
  }
  return result;
}
```

**Time and Space Complexity Analysis for Approach 4:**

* **Time Complexity**: O(n log n), where n is the number of candidates.
* **Space Complexity**: O(n), as the call stack can grow up to n levels.

**Approach 5: Optimized Using Two Pointers**

**Explanation:** This approach uses two pointers to navigate through the sorted candidate array while maintaining the sum of the combination. It effectively narrows down the search space, reducing the time complexity.

**Approach 5 Code:**
```cpp
vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
  sort(candidates.begin(), candidates.end());
  vector<vector<int>> result;
  vector<int> combination;
  int left = 0, right = candidates.size() - 1;
  while (left < right) {
    int sum = candidates[left] + candidates[right];
    if (sum == target) {
      combination.push_back(candidates[left]);
      combination.push_back(candidates[right]);
      result.push_back(combination);
      combination.clear();
      left++;
      while (left < right && candidates[left] == candidates[left - 1]) left++;  // Skip duplicates
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }
  return result;
}
```

**Time and Space Complexity Analysis for Approach 5:**

* **Time Complexity**: O(n log n), where n is the number of candidates.
* **Space Complexity**: O(n), as the call stack can grow up to n levels.**Question**: combination-sum-ii-find-all-unique-combinations/: Problem Statement: Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target. Each number in candidates may only be used once in the combination.

## Approach 1: Recursion + Backtracking
**Explanation**: This approach utilizes recursion and backtracking to explore all possible combinations. It recursively generates combinations, checking if the current combination sums to the target. If not, it backtracks and tries other combinations.

**C++ Code**:
```cpp
class Solution {
private:
    vector<vector<int>> combinations;
    vector<int> currentCombination;
    
    void backtrack(vector<int>& candidates, int target, int start) {
        if (target == 0) {
            combinations.push_back(currentCombination);
            return;
        }
        if (target < 0) {
            return;
        }
        for (int i = start; i < candidates.size(); i++) {
            if (i > start && candidates[i] == candidates[i - 1]) {
                continue;
            }
            currentCombination.push_back(candidates[i]);
            backtrack(candidates, target - candidates[i], i + 1);
            currentCombination.pop_back();
        }
    }
    
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        backtrack(candidates, target, 0);
        return combinations;
    }
};
```

**Time and Space Complexity Analysis**:
* **Time Complexity:** O(2^N), where N is the number of candidates. Each candidate can either be included or excluded, resulting in an exponential number of combinations.
* **Space Complexity:** O(N), as the recursion stack can store up to N elements of the current combination.

## Approach 2: Dynamic Programming
**Explanation**: This approach leverages dynamic programming to avoid redundant computations. It initializes a 2D array, where each cell represents the number of ways to reach a particular target using a subset of candidates. The optimal solution is then obtained by traversing the array.

**C++ Code**:
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        int n = candidates.size();
        
        // Create a 2D table to store the number of combinations to reach each target
        vector<vector<int>> dp(target + 1, vector<int>(n + 1, 0));
        
        // Initialize the base case (target = 0)
        for (int i = 0; i <= n; i++) {
            dp[0][i] = 1;
        }
        
        // Iterate over the candidates and targets
        for (int i = 1; i <= target; i++) {
            for (int j = 1; j <= n; j++) {
                // Try including and excluding the current candidate
                dp[i][j] = dp[i][j - 1];
                if (i - candidates[j - 1] >= 0) {
                    dp[i][j] += dp[i - candidates[j - 1]][j - 1];
                }
            }
        }
        
        // Extract the combinations from the dp table
        vector<vector<int>> combinations;
        backtrack(dp, target, n, candidates, combinations);
        return combinations;
    }
    
    void backtrack(vector<vector<int>>& dp, int target, int n, vector<int>& candidates, vector<vector<int>>& combinations) {
        if (target == 0) {
            combinations.push_back({});
            return;
        }
        for (int j = n; j >= 1; j--) {
            // Check if the current candidate was included in the previous combination
            if (target - candidates[j - 1] >= 0 && dp[target][j] != dp[target][j - 1]) {
                currentCombination.push_back(candidates[j - 1]);
                backtrack(dp, target - candidates[j - 1], j - 1, candidates, combinations);
                currentCombination.pop_back();
            }
        }
    }
};
```

**Time and Space Complexity Analysis**:
* **Time Complexity:** O(N * T), where N is the number of candidates and T is the target.
* **Space Complexity:** O(N * T), as the dp table stores the number of combinations for each target and each subset of candidates.