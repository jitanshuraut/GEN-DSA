**Question**: Given a String, find the length of longest substring without any repeating character.

**Approach 1: Brute Force**  

Explanation: 
The simplest solution is to try all possible substrings and check whether it contains unique characters or not. This can be done by using two nested loops. The outer loop will iterate over the start index of the substring, and the inner loop will iterate over the end index of the substring. For each substring, we can check if it contains unique characters or not by using a set. 

Code:
```cpp
int lengthOfLongestSubstring(string s) {
  int n = s.size();
  int maxLen = 0;

  for (int i = 0; i < n; i++) {
    set<char> charSet;
    for (int j = i; j < n; j++) {
      if (charSet.find(s[j]) == charSet.end()) {
        charSet.insert(s[j]);
        maxLen = max(maxLen, j - i + 1);
      } else {
        break;
      }
    }
  }
  return maxLen;
}
```

Time and Space Complexity Analysis:
* Time Complexity: O(n^2), where n is the length of the input string.
* Space Complexity: O(n), where n is the length of the input string.

**Approach 2: Optimized using Sliding Window with Set** 

Explanation: 
We can optimize the brute force approach using a sliding window and a set. The idea is to maintain a sliding window of unique characters, and expand the window as long as the characters remain unique. When a repeating character is encountered, we can shrink the window by removing the leftmost character until the window contains unique characters again.

Code:
```cpp
int lengthOfLongestSubstring(string s) {
  int n = s.size();
  int maxLen = 0;
  int start = 0;
  set<char> charSet;

  for (int end = 0; end < n; end++) {
    if (charSet.find(s[end]) == charSet.end()) {
      charSet.insert(s[end]);
      maxLen = max(maxLen, end - start + 1);
    } else {
      while (charSet.find(s[end]) != charSet.end()) {
        charSet.erase(s[start]);
        start++;
      }
      charSet.insert(s[end]);
    }
  }
  return maxLen;
}
```

Time and Space Complexity Analysis:
* Time Complexity: O(n), where n is the length of the input string.
* Space Complexity: O(n), where n is the length of the input string.

**Approach 3: Optimized using Sliding Window with Map** 

Explanation: 
Similar to Approach 2, but we can use a map to track the last occurrence of each character in the string. This allows us to directly jump to the next unique character without having to iterate through the entire window.

Code:
```cpp
int lengthOfLongestSubstring(string s) {
  int n = s.size();
  int maxLen = 0;
  int start = 0;
  map<char, int> charMap;

  for (int end = 0; end < n; end++) {
    if (charMap.find(s[end]) != charMap.end()) {
      start = max(start, charMap[s[end]] + 1);
    }
    charMap[s[end]] = end;
    maxLen = max(maxLen, end - start + 1);
  }
  return maxLen;
}
```

Time and Space Complexity Analysis:
* Time Complexity: O(n), where n is the length of the input string.
* Space Complexity: O(n), where n is the length of the input string.**Question**: length-of-longest-substring-without-any-repeating-character/: Problem Statement: Given a String, find the length of longest substring without any repeating character.

**Approach 1: Brute-Force Approach**

**Explanation**: This is the most straightforward approach. We can consider all possible substrings of the given string and check if each substring has no repeating characters. The substring with the maximum length is the required answer.

**Approach 1 Code**:

```cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int longest_substring_without_repeating_character(string str) {
  int n = str.length();
  int max_len = 0;
  for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {
      unordered_set<char> char_set;
      bool has_repeating_character = false;
      for (int k = i; k <= j; k++) {
        if (char_set.find(str[k]) != char_set.end()) {
          has_repeating_character = true;
          break;
        }
        char_set.insert(str[k]);
      }
      if (!has_repeating_character) {
        max_len = max(max_len, j - i + 1);
      }
    }
  }
  return max_len;
}

int main() {
  string str = "abcabcbb";
  int result = longest_substring_without_repeating_character(str);
  cout << "The length of the longest substring without any repeating character is: " << result << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 1**:

* **Time complexity**: O(n^3), where n is the length of the given string.
* **Space complexity**: O(n), where n is the length of the given string.

**Approach 2: Sliding Window Technique**

**Explanation**: The sliding window technique is a more efficient approach than the brute-force approach. We maintain a sliding window that represents the current substring under consideration. We move the window forward one character at a time and check if the current substring has no repeating characters. If it does, we update the maximum length.

**Approach 2 Code**:

```cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int longest_substring_without_repeating_character(string str) {
  int n = str.length();
  int max_len = 0;
  int start = 0;
  int end = 0;
  unordered_set<char> char_set;

  while (end < n) {
    if (char_set.find(str[end]) == char_set.end()) {
      char_set.insert(str[end]);
      max_len = max(max_len, end - start + 1);
      end++;
    } else {
      char_set.erase(str[start]);
      start++;
    }
  }

  return max_len;
}

int main() {
  string str = "abcabcbb";
  int result = longest_substring_without_repeating_character(str);
  cout << "The length of the longest substring without any repeating character is: " << result << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 2**:

* **Time complexity**: O(n), where n is the length of the given string.
* **Space complexity**: O(n), where n is the length of the given string.

**Approach 3: Trie Data Structure**

**Explanation**: We can use a trie data structure to efficiently check if a substring has any repeating characters. We can insert all the characters of the given string into the trie and then check if the trie contains any duplicate characters.

**Approach 3 Code**:

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

struct TrieNode {
  unordered_map<char, TrieNode*> children;
  bool is_end_of_word;
};

TrieNode* create_trie_node() {
  TrieNode* node = new TrieNode;
  node->is_end_of_word = false;
  return node;
}

void insert_string_into_trie(TrieNode* root, string str) {
  TrieNode* curr = root;
  for (char c : str) {
    if (curr->children.find(c) == curr->children.end()) {
      curr->children[c] = create_trie_node();
    }
    curr = curr->children[c];
  }
  curr->is_end_of_word = true;
}

bool has_duplicate_characters(TrieNode* root, string str) {
  TrieNode* curr = root;
  for (char c : str) {
    if (curr->children[c]->is_end_of_word) {
      return true;
    }
    curr = curr->children[c];
  }
  return false;
}

int longest_substring_without_repeating_character(string str) {
  TrieNode* root = create_trie_node();
  int n = str.length();
  int max_len = 0;
  int start = 0;
  int end = 0;

  while (end < n) {
    if (!has_duplicate_characters(root, str.substr(start, end - start + 1))) {
      insert_string_into_trie(root, str.substr(start, end - start + 1));
      max_len = max(max_len, end - start + 1);
      end++;
    } else {
      start++;
    }
  }

  return max_len;
}

int main() {
  string str = "abcabcbb";
  int result = longest_substring_without_repeating_character(str);
  cout << "The length of the longest substring without any repeating character is: " << result << endl;
  return 0;
}
```

**Time and Space Complexity Analysis for Approach 3**:

* **Time complexity**: O(n^2), where n is the length of the given string.
* **Space complexity**: O(n^2), where n is the length of the given string.

**Note**: Approaches 1 and 2 are more efficient than Approach 3 for this problem. Approach 3 is included for completeness, but it is not the best approach for this problem.