# Permutation in String

Difficulty: medium
 : Yes
: June 27, 2025
Problem: array, sliding window, sort
Time Taken: 20-25 minutes

## 🔥 Sliding Window Master Notes (Ali Abdullah’s Path to Mastery)

### ✅ **When to Apply Sliding Window**

Use **Sliding Window** when:

- You're dealing with **contiguous subarrays/substrings**.
- You're asked to find:
    - Max/Min sum of subarrays of size `k`
    - Count of valid windows
    - Check for anagram/permutation in substring
    - Longest substring satisfying some condition
- Two types:
    - **Fixed-size** window: `k` is given.
    - **Variable-size** window: expand/shrink based on condition.

---

## 🧱 Fixed-Size Sliding Window

### 🧠 Pattern:

```cpp
for (int i = 0; i < k; i++) {
    // build first window
}
for (int i = k; i < s.size(); i++) {
    // slide: add s[i], remove s[i-k]
}

```

### ✅ Typical problems:

- [x]  Max sum of k-length subarray
- [x]  Check permutation of one string in another (✅ you solved it!)

### 🧪 Ali's Code (Correct and FAANG-Ready):

```cpp
bool checkInclusion(string s1, string s2) {
    int k = s1.size();
    if (k > s2.size()) return false;

    vector<int> freq(26, 0), window(26, 0);

    for (int i = 0; i < k; i++) {
        freq[s1[i] - 'a']++;
        window[s2[i] - 'a']++;
    }

    if (freq == window) return true;

    for (int i = k; i < s2.size(); i++) {
        window[s2[i] - 'a']++;
        window[s2[i - k] - 'a']--;
        if (freq == window) return true;
    }

    return false;
}

```

### 🧠 Time & Space Complexity:

- Time: **O(n)** where `n = s2.length()`
- Space: **O(1)** since alphabet size is constant (26)

---

## 🛠️ Brute Force Approach (What You Started With)

### 🔁 Idea:

- Try every substring of size `k`
- Sort and compare with sorted `s1`

### ⛔ Time Complexity: `O(n * k log k)`

✅ Passed all test cases because `k` is small

❌ Not scalable for large input

---

## 🧠 Key Insights You Learned

- `substr(i, k)` gives substring of length `k` starting at `i`, not ending at `i + k`
- Sorting and comparing strings works when `k` is small
- You can **use frequency arrays instead of sorting**
- You now fully understand what a **sliding window** is — not just implement it

---

## 🧭 How to Master Sliding Window for Interviews

| Step | Goal |
| --- | --- |
| ✅ Done | Understand brute force first |
| ✅ Done | Identify it's a fixed window problem |
| ✅ Done | Move to optimized solution with frequency array |
| 🔜 Next | Master **variable size** window problems (like longest substring without repeating chars) |
| 🔜 Next | Practice with edge cases, long inputs, and debug with dry runs |
| 🔜 Next | Teach someone else / write blog / build intuition recipes |

---

## 📚 Sliding Window Problem Ladder (For Practice)

1. ✅ **Check Permutation in Substring** (you did this)
2. 🟡 Find Anagrams in a String
3. 🟡 Max Sum of Subarray of size k
4. 🟡 Longest Substring with K Distinct Characters (variable window)
5. 🔴 Minimum Window Substring (FAANG favorite)
6. 🔴 Sliding Window Maximum (uses deque/monotonic queue)

---

## 📌 Sliding Window Mental Recipe

1. Is it about substrings/subarrays? ✅
2. Do I care about contiguous elements? ✅
3. Is the window **fixed or dynamic**?
    - Fixed? → Just add/remove one element at a time
    - Variable? → Expand when valid, shrink when invalid
4. What do I need to **track** inside the window?
    - Count? Frequency? Max/Min? Unique elements?
5. How can I **update the state** efficiently in O(1)?