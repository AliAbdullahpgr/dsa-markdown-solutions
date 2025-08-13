# Permutation in String

Difficulty: medium
 : Yes
: July 2, 2025
Problem: array, hashtable/freq method, sliding window
Time Taken: 20 minutes

### ✅ Problem Summary

We are given two strings: `s1` and `s2`.

- We need to check if **any permutation of `s1` exists in `s2`** as a **substring**.
- For example, if `s1 = "ab"` and `s2 = "eidbaooo"`, then `"ba"` is a permutation of `"ab"` and is present in `s2`.

---

### 🧠 How to Think About It

- This is a **sliding window problem**.
- Ask yourself: *Is it a fixed-size or variable-size window?*
    
    → Since we want to match the permutation of `s1`, which is of fixed length `k = s1.size()`, the **window size is fixed**.
    

---

### 🧰 Technique Used

- Use **frequency count arrays** for comparison:
    - One for `s1` → what we want to find.
    - One for the current window in `s2`.
- This is better than maps for this problem:
    - Space complexity is **O(1)** since we only use arrays of size 26 (for lowercase letters).

---

### 🪟 Sliding the Window

- Step 1: Initialize two vectors of size 26 (for lowercase letters).
- Step 2: Fill both `freq` (for `s1`) and the first window in `s2`.
- Step 3: Check if both frequency arrays match → if yes, return `true`.
- Step 4: Slide the window over `s2`:
    - Add the next character.
    - Remove the character that falls out of the window.
    - Compare again.
- Step 5: If no match is found, return `false`.

---

### ✅ Final Code

```cpp
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        if(s1.size() > s2.size()) return false;

        vector<int> freq(26, 0);     // Frequency of s1
        vector<int> window(26, 0);   // Frequency of current window in s2

        int k = s1.size();           // Fixed window size

        // Initialize both freq and window for the first k characters
        for(int i = 0; i < k; i++) {
            freq[s1[i] - 'a']++;
            window[s2[i] - 'a']++;
        }

        // Check first window
        if(freq == window) return true;

        // Slide the window
        for(int i = k; i < s2.size(); i++) {
            window[s2[i] - 'a']++;       // Add new character
            window[s2[i - k] - 'a']--;   // Remove old character

            if(freq == window) return true;
        }

        return false;
    }
};

```

---

### 🎯 Final Thoughts

- **Really solvable** and **enjoyable** problem.
- Shows the power of **frequency counting** + **fixed-size sliding window**.
- Elegant solution with **O(n)** time and **O(1)** space.