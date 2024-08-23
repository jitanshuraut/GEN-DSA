**Question**: majority-elementsn-3-times-find-the-elements-that-appears-more-than-n-3-times-in-the-array/: Problem Statement: Given an array of N integers. Find the elements that appear more than N/3 times in the array. If no such element exists, return an empty vector.

**Approach 1: HashMap**
**Explanation**: Iterate over the array and store the frequency of each element in a HashMap. Then, iterate over the HashMap and check if the frequency of an element is greater than N/3. If yes, add the element to the result.

**C++ Code**:

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

using namespace std;

vector<int> majorityElements(vector<int>& nums) {
  unordered_map<int, int> frequency;
  int n = nums.size();
  for (int num : nums) {
    frequency[num]++;
  }
  vector<int> result;
  for (const auto& [num, count] : frequency) {
    if (count > n / 3) {
      result.push_back(num);
    }
  }
  return result;
 }

int main() {
  vector<int> nums = {3, 2, 3};
  vector<int> result = majorityElements(nums);
  for (int num : result) {
    cout << num << " ";
  }
  cout << endl;
  return 0;
}
```

**Time Complexity**: O(N), where N is the size of the input array.
**Space Complexity**: O(N), as we store the frequency of each element in the HashMap.

**Approach 2: Boyer-Moore Majority Vote Algorithm**
**Explanation**: The Boyer-Moore Majority Vote Algorithm can find the majority elements in linear time and constant space complexity. It works by using two pointers and counting the occurrences of the majority elements.

**C++ Code**:

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> majorityElements(vector<int>& nums) {
  int n = nums.size();
  int maj1 = 0, maj2 = 0, count1 = 0, count2 = 0;
  for (int num : nums) {
    if (maj1 == num) {
      count1++;
    } else if (maj2 == num) {
      count2++;
    } else if (count1 == 0) {
      maj1 = num;
      count1 = 1;
    } else if (count2 == 0) {
      maj2 = num;
      count2 = 1;
    } else {
      count1--;
      count2--;
    }
  }
  count1 = 0;
  count2 = 0;
  for (int num : nums) {
    if (num == maj1) {
      count1++;
    } else if (num == maj2) {
      count2++;
    }
  }
  vector<int> result;
  if (count1 > n / 3) {
    result.push_back(maj1);
  }
  if (count2 > n / 3) {
    result.push_back(maj2);
  }
  return result;
}

int main() {
  vector<int> nums = {3, 2, 3};
  vector<int> result = majorityElements(nums);
  for (int num : result) {
    cout << num << " ";
  }
  cout << endl;
  return 0;
}
```

**Time Complexity**: O(N), where N is the size of the input array.
**Space Complexity**: O(1), as we only store a constant number of variables.**Question**: Given an array of N integers. Find the elements that appear more than N/3 times in the array. If no such element exists, return an empty vector.

**Approach 1: Boyer-Moore Majority Vote Algorithm**
- **Explanation**:
  - The Boyer-Moore Majority Vote Algorithm is a linear time and constant space algorithm that can find majority elements in an array.
  - The algorithm works by maintaining two variables, a majority candidate and a count of its occurrences.
  - It iterates through the array and updates the majority candidate and the count.
  - If the count becomes zero, it means that the current majority candidate is not a majority element, so it is reset to the next element in the array and the count is set to 1.
  - If the count becomes equal to the majority threshold (i.e. N/3), the current majority candidate is returned as a majority element.
- **Code**:
```cpp
vector<int> findMajorityElements(vector<int>& nums) {
  int majority1 = -1, count1 = 0, majority2 = -1, count2 = 0;
  for (int num : nums) {
    if (num == majority1) {
      count1++;
    } else if (num == majority2) {
      count2++;
    } else if (count1 == 0) {
      majority1 = num;
      count1 = 1;
    } else if (count2 == 0) {
      majority2 = num;
      count2 = 1;
    } else {
      count1--;
      count2--;
    }
  }

  count1 = 0;
  count2 = 0;
  for (int num : nums) {
    if (num == majority1) count1++;
    if (num == majority2) count2++;
  }

  vector<int> result;
  if (count1 > nums.size() / 3) result.push_back(majority1);
  if (count2 > nums.size() / 3) result.push_back(majority2);
  return result;
}
```
- **Time and Space Complexity Analysis**:
  - Time Complexity: O(N), where N is the length of the array.
  - Space Complexity: O(1), as it uses constant space to store the majority candidates and their counts.

**Approach 2: HashMap**
- **Explanation**:
  - Create a hashmap to store the count of each element in the array.
  - Iterate over the array and update the count in the hashmap.
  - Check if any element's count is greater than N/3 times the length of the array.
  - Return the elements that satisfy this condition.
- **Code**:
```cpp
vector<int> findMajorityElements(vector<int>& nums) {
  unordered_map<int, int> countMap;
  for (int num : nums) {
    countMap[num]++;
  }

  vector<int> result;
  for (auto& [num, count] : countMap) {
    if (count > nums.size() / 3) {
      result.push_back(num);
    }
  }

  return result;
}
```
- **Time and Space Complexity Analysis**:
  - Time Complexity: O(N), where N is the length of the array.
  - Space Complexity: O(N), as it uses a hashmap to store the count of each element.

**Approach 3: Sorting**
- **Explanation**:
  - Sort the array in ascending order.
  - Find the elements that appear consecutively for more than N/3 times the length of the array.
- **Code**:
```cpp
vector<int> findMajorityElements(vector<int>& nums) {
  sort(nums.begin(), nums.end());

  vector<int> result;
  int count = 1, prev = nums[0];
  for (int i = 1; i < nums.size(); i++) {
    if (nums[i] == prev) {
      count++;
    } else {
      if (count > nums.size() / 3) {
        result.push_back(prev);
      }
      count = 1;
      prev = nums[i];
    }
  }

  if (count > nums.size() / 3) {
    result.push_back(prev);
  }

  return result;
}
```
- **Time and Space Complexity Analysis**:
  - Time Complexity: O(N log N), where N is the length of the array.
  - Space Complexity: O(1), as it does not use any additional data structures.