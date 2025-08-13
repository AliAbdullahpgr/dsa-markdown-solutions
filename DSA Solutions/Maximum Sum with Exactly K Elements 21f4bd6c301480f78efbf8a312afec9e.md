# Maximum Sum with Exactly K Elements

Difficulty: easy
 : Yes
: June 27, 2025
Problem: array, sliding window
Time Taken: 10-20 minutes

## 🧠 Greedy Problem Note: Maximize Sum After K Increments

**LeetCode 2656 – Maximize the Sum of Selected Numbers From an Array After K Operations**

---

### 📜 Problem Statement:

- Given an integer array `nums` and an integer `k`, perform the following operation `k` times:
    1. Pick the **maximum number** in `nums`.
    2. Add it to your **score**.
    3. Increment it by `1`.
- Return the **total score** after `k` operations.

---

### ✅ Initial Attempt (Greedy Logic):

```cpp
class Solution {
public:
    int maximizeSum(vector<int>& nums, int k) {
        int sum = 0;
        int m = *max_element(nums.begin(), nums.end());
        for(int i = 0; i < k; i++) {
            sum += m++;
        }
        return sum;
    }
};

```

### ✔️ Explanation:

- Find the maximum value `m` from the array.
- In each of the `k` rounds, take `m`, add to sum, and increment `m`.
- Greedy because we **always choose the locally optimal (current maximum)** to get the globally optimal result.

### 🧠 Why this is Greedy:

- Always selecting the current maximum ensures the **highest possible gain at each step**.
- It doesn't require backtracking or looking ahead — just immediate best.

---

### 🔍 Minor Bug in First Version:

Originally:

```cpp
int m;
for(auto i:nums) m = max(m,i);

```

- This causes **undefined behavior** due to `m` being uninitialized.

✅ Fixed with:

```cpp
int m = INT_MIN;

```

**Or shorter:**

```cpp
int m = *max_element(nums.begin(), nums.end());

```

---

### ⚡ Optimization Using Math:

The sum:

```
m + (m + 1) + (m + 2) + ... + (m + k - 1)

```

is an **Arithmetic Progression (AP)** with:

- First term = m
- Number of terms = k
- Common difference = 1

So we use the AP sum formula:

Sum=k⋅m+k⋅(k−1)2\text{Sum} = k \cdot m + \frac{k \cdot (k - 1)}{2}

---

### 🚀 Final Optimized Code:

```cpp
class Solution {
public:
    int maximizeSum(vector<int>& nums, int k) {
        int m = *max_element(nums.begin(), nums.end());
        return k * m + (k * (k - 1)) / 2;
    }
};

```

- ✅ Eliminates the loop
- ✅ Time: O(n) due to `max_element`
- ✅ Space: O(1)

---

### 📚 Concepts Covered:

- ✅ Greedy Strategy
- ✅ Arithmetic Progression Sum
- ✅ Loop Elimination via Math
- ✅ STL function `max_element`

---

### 🏁 Final Verdict:

| Aspect | Status |
| --- | --- |
| Greedy Valid? | ✅ Yes |
| Optimized? | ✅ Fully (via AP formula) |
| Correctness? | ✅ Verified |
| Time Complexity | ✅ O(n) |
| Space | ✅ O(1) |