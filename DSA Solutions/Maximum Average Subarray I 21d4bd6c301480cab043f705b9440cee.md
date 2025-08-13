# Maximum Average Subarray I

Difficulty: easy
 : Yes
: June 25, 2025
Problem: array, sliding window
Time Taken: 1 hour+

### 🔍 Problem

> Find the contiguous subarray of length k with the maximum average value and return that average.
> 

---

### 💣 Brute Force (TLE Risk)

### ⚠️ Issue You Faced

- Initially, you were going out of bounds using this condition:
    
    ```cpp
    i + k < nums.size()
    
    ```
    
    which is incorrect.
    

### ✅ Correct Condition:

```cpp
i <= nums.size() - k

```

### 🧠 Logic

- Loop through the array with index `i`
- For every `i`, calculate the sum of next `k` elements
- Track the maximum sum

### 🧾 Code

```cpp
double findMaxAverage(vector<int>& nums, int k) {
    double maxSum = INT_MIN;
    for(int i = 0; i <= nums.size() - k; i++) {
        double sum = 0;
        for(int j = i; j < i + k; j++) {
            sum += nums[j];
        }
        maxSum = max(maxSum, sum);
    }
    return maxSum / k;
}

```

### ❌ Time Complexity:

- O(n * k), will cause **TLE** on large inputs

---

### ⚡ Optimized Solution (Sliding Window)

### ✔️ Idea:

1. First, get the sum of the first `k` elements
2. Then slide the window forward:
    - **Add** the next element
    - **Remove** the first element of the previous window
    - Keep updating the max sum

### 📘 Example:

Given array: `[1, 12, -5, -6, 50, 3]`, `k = 3`

- First sum: `1 + 12 + (-5) = 8` → max = 8
- Slide window:
    - Add `6`, remove `1`: `8 - 1 + (-6) = 1`
    - Add `50`, remove `12`: `1 - 12 + 50 = 39`
    - Add `3`, remove `5`: `39 - (-5) + 3 = 47`

### ✅ Code:

```cpp
double findMaxAverage(vector<int>& nums, int k) {
    int n = nums.size();
    double sum = 0;

    // Initial window sum
    for(int i = 0; i < k; i++) {
        sum += nums[i];
    }

    double maxSum = sum;

    // Slide the window
    for(int i = k; i < n; i++) {
        sum += nums[i] - nums[i - k];
        maxSum = max(maxSum, sum);
    }

    return maxSum / k;
}

```

### 🕒 Time Complexity:

- O(n) — efficient for large inputs

---

### 🔑 Summary

- **Brute force** works but is slow → O(n * k)
- **Sliding window** is efficient → O(n)
- Always be careful with bounds (`i <= n - k`, not `i + k < n`)
- Use **sum = sum + new - old** to slide the window efficiently