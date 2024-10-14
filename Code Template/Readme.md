# Sliding Window

## Fixed Size

```c++
int left = 0, right = 0;
int k = // window size;

while (right < size) {
    // Expand the window
    // Perform operations based on the window

    if (right - left + 1 == k) { // Window reaches fixed size
        // Calculate result or check condition for the fixed window size
        
        // Move the left pointer to shrink the window
        left++;
    }

    // Move the right pointer to expand the window
    right++;
}
```

### Fixed Size Sliding Window Problems

- [Maximum Sum of a Subarray of Size K](https://leetcode.com/problems/maximum-sum-of-a-subarray-of-size-k/)
- [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
- [Average of Subarray of Size K](https://leetcode.com/problems/average-of-subarray-of-size-k/)
- [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)
- [Permutation in String](https://leetcode.com/problems/permutation-in-string/)


## Variable Size

```c++
int left = 0, right = 0;

while (right < size) {
    // Expand the window by adding the element at 'right' index
    
    // Check if the window satisfies a given condition
    while (condition is violated) {
        // Shrink the window by moving 'left'
        left++;
    }
    
    // Calculate the result when the condition is satisfied
    // Update result as needed (e.g., longest substring, max sum, etc.)

    // Move the 'right' pointer to expand the window
    right++;
}
```

### Variable Size Sliding Window Problems

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
- [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)


## Two Pointers Template

```c++
int left = 0, right = size - 1;
while (left < right) {
    // Perform operations based on the two pointers

    if (/* condition */) {
        left++; // Move the left pointer
    } else {
        right--; // Move the right pointer
    }
}
```

### Two Pointers Problems

- [3Sum](https://leetcode.com/problems/3sum/)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
- [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
- [Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/)

## Standard Binary Search (Search for a Specific Value)

```c++
int binarySearch(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;  // Avoid overflow

        if (arr[mid] == target) {
            return mid;  // Target found
        } 
        else if (arr[mid] < target) {
            left = mid + 1;  // Move to the right half
        } 
        else {
            right = mid - 1;  // Move to the left half
        }
    }

    return -1;  // Target not found
}
```

## Binary Search for Lower Bound (First Occurrence)

```c++
int lowerBound(vector<int>& arr, int target) {
    int left = 0, right = arr.size();  // right is 'size' for the insertion point

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] < target) {
            left = mid + 1;  // Target is to the right
        } else {
            right = mid;  // Shrink towards the left
        }
    }

    return left;  // 'left' will be the lower bound
}
```

## Binary Search for Upper Bound (Next Larger Element)

```c++
int upperBound(vector<int>& arr, int target) {
    int left = 0, right = arr.size();  // right is 'size' for the insertion point

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] <= target) {
            left = mid + 1;  // Move to the right half
        } else {
            right = mid;  // Shrink towards the left
        }
    }

    return left;  // 'left' will be the upper bound
}
```

## Binary Search for Maximum/Minimum Value in Monotonic Function

```c++
int findPeak(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] < arr[mid + 1]) {
            left = mid + 1;  // Peak is to the right
        } else {
            right = mid;  // Peak is to the left
        }
    }

    return left;  // or return right; both point to the peak
}
```

## Binary Search on Answer

```c++
bool isPossible(vector<int>& stations, int K, double distance) {
    // Function that checks if we can place the stations such that the max distance is <= 'distance'
    int count = 0;
    for (int i = 1; i < stations.size(); i++) {
        count += (stations[i] - stations[i - 1]) / distance;
    }
    return count <= K;  // Check if we can place at most K stations
}

double minimizeMaxDistance(vector<int>& stations, int K) {
    double left = 0, right = 1e9;

    while (right - left > 1e-6) {  // Precision level
        double mid = left + (right - left) / 2;

        if (isPossible(stations, K, mid)) {
            right = mid;  // Try to minimize the max distance
        } else {
            left = mid;  // Increase the allowed distance
        }
    }

    return left;  // or return right
}
```

### Binary Search Problems

- [Binary Search](https://leetcode.com/problems/binary-search/)
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/)
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)
- [Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
- [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)


## Backtracking Template

```c++
void backtrack(/* parameters */) {
    // Base case
    if (/* condition */) {
        // Handle the solution
        return;
    }
    
    for (/* choices */) {
        // Choose an option
        backtrack(/* parameters with choice */);
        // Undo the choice (if necessary)
    }
}
```

### Backtracking Problems

- [Permutations](https://leetcode.com/problems/permutations/)
- [Subsets](https://leetcode.com/problems/subsets/)
- [N-Queens](https://leetcode.com/problems/n-queens/)
- [Combination Sum](https://leetcode.com/problems/combination-sum/)
- [Word Search](https://leetcode.com/problems/word-search/)


## Dynamic Programming Template

```c++
vector<int> dp(size, -1); // or use appropriate size

for (int i = 0; i < size; i++) {
    if (/* base case condition */) {
        dp[i] = /* base case value */;
    } else {
        // Fill dp[i] based on previous states
        dp[i] = /* calculation using dp[i-1], dp[i-2], etc. */;
    }
}

// The answer will be in dp[desired_index];
```

### Dynamic Programming Problems

- [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- [Coin Change](https://leetcode.com/problems/coin-change/)
- [Edit Distance](https://leetcode.com/problems/edit-distance/)
- [Unique Paths](https://leetcode.com/problems/unique-paths/)


## Breadth-First Search (BFS) Template

```c++
#include <queue>

void bfs(/* parameters */) {
    std::queue</* node type */> q;
    // Initialize the queue with starting point

    while (!q.empty()) {
        auto current = q.front();
        q.pop();

        // Process the current node or state
        for (/* neighbors or options */) {
            // Check conditions to add to queue
            q.push(/* new state */);
        }
    }
}
```

### Breadth-First Search (BFS) Problems

- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- [Word Ladder](https://leetcode.com/problems/word-ladder/)
- [Open the Lock](https://leetcode.com/problems/open-the-lock/)
- [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- [Shortest Path in a Binary Matrix](https://leetcode.com/problems/shortest-path-in-a-binary-matrix/)

## Depth-First Search (DFS) Template

```c++
void dfs(/* parameters */) {
    // Base case
    if (/* condition */) {
        return;
    }
    
    // Process the current node or state
    for (/* neighbors or options */) {
        dfs(/* parameters for the next state */);
    }
}
```

### Depth-First Search (DFS) Problems

- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- [Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [Combinations](https://leetcode.com/problems/combinations/)
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

## 

```c++

```

### 


## 

```c++

```

### 


## 

```c++

```

### 
