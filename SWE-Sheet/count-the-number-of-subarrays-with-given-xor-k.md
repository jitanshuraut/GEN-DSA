**Question**: count-the-number-of-subarrays-with-given-xor-k/: Problem Statement: Given an array of integers A and an integer B. Find the total number of subarrays having bitwise XOR of all elements equal to k.

**Approach 1: Brute Force**
 **Explanation**: This approach involves iterating over all possible subarrays of the given array and checking if the bitwise XOR of the elements in the subarray is equal to the given integer k. For each valid subarray, we increment a counter.
```cpp
int countSubarrays(int arr[], int n, int k) 
{ 
    int count = 0; 
    for (int i = 0; i < n; i++) { 
        int curr_xor = 0; 
        for (int j = i; j < n; j++) { 
            curr_xor = curr_xor ^ arr[j]; 
            if (curr_xor == k) 
                count++; 
        } 
    } 
} 
```
**Time and Space Complexity Analysis**: The brute force approach has a time complexity of O(n^2), where n is the number of elements in the array, and a space complexity of O(1).

**Approach 2: Optimized Approach using Maps**
**Explanation**: This approach uses a map to store the prefix XOR values of the array and their corresponding frequencies. For each prefix XOR value, we check if the (prefix XOR value ^ k) exists in the map. If it does, we add its frequency to the count of valid subarrays.
```cpp
int countSubarrays(int arr[], int n, int k) 
{ 
    int prefixXOR = 0; 
    int count = 0; 
    unordered_map<int, int> freq; 
    freq[0] = 1; 
    for (int i = 0; i < n; i++) 
    {  
        prefixXOR = prefixXOR ^ arr[i]; 
        count += freq[prefixXOR ^ k]; 
        freq[prefixXOR]++; 
    } 
    return count; 
}
```
**Time and Space Complexity Analysis**: The optimized approach using maps has a time complexity of O(n), where n is the number of elements in the array, and a space complexity of O(n).

**Approach 3: Optimized Approach using Two Pointers**
**Explanation**: This approach maintains two pointers, left and right, and expands the subarray by moving the right pointer. For each valid subarray, we increment a counter. If the bitwise XOR of the subarray equals k, we advance the left pointer until the bitwise XOR is no longer equal to k.
```cpp
int countSubarrays(int arr[], int n, int k) 
{ 
    int pre[n + 1]; 
    for (int i = 0; i < n; i++) 
        pre[i + 1] = pre[i] ^ arr[i]; 
    int ans = 0, left = 0, right = 0; 
    while (left <= right && right <= n) 
    { 
        if (pre[right] - pre[left] == k) 
        { 
            ans++; 
            right++; 
        } 
        else if (pre[right] - pre[left] < k) 
        { 
            right++; 
        } 
        else 
        { 
            left++; 
        } 
    } 
    return ans; 
}
```
**Time and Space Complexity Analysis**: The optimized approach using two pointers has a time complexity of O(n), where n is the number of elements in the array, and a space complexity of O(n).

**Approach 4: Recursive Approach**
**Explanation**: This approach uses recursion to calculate the count of valid subarrays. It considers two cases: including the current element in the subarray or excluding it. The final count is returned by combining the counts for both cases.
```cpp
int countSubarraysUtil(int arr[], int n,  int k, int XOR)
{
    if (n == 0) 
    {
        if (XOR == k) 
            return 1; 
        return 0; 
    }
    return countSubarraysUtil(arr + 1, n - 1, k, XOR ^ arr[0]) + countSubarraysUtil(arr + 1, n - 1, k, XOR); 
}

int countSubarrays(int arr[], int n, int k) 
{ 
    return countSubarraysUtil(arr, n, k, 0); 
}
```
**Time and Space Complexity Analysis**: The recursive approach has a time complexity of O(2^n), where n is the number of elements in the array, and a space complexity of O(n).

