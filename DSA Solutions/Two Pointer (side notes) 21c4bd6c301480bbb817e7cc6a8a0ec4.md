# Two Pointer (side notes)

: No

# Two Pointers

> Two-pointer technique means using two index variables, possibly on the same or different arrays, that move with some logic to solve a problem efficiently, usually in linear time.
> 

---

### 🔧 So what’s allowed?

| Situation | Is it two-pointer? | Why |
| --- | --- | --- |
| Two pointers on same array | ✅ | Common case (e.g., palindrome, reverse, two-sum) |
| One on each of two arrays | ✅ | Used in merging, intersection, etc. |
| One pointer reads, one writes | ✅ | If both work in coordination (e.g., move zeroes) |
| One pointer decides, other follows | ✅ | Still valid |
| Using a third pointer (e.g., result writer) | ✅ | Still “two-pointer” *if only two are doing core logic* |

---

## 🎯 What Actually Matters?

Not where the pointers are, but:

- Are **two pointers** working together?
- Are they moving **with a rule**?
- Are they solving a problem in a **linear pass**?

---

## 🧾 Final Clean Answer (No BS)

> Two-pointer technique is any algorithm where two indexes (on same or different arrays) interact directly or indirectly to solve a problem more efficiently than brute-force — especially when each pointer moves linearly.
> 

✅ Same array → fine

✅ Different arrays → still fine

✅ Third pointer (like a writer)? → fine, if it’s not part of decision logic

**Brute-force** means solving a problem by trying **all possible options**, without using any optimization, shortcuts, or smart tricks.

# ✅ When to Use Two Pointers — Master Rule List

---

### 1. **When Comparison of Two Indexes is Required**

- ✅ Comparing values like `arr[i]` and `arr[j]`
- Examples: checking equality, sum, order, difference, etc.
- [**977. Squares of a Sorted Array**](https://leetcode.com/problems/squares-of-a-sorted-array/)
- [**125. Valid Palindrome**](https://leetcode.com/problems/valid-palindrome/description/)
- [**283. Move Zeroes**](https://leetcode.com/problems/move-zeroes/description/)

---

### 2. **When You Need to Scan From Both Ends - comparison inc.**

- ✅ Start from left and right (like `i = 0`, `j = n-1`)
- Examples: reversing, palindrome, max area in container
- [**189. Rotate Array**](https://leetcode.com/problems/rotate-array/description/)
- [**344. Reverse String**](https://leetcode.com/problems/reverse-string/)
- [**345. Reverse Vowels of a String**](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)
- [**125. Valid Palindrome**](https://leetcode.com/problems/valid-palindrome/description/)

---

### 3. **When You Want to Avoid Nested Loops**

- ✅ Replacing brute-force O(n²) by coordinated movement of two pointers
- Example: avoiding checking all pairs
- [**189. Rotate Array**](https://leetcode.com/problems/rotate-array/description/)

---

### 4. **When You’re Building or Filtering in the same Place (Array/String)**

- ✅ One pointer reads, one writes
- Example: remove duplicates, move zeroes, compress array
- [**283. Move Zeroes**](https://leetcode.com/problems/move-zeroes/description/)
- [**189. Rotate Array**](https://leetcode.com/problems/rotate-array/description/)
- [**344. Reverse String**](https://leetcode.com/problems/reverse-string/)

---

### 6. **When You’re Merging or Comparing Two Sorted Lists**

- ✅ Each pointer on a different array
- Compare or merge in sorted order efficiently
- [**392. Is Subsequence**](https://leetcode.com/problems/is-subsequence/description/)
- [**1768. Merge Strings Alternatel**](https://leetcode.com/problems/merge-strings-alternately/description/)

---

### 7. **When You Know the Input is Sorted or Can Be Sorted**

- ✅ Sorting + two-pointer = most common combo
- Enables you to eliminate large portions of the data intelligently
- [**392. Is Subsequence**](https://leetcode.com/problems/is-subsequence/description/)

---

### 8. **When You’re Working With Symmetry**

- ✅ Like comparing mirror elements (`arr[i] vs arr[n-1-i]`)
- E.g., palindrome, mirrored structure
- [**125. Valid Palindrome**](https://leetcode.com/problems/valid-palindrome/description/)