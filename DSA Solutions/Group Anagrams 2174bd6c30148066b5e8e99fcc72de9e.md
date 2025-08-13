# Group Anagrams

Difficulty: medium
 : Yes
: June 19, 2025
Problem: array, hashtable/freq method
Time Taken: 30 minutes

## 🧩 Problem Summary

We are given a list of strings, and we need to group all **anagrams** together.

An **anagram** is a word formed by rearranging the letters of another word.

---

## ❌ My Initial Attempt

I started by:

- Creating a **frequency map** of characters for each string.
- Then using a **nested loop** to compare strings `i` and `j` (`i ≠ j`).
- If the strings had the same frequency count, I added them to the same group.

```cpp
for (string s : strs) m[s]--; // used this to reduce character count
for (int j = 0; j < strs.size(); j++) {
    if (check(m, strs[j]) && i != j) {
        v[i].push_back(strs[j]);
        strs.erase(strs.begin() + j); // O(n)
    }
}

```

### ❗ Problem:

- `vector.erase()` is **O(n)**, and inside a loop, this becomes **O(n^2)**.
- **Inefficient** for large inputs → likely to give **TLE (Time Limit Exceeded)**.

---

## ✅ Better Approach – Sorting Strings

A more efficient idea:

- **Sort each string** and use the sorted version as a **key** in a hashmap.
- All anagrams will share the same sorted form.

### 🔧 Example:

Input: `["eat", "tea", "tan", "ate", "nat", "bat"]`

After sorting:

- `"eat"` → `"aet"`
- `"tea"` → `"aet"`
- `"tan"` → `"ant"`
- `"ate"` → `"aet"`
- `"nat"` → `"ant"`
- `"bat"` → `"abt"`

### 📦 Map:

```cpp
aet → ["eat", "tea", "ate"]
ant → ["tan", "nat"]
abt → ["bat"]

```

Then return all values in the map as 2D vector.

### 🕒 Time Complexity:

```
O(m * n log n)
m = number of strings
n = average length of each string

```

---

## 💡 Most Optimal Approach – Frequency Count (No Sorting)

We can do **better** by avoiding sorting.

### 💥 Key Insight:

- Create a **frequency vector of size 26** for each string.
- Use that vector to create a **unique key**.
- All anagrams will have the **same frequency vector**, hence same key.

### 🧠 Genius Step:

- Turn the frequency vector into a string using `#` as a separator.
- This ensures uniqueness of keys like:

```cpp
for (char c : s) freq[c - 'a']++;

string key;
for (int i = 0; i < 26; i++) {
    key += to_string(freq[i]) + "#";
}

m[key].push_back(s); // group strings with same key

```

### 🔁 At the End:

- Return all `map[key]` values as the final result.

### 🕒 Time Complexity:

```
O(m * n), where:
m = number of strings
n = average string length (we do 26 operations per string)

```

This is **faster than sorting** and is the **most optimal solution**.

---

## ✅ Summary of All Approaches

| Approach | Technique | Time Complexity | Space | Notes |
| --- | --- | --- | --- | --- |
| Brute-force | Nested loop + erase | O(n² * k) | High | TLE on large inputs |
| Sorted key (mapping) | sort + map | O(m * n log n) | Medium | Easier to implement |
| Frequency vector key | count + map | **O(m * n)** | High | **Best performance overall** |

---