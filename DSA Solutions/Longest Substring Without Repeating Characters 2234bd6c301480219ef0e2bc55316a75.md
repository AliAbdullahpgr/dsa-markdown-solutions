# Longest Substring Without Repeating Characters

Difficulty: medium
 : Yes
: July 1, 2025
Problem: array, sliding window, two pointers
Time Taken: 20-25 minutes

### 🚀 Goal:

Find the **length of the longest substring** in `s` that has **all unique characters**.

---

### 🔧 Approach (Sliding Window with Set):

- Use **two pointers** `left` and `right` to form a sliding window.
- Use an **unordered_set window** to keep track of characters inside the current window.
- Expand the window by moving `right`, and **shrink it from the left** if you find a duplicate.
- After every valid step, update the max length.

---

### 🧠 Step-by-Step Logic:

- Initialize:
    
    `int left = 0, len = 0;`
    
    `unordered_set<char> window;`
    
- Loop through the string with `right` pointer:
    - While `s[right]` is in the set → we have a duplicate.
        - Keep removing `s[left]` from the set and move `left++` until `s[right]` is no longer in the set.
    - Now `s[right]` is unique in current window:
        - Add `s[right]` to the set.
        - Update `len` with `right - left + 1`.

---

### ✅ Final Code (Cleaned & Sharp):

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int left = 0, len = 0;
        unordered_set<char> window;

        for (int right = 0; right < s.size(); right++) {
            while (window.count(s[right])) {
                window.erase(s[left]);
                left++;
            }
            window.insert(s[right]);
            len = max(len, right - left + 1);
        }

        return len;
    }
};

```

---

### ⏱️ Time & Space:

- **Time:** O(n) — each character is visited at most twice (once by `right`, once by `left`)
- **Space:** O(min(n, m)) — for the `unordered_set` (`m` is charset size)

---

### 🧪 Example:

Input: `"abcabcbb"`

Valid substrings: `"abc"`, `"bca"`, `"cab"`

Longest = `"abc"` → length = `3`