**Approach 5: Backtracking Approach**
**Explanation**: This approach uses backtracking to generate all possible subarrays and check if their bitwise XOR is equal to k. If so, the count is incremented.
```cpp
void countSubarraysUtil(int arr[], int n, vector<int> &subarray, int k, int &count) 
{ 
    if (n == arr.size()) 
    { 
        int XOR = 0; 
        for (int i = 0; i < subarray.size(); i++) 
            XOR ^= subarray[i]; 
        if (XOR == k) 
            count++; 
        return; 
    } 
    countSubarraysUtil(arr, n + 1, subarray, k, count); 
    subarray.push_back(arr[n]); 
    countSubarraysUtil(arr, n + 1, subarray, k, count); 
    subarray.pop_back(); 
} 

int countSubarrays(int arr[], int n, int k) 
{ 
    int count = 0; 
    vector<int> subarray; 
    countSubarraysUtil(arr, 0, subarray, k, count); 
    return count; 
} 
```
**Time and Space Complexity Analysis**: The backtracking approach has a time complexity of O(2^n), where n is the number of elements in the array, and a space complexity of O(n).**Question**: count-the-number-of-subarrays-with-given-xor-k/: Problem Statement: Given an array of integers A and an integer B. Find the total number of subarrays having bitwise XOR of all elements equal to k.

**Approach 1: Brute Force**
* **Explanation**: Calculate the XOR of each possible subarray and count the number of subarrays having XOR equal to k.
* **C++ Code**:
```cpp
int countSubarrays(vector<int>& A, int k) {
    int count = 0;
    int n = A.size();
    for (int i = 0; i < n; i++) {
        int XOR = 0;
        for (int j = i; j < n; j++) {
            XOR ^= A[j];
            if (XOR == k) {
                count++;
            }
        }
    }
    return count;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N^2)
* Space Complexity: O(1)

**Approach 2: Prefix XOR and HashMap**
* **Explanation**: Use the prefix XOR array to reduce the number of XOR calculations. The key idea is to find all pairs of indices (i, j) such that XOR(A[0..i]) ^ XOR(A[0..j]) = k. We can use a HashMap to store the count of each prefix XOR.
* **C++ Code**:
```cpp
int countSubarrays(vector<int>& A, int k) {
    int count = 0;
    int prefixXOR = 0;
    unordered_map<int, int> XORCount;
    XORCount[0] = 1;
    for (int i = 0; i < A.size(); i++) {
        prefixXOR ^= A[i];
        count += XORCount[prefixXOR ^ k];
        XORCount[prefixXOR]++;
    }
    return count;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N)
* Space Complexity: O(N)

**Approach 3: Trie**
* **Explanation**: Build a Trie to store all possible prefixes of the array. For each element, insert its XOR into the Trie. While inserting, count the number of paths that have XOR equal to k.
* **C++ Code**:
```cpp
struct TrieNode {
    TrieNode* children[2];
    int count;
    TrieNode() {
        children[0] = children[1] = nullptr;
        count = 0;
    }
};
int countSubarrays(vector<int>& A, int k) {
    TrieNode* root = new TrieNode();
    int count = 0;
    TrieNode* current = root;
    for (int i = 0; i < A.size(); i++) {
        int XOR = 0;
        current = root;
        for (int j = i; j < A.size(); j++) {
            XOR ^= A[j];
            if (current->children[XOR & 1] == nullptr) {
                current->children[XOR & 1] = new TrieNode();
            }
            current = current->children[XOR & 1];
            current->count++;
            if (XOR == k) {
                count += current->count - 1;
            }
        }
    }
    return count;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N * log N)
* Space Complexity: O(N)

**Approach 4: Sliding Window Technique**
* **Explanation**: Use a sliding window of size k to count the number of subarrays having XOR equal to k. Increment the count when the window XOR is equal to k.
* **C++ Code**:
```cpp
int countSubarrays(vector<int>& A, int k) {
    int windowXOR = 0;
    int count = 0;
    for (int i = 0, j = 0; i < A.size(); i++) {
        windowXOR ^= A[i];
        while (j < i && windowXOR != k) {
            windowXOR ^= A[j];
            j++;
        }
        if (windowXOR == k) {
            count += i - j + 1;
        }
    }
    return count;
}
```
**Time and Space Complexity Analysis**:
* Time Complexity: O(N)
* Space Complexity: O(1)