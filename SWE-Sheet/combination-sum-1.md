**Question**: "combination-sum-1/: Problem Statement: "

## Approach 1: Backtracking

**Explanation:**
- Initialize an empty vector to store the combinations.
- Iterate through the candidates array from the beginning.
- For each candidate, recursively explore combinations that include the candidate and combinations that don't.
- Keep track of the remaining target sum as we traverse the candidates.

**Approach 1 Code**:
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> combination;
        backtrack(candidates, target, 0, combination, result);
        return result;
    }

private:
    void backtrack(vector<int>& candidates, int target, int start, vector<int>& combination, vector<vector<int>>& result) {
        if (target == 0) {
            result.push_back(combination);
            return;
        }
        if (target < 0) {
            return;
        }

        for (int i = start; i < candidates.size(); i++) {
            combination.push_back(candidates[i]);
            backtrack(candidates, target - candidates[i], i, combination, result);
            combination.pop_back();  // backtrack
        }
    }
};
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(2^n), where n is the number of candidates. Each candidate can be either included or excluded, leading to exponential combinations.
- Space Complexity: O(n), as the recursive stack space required is proportional to the number of candidates.

## Approach 2: Dynamic Programming (Memoization)

**Explanation:**
- Create a map to store the computed combinations for different target sums.
- Iterate through the candidates array.
- For each candidate, recursively explore combinations that include the candidate and combinations that don't.
- Check if the combination for the remaining target sum has already been computed. If so, reuse the stored combination. Otherwise, compute it and store it for future use.

**Approach 2 Code**:
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        unordered_map<int, vector<vector<int>>> memo;
        return combinationSumUtil(candidates, target, 0, memo);
    }

private:
    vector<vector<int>> combinationSumUtil(vector<int>& candidates, int target, int start, unordered_map<int, vector<vector<int>>>& memo) {
        if (target == 0) {
            return {{}};
        }
        if (target < 0) {
            return {};
        }

        if (memo.count(target) > 0) {  // Check if already computed
            return memo[target];
        }

        vector<vector<int>> combinations;
        for (int i = start; i < candidates.size(); i++) {
            vector<vector<int>> subCombinations = combinationSumUtil(candidates, target - candidates[i], i, memo);
            for (const auto& subCombination : subCombinations) {
                subCombination.push_back(candidates[i]);
                combinations.push_back(subCombination);
            }
        }

        memo[target] = combinations;
        return combinations;
    }
};
```

**Time and Space Complexity Analysis**:
- Time Complexity: O(n * target), where n is the number of candidates and target is the target sum. Each candidate is considered for each possible target sum, resulting in a linear time complexity per target.
- Space Complexity: O(target), as we need to store the combinations for each target sum in the memoization map.**Question**: Combination Sum I

**Problem Statement**: Given a list of candidate numbers `candidates` (without duplicates) and a target number `target`, find all unique combinations of `candidates` where the sum of selected numbers is equal to the `target`. The same number can be used multiple times in a combination.
Note: The solution set must not contain duplicate combinations.

**Approach 1: Backtracking**
**Explanation**: This approach uses backtracking to explore all possible combinations of `candidates`. We start with an empty combination and then iteratively add candidates to the combination. If the sum of the combination exceeds the target, we backtrack and remove the last added candidate. If the sum of the combination equals the target, we add it to the solution set.

**Approach 1 Code**:
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> combination;
        backtrack(candidates, target, combination, result, 0);
        return result;
    }

private:
    void backtrack(vector<int>& candidates, int target, vector<int>& combination, vector<vector<int>>& result, int start) {
        if (target == 0) {
            result.push_back(combination);
            return;
        }
        for (int i = start; i < candidates.size(); i++) {
            if (candidates[i] > target) {
                break;
            }
            combination.push_back(candidates[i]);
            backtrack(candidates, target - candidates[i], combination, result, i);
            combination.pop_back();
        }
    }
};
```

**Time and Space Complexity Analysis for Approach 1**:
  - Time Complexity: O(2^n), where n is the number of candidates.
  - Space Complexity: O(n), since we need to store the current combination and the result set.

**Approach 2: Dynamic Programming**
**Explanation**: This approach uses dynamic programming to solve the problem. We define a 2D array `dp` where `dp[i][j]` represents the number of ways to sum up to `j` using the first `i` candidates. We initialize `dp[0][0] = 1` and `dp[i][0] = 1` for all `i`. Then, for each candidate `candidates[i]`, we iterate through all previous sums `j` and update `dp[i][j]` accordingly. Finally, we return the number of ways to sum up to `target` using all candidates.

**Approach 2 Code**:
```cpp
class Solution {
public:
    int combinationSum4(vector<int>& candidates, int target) {
        vector<unsigned int> dp(target + 1, 0);
        dp[0] = 1;
        for (int i = 1; i <= target; i++) {
            for (int candidate : candidates) {
                if (i >= candidate) {
                    dp[i] += dp[i - candidate];
                }
            }
        }
        return dp[target];
    }
};
```

**Time and Space Complexity Analysis for Approach 2**:
  - Time Complexity: O(n * target), where n is the number of candidates and target is the target sum.
  - Space Complexity: O(target), since we need to store the dp array.