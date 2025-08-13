# Longest Palindrome

Difficulty: easy
 : Yes
: June 20, 2025
Problem: array, hashtable/freq method, sort
Time Taken: 10-20 minutes

### 🧩 Longest Palindrome Problem — My Thought Process

The **longest palindrome** problem was really interesting to solve. I used the **frequency count method** to count the frequency of each element in the string.

There are **two kinds of frequencies** we see:

- **Even frequencies**
- **Odd frequencies**

---

### 🛠️ Step-by-Step Explanation:

### 🔹 1. Count Frequencies:

First, I counted how many times each character occurs using a `map`.

```cpp
unordered_map<char,int>m;
for(auto i: s) m[i]++;

```

For example, if the input is `"abccccdd"`

the frequency map would be:

```
a = 1
b = 1
c = 4
d = 2

```

---

### 🔹 2. Handling Even Frequencies:

All **even frequencies** can be used directly in the palindrome. So for each character, if the frequency is even, I simply added it to `count`:

```cpp
if(i.second % 2 == 0) {
    count += i.second;
}

```

---

### 🔹 3. The Problem with Odd Frequencies:

At first, I thought I only needed the **largest odd frequency**, so I wrote something like:

```cpp
if(pair.second % 2 == 1 && odd < pair.second)
    odd = pair.second;

```

But I realized that was **wrong**.

Why? Because we can take part of **every odd frequency**, just not the full number.

So if a character has a frequency like `3`, `5`, etc., we can take `freq - 1` from it (like `3-1 = 2`, `5-1 = 4`, etc.).

So I updated my logic to:

```cpp
if(i.second % 2 == 1) {
    odd += i.second - 1;
    alt = true; // remember that an odd frequency was found
}

```

---

### 🔹 4. One Central Odd Character:

Now another problem arises. If there is **any odd frequency**, we can place **just one** character in the **center** of the palindrome. This will make the total palindrome length longer by `+1`.

So I used a boolean (`alt`) to track if **any** odd was found. If yes, I added `1` to `odd`.

```cpp
if(alt) {
    odd++;
}

```

---

### 🔹 5. Final Total:

At the end, I combined the even parts (`count`) and the processed odd part (`odd`) like this:

```cpp
count += odd;

```

---

### 📦 Final Code:

```cpp
class Solution {
public:
    int longestPalindrome(string s) {
        unordered_map<char,int>m;
        for(auto i: s) m[i]++;

        int odd = 0;
        int count = 0;
        bool alt = false;

        for(auto i : m) {
            if(i.second % 2 == 1) {
                odd += i.second - 1;
                alt = true;
            } else {
                count += i.second;
            }
        }

        if(alt) {
            odd++;
        }

        count += odd;
        return count;
    }
};

```

---

### 🔚 Summary:

- Count all characters.
- Use all even frequencies completely.
- From odd frequencies, use `freq - 1`.
- If any odd exists, add `1` to place a central character.
- Final result = total of even parts + adjusted odd parts.

This made the whole idea click for me — the center character from an odd frequency is what gives the final +1 advantage.