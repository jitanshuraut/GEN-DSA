**Question:**

palindrome-partitioning/: Problem Statement: You are given a string s, partition it in such a way that every substring is a palindrome. Return all such palindromic partitions of s.

**Approach 1: Brute Force**

**Explanation:**

This approach iterates through all possible partitions of the string and checks if each substring is a palindrome. If yes, the partition is added to the result list.

**Approach 1 Code:**

```cpp
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<vector<string>> result;
        vector<string> currentPartition;
        partitionHelper(s, 0, currentPartition, result);
        return result;
    }
private:
    void partitionHelper(string s, int start, vector<string>& currentPartition, vector<vector<string>>& result) {
        int n = s.length();
        // Base case: end of string reached
        if (start == n) {
            result.push_back(currentPartition);
            return;
        }
        // Iterate through all possible substring lengths 
        for (int end = start + 1; end <= n; end++) {
            string substring = s.substr(start, end - start);
            if (isPalindrome(substring)) {
                currentPartition.push_back(substring);
                partitionHelper(s, end, currentPartition, result);
                currentPartition.pop_back();
            }
        }
    }
    bool isPalindrome(string s) {
        int n = s.length();
        for (int i = 0; i < n / 2; i++) {
            if (s[i] != s[n - i - 1]) {
                return false;
            }
        }
        return true;
    }
};
```

**Time and Space Complexity Analysis for Approach 1:**

* Time Complexity: O(2^n), where n is the length of the string.
* Space Complexity: O(n), since the recursion stack can go up to n levels.

**Approach 2: Memoized Brute Force**

**Explanation:**

This approach uses memoization to store the results of previously encountered substrings, avoiding redundant checks.

**Approach 2 Code:**

```cpp
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<vector<string>> result;
        unordered_map<string, vector<vector<string>>> memo;
        return partitionHelper(s, 0, memo);
    }
private:
    vector<vector<string>> partitionHelper(string s, int start, unordered_map<string, vector<vector<string>>>& memo) {
        int n = s.length();
        if (start == n) {
            return { {} };
        }
        if (memo.count(s.substr(start)) > 0) {
            return memo[s.substr(start)];
        }
        vector<vector<string>> partitions;
        for (int end = start + 1; end <= n; end++) {
            string substring = s.substr(start, end - start);
            if (isPalindrome(substring)) {
                vector<vector<string>> subpartitions = partitionHelper(s, end, memo);
                for (auto& subpartition : subpartitions) {
                    subpartition.insert(subpartition.begin(), substring);
                    partitions.push_back(subpartition);
                }
            }
        }
        memo[s.substr(start)] = partitions;
        return partitions;
    }
    bool isPalindrome(string s) {
        int n = s.length();
        for (int i = 0; i < n / 2; i++) {
            if (s[i] != s[n - i - 1]) {
                return false;
            }
        }
        return true;
    }
};
```

**Time and Space Complexity Analysis for Approach 2:**

* Time Complexity: O(2^n), but reduced due to memoization.
* Space Complexity: O(n), for the recursion stack and memoization table.

**Approach 3: Dynamic Programming**

**Explanation:**

This approach builds a table where each cell contains a boolean value indicating whether the corresponding substring is a palindrome. It then uses this table to find all palindromic partitions.

**Approach 3 Code:**

```cpp
class Solution {
public:
    vector<vector<string>> partition(string s) {
        int n = s.length();
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }
        for (int length = 2; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;
                if (length == 2) {
                    dp[i][j] = (s[i] == s[j]);
                } else {
                    dp[i][j] = (dp[i + 1][j - 1] && (s[i] == s[j]));
                }
            }
        }
        vector<vector<string>> result;
        vector<string> currentPartition;
        partitionHelper(s, 0, dp, currentPartition, result);
        return result;
    }
private:
    void partitionHelper(string s, int start, vector<vector<bool>>& dp, vector<string>& currentPartition, vector<vector<string>>& result) {
        int n = s.length();
        if (start == n) {
            result.push_back(currentPartition);
            return;
        }
        for (int end = start + 1; end <= n; end++) {
            string substring = s.substr(start, end - start);
            if (dp[start][end - 1]) {
                currentPartition.push_back(substring);
                partitionHelper(s, end, dp, currentPartition, result);
                currentPartition.pop_back();
            }
        }
    }
};
```

**Time and Space Complexity Analysis for Approach 3:**

* Time Complexity: O(n^2), for building the DP table and partitioning the string.
* Space Complexity: O(n^2), for the DP table.

**Approach 4: Backtracking**

**Explanation:**

This approach uses recursion to generate all possible partitions of the string. It backtracks when a partition is not palindromic.

**Approach 4 Code:**

```cpp
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<vector<string>> result;
        vector<string> currentPartition;
        backtrack(s, 0, currentPartition, result);
        return result;
    }
private:
    void backtrack(string s, int start, vector<string>& currentPartition, vector<vector<string>>& result) {
        int n = s.length();
        if (start == n) {
            result.push_back(currentPartition);
            return;
        }
        for (int end = start + 1; end <= n; end++) {
            string substring = s.substr(start, end - start);
            if (isPalindrome(substring)) {
                currentPartition.push_back(substring);
                backtrack(s, end, currentPartition, result);
                currentPartition.pop_back();
            }
        }
    }
    bool isPalindrome(string s) {
        int n = s.length();
        for (int i = 0; i < n / 2; i++) {
            if (s[i] != s[n - i - 1]) {
                return false;
            }
        }
        return true;
    }
};
```

**Time and Space Complexity Analysis for Approach 4:**

* Time Complexity: O(2^n), for generating all possible partitions.
* Space Complexity: O(n), for the recursion stack.**Question**: "palindrome-partitioning/: Problem Statement: You are given a string s, partition it in such a way that every substring is a palindrome. Return all such palindromic partitions of s."

**Approach 1**: Brute Force Approach

**Explanation**: The brute force solution to this problem is to generate all possible partitions of the string and check if each partition is a palindrome. This approach is inefficient because it requires exponential time complexity.

**Approach 1 Code**: Below is C++ implementation of Brute Force technique:

```cpp
#include <bits/stdc++.h>

bool isPalindrome(string s) {
  int i = 0;
  int j = s.length() - 1;
  while (i < j) {
    if (s[i] != s[j]) {
      return false;
    }
    i++;
    j--;
  }
  return true;
}

vector<vector<string>> partition(string s) {
  if (s.empty()) {
    return {{}};
  }
  vector<vector<string>> result;
  for (int i = 1; i <= s.length(); i++) {
    string prefix = s.substr(0, i);
    if (isPalindrome(prefix)) {
      vector<vector<string>> suffixes = partition(s.substr(i));
      for (auto& suffix : suffixes) {
        suffix.insert(suffix.begin(), prefix);
        result.push_back(suffix);
      }
    }
  }
  return result;
}
```

**Time and Space Complexity Analysis for Approach 1**: The time complexity of this approach is O(2^n), where n is the length of the string s. The space complexity is O(n), where n is the length of the string s.

**Approach 2**: Dynamic Programming Approach

**Explanation**: The dynamic programming approach to this problem is to use a table to store the palindromic partitions of the string s. The table is indexed by the start and end indices of the substring. The value at each index is a list of palindromic partitions of the substring. The table is filled in bottom-up fashion, starting with the substrings of length 1. For each substring, the table is checked to see if it is a palindrome. If it is, then the palindromic partition of the substring is added to the table. Otherwise, the table is updated with the palindromic partitions of the substring's sub-substrings.

**Approach 2 Code**: Below is C++ implementation of Dynamic Programming technique:

```cpp
#include <bits/stdc++.h>

bool isPalindrome(string s) {
  int i = 0;
  int j = s.length() - 1;
  while (i < j) {
    if (s[i] != s[j]) {
      return false;
    }
    i++;
    j--;
  }
  return true;
}

vector<vector<string>> partition(string s) {
  int n = s.length();
  vector<vector<vector<string>>> dp(n, vector<vector<string>>(n));
  for (int i = 0; i < n; i++) {
    dp[i][i].push_back({s.substr(i, 1)});
  }
  for (int len = 2; len <= n; len++) {
    for (int i = 0; i <= n - len; i++) {
      int j = i + len - 1;
      if (isPalindrome(s.substr(i, len))) {
        dp[i][j].push_back({s.substr(i, len)});
      }
      for (int k = i; k < j; k++) {
        for (auto& left : dp[i][k]) {
          for (auto& right : dp[k + 1][j]) {
            dp[i][j].push_back(left);
            dp[i][j].back().push_back(right);
          }
        }
      }
    }
  }
  return dp[0][n - 1];
}
```

**Time and Space Complexity Analysis for Approach 2**: The time complexity of this approach is O(n^3), where n is the length of the string s. The space complexity is O(n^2), where n is the length of the string s.