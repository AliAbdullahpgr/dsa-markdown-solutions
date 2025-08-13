# Sort Array by Parity II

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 10-20 minutes

### Sort Array by Parity II

This problem asks us to **sort the array in terms of parity** too, but specifically states that:

- **Elements should be even at even indexes**
- **Elements should be odd at odd indexes**

---

### 🧠 Key Insight

We get to know how to solve this problem by noticing that:

- There are **equal numbers of even and odd elements** in the array.

---

### 🚀 Approach – Two Pointer

We can simply solve this problem using the **two pointer approach**:

- We need a pointer for **even indexes**
- And a pointer for **odd indexes**

For example, if an array has indexes `0 1 2 3 4`,

then:

- `0, 2, 4` are **even indexes**
- `1, 3` are **odd indexes**

Let `i` be the pointer for even indexes and `j` for odd indexes.

---

### 🔄 Loop Logic

- If both the **index and element** are even, or both are odd → simply skip (i.e., `i += 2` or `j += 2`)
- While iterating, make sure `i` and `j` are **less than the size** of the array
- The **main important part** of the code:
    - If there is an **odd element at an even index** and an **even element at an odd index**, then **swap them**

---

### 🕒 Time and Space Complexity

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)