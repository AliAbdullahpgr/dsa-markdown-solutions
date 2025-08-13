# String Compression

Difficulty: medium
 : Yes
: June 23, 2025
Problem: string, two pointers
Time Taken: 30 minutes

## Problem Understanding

Given a character array `chars`, compress it **in-place** such that:

- Repeated characters are replaced with the character followed by the count.
- Only consecutive repeats count.
- You must return the **new length** of the array.
- Do not use extra space for another array.

---

## ❌ Initial Intuition — HashMap

### Thought:

Use a `hashmap` to store frequencies of characters.

### Why it doesn't work:

- Hashmaps store **total frequency**, not **consecutive frequency**.
- Example:
    
    ```cpp
    chars = ['a','a','a','b','b','b','a']
    
    ```
    
    Using a hashmap → `'a': 4, 'b': 3` → compression: `['a','4','b','3']` → ❌ **Wrong**!
    

### Correct Output:

```cpp
['a','3','b','3','a']

```

Because the final `'a'` is a new run.

---

## ✅ Step 1 — Understand with Extra Array

To get the logic right, you initially used an **extra array** `s`:

### Core idea:

- Traverse the array.
- Count consecutive characters.
- On encountering a new character:
    - Add the previous character and its count (if > 1) to the result.

### Code:

```cpp
vector<char> compress(vector<char>& chars) {
    vector<char> s;
    int count = 1;

    for (int i = 1; i < chars.size(); i++) {
        if (chars[i] == chars[i - 1]) {
            count++;
        } else {
            s.push_back(chars[i - 1]);
            if (count > 1) {
                string k = to_string(count);
                for (char c : k) s.push_back(c);
            }
            count = 1;
        }
    }

    // Handle the last character
    s.push_back(chars.back());
    if (count > 1) {
        string k = to_string(count);
        for (char c : k) s.push_back(c);
    }

    chars = s;
    return s.size();
}

```

### Issue:

- Uses extra space (`s`), which is not allowed.

---

## ✅ Step 2 — In-Place Solution Using Index Pointer

Now we remove the extra array and do it in-place.

### Concept:

- Use a pointer `index` to write into the same array.
- Use a loop to count repeats.
- Add the character at `index`, followed by its count (if > 1).

### Call it: **Unique Pointer Index Approach** (not slow/fast)

---

### Code:

```cpp
class Solution {
public:
    int compress(vector<char>& chars) {
        int index = 0;
        int count = 1;
        for (int i = 1; i < chars.size(); i++) {
            if (chars[i]==chars[i-1]) {
                count++;
            } else {
                chars[index++] = chars[i - 1];
                if (count > 1) {
                    string k = to_string(count);
                    for (char c : k) {
                        chars[index++] = c;
                    }
                }
                count = 1;
            }
        }
        chars[index++] = chars.back();
        if (count > 1) {
            string k = to_string(count);
            for (char c : k) {
                chars[index++] = c;
            }
        }
        chars.resize(index);
        return index;
    }
};

```

---

### 🔁 Similar Problems (to revisit from Notion):

- **Remove Duplicates from Sorted Array**
- **Move Zeros**

Both use the same pattern of "overwrite in-place using index pointer."

---

## ✅ Final Thoughts

- Hashmap is **not suitable** for problems requiring **consecutive counting**.
- Always understand the **nature of repetition** (consecutive vs global).
- Learning with an extra array first is okay for understanding.
- The "unique index pointer" approach is clean and efficient.

---