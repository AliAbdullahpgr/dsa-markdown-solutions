# Best time to Buy and Sell Stocks

Difficulty: easy
 : Yes
: June 21, 2025
Problem: array, dynamic programming, two pointers
Time Taken: 20 minutes

## Best Time to Buy and Sell Stock — Two Pointer (Greedy) Approach

### 📘 Problem Recap:

You’re given an array `prices[]` where `prices[i]` is the stock price on the `i-th` day.

You need to **buy once and sell once**, and return the **maximum profit**.

If no profit is possible, return `0`.

---

### 🧠 Your Idea:

We want to:

- **Buy at a low price**
- **Sell at a higher price later**

Example:

```cpp
prices = [7, 1, 5, 3, 6, 4]

```

Best option:

- Buy at `1` (index 1)
- Sell at `6` (index 4)
- Profit = `6 - 1 = 5` ✅

Other options:

- Buy at 1, sell at 5 → profit = 4
- Buy at 1, sell at 4 → profit = 3
    
    ➡️ So, max is **5**
    

---

### 🧭 Two Pointer Intuition

We use:

```cpp
left = 0;   // buying day
right = 1;  // selling day

```

We slide `right` forward to explore selling opportunities and update `left` only when we find a **better (lower)** price to buy.

---

### 🔄 Why do we write `left = right`?

Good question.

We do:

```cpp
if (prices[left] >= prices[right]) {
    left = right;
}

```

**Explanation:**

- If `prices[right]` is **less than or equal to** `prices[left]`, it means this day is **cheaper** than our current buying day.
- So we **update the buy day** by moving `left` to `right` to buy at a **lower price**.
- We want to **always buy at the lowest possible price** before selling.

---

### 🔁 Loop Ends:

We only move `right++` in every iteration. So eventually, `right` hits the end of array.

Loop condition is:

```cpp
while (right < prices.size())

```

This ensures we stop after checking all possible sell days.

---

### ✅ Clean Code:

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int left = 0;  // buy
        int right = 1; // sell
        int maxProfit = 0;

        while (right < prices.size()) {
            if (prices[left] < prices[right]) {
                int profit = prices[right] - prices[left];
                maxProfit = max(maxProfit, profit);
            } else {
                // found a lower price to buy at
                left = right;
            }
            right++;
        }

        return maxProfit;
    }
};

```

---

### ✅ Dry Run:

For `prices = [7, 1, 5, 3, 6, 4]`

| left | right | prices[left] | prices[right] | Action | maxProfit |
| --- | --- | --- | --- | --- | --- |
| 0 | 1 | 7 | 1 | 1 < 7 → `left = right` | 0 |
| 1 | 2 | 1 | 5 | 5 > 1 → profit = 4 | 4 |
| 1 | 3 | 1 | 3 | 3 > 1 → profit = 2 | 4 |
| 1 | 4 | 1 | 6 | 6 > 1 → profit = 5 ✅ | 5 |
| 1 | 5 | 1 | 4 | 4 > 1 → profit = 3 | 5 |

---

### 🧠 Key Points:

- Use two pointers to track best **buy** and **sell** days.
- If we find a lower price → update `left` to `right` (new best day to buy).
- Only **one pass** through the array → efficient.

---

### ⏱ Time & Space:

- **Time:** `O(n)`
- **Space:** `O(1)`