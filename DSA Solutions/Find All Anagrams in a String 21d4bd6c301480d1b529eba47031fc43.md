# Find All Anagrams in a String

Difficulty: medium
 : Yes
: June 25, 2025
Problem: sliding window, string
Time Taken: 20-25 minutes

### 🧠 **My Brute Force Attempt (What I Tried First)**

- I first **sorted the string `p`**.
- Then I created a new string `k` for every window of size `p.size()` from `s`.
- I sorted `k` and compared it with sorted `p`.
- If they matched, I pushed the index `i` into the answer array.

```cpp
string p_sorted = p;
sort(p_sorted.begin(), p_sorted.end());

for (int i = 0; i <= s.size() - p.size(); ++i) {
    string k = s.substr(i, p.size());
    sort(k.begin(), k.end());
    if (k == p_sorted) {
        ans.push_back(i);
    }
}

```

- This worked well for small inputs but gave **TLE (Time Limit Exceeded)** for large inputs.
- I realized the time complexity was around **`O(n * k log k)`**, which is too slow for large test cases.

---

### 🤖 ChatGPT's Suggested Optimized Approach

ChatGPT suggested using a **frequency counter approach with Sliding Window**.

### 📺 I Visualized and Dry-Run the Solution:

- Used **two arrays of size 26**:
    - One for `p`'s character frequencies: `freq[26]`
    - One for current window over `s`: `window[26]`
- First step: initialize both with the first `p.size()` elements.

```cpp
for (int i = 0; i < p.size(); i++) {
    freq[p[i] - 'a']++;
    window[s[i] - 'a']++;
}

```

- Now, compare both arrays:
    - If they’re equal → it’s an anagram → push `0` into the result.

### 🪟 Now Sliding the Window:

- For each index `i` starting from `p.size()` to `s.size()`:
    - Remove the character going out of the window: `s[i - p.size()]`
    - Add the character coming into the window: `s[i]`
    - Compare the `window` array with `freq`
    - If equal → push the starting index of the window

### 🤯 The Confusing Part: Why `i - p.size() + 1`?

- Our window size is `p.size()`.
- At index `i`, the new window ends at `i` and starts at `i - p.size() + 1`.
- So to **push the starting index of the window**, we use:

```cpp
ans.push_back(i - p.size() + 1);

```

- This ensures it's **0-based indexing** and **aligned with window start**.

---

### ✅ Final C++ Code (Sliding Window + Frequency Array)

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        if (s.size() < p.size()) return {};

        vector<int> freq(26, 0), window(26, 0), ans;

        // fill initial frequencies
        for (int i = 0; i < p.size(); ++i) {
            freq[p[i] - 'a']++;
            window[s[i] - 'a']++;
        }

        // check initial window
        if (freq == window) ans.push_back(0);

        // slide the window
        for (int i = p.size(); i < s.size(); ++i) {
            window[s[i] - 'a']++; // new character in
            window[s[i - p.size()] - 'a']--; // old character out

            if (freq == window)
                ans.push_back(i - p.size() + 1); // push window start
        }

        return ans;
    }
};

```

---

### 🧩 Time & Space Complexity

- **Time Complexity:** `O(n)`
    
    Every character is processed once.
    
- **Space Complexity:** `O(1)`
    
    Only 2 arrays of size 26 are used.
    

---