# Range Sum Query - Immutable

Difficulty: easy
 : Yes
: June 17, 2025
Problem: array, prefixSum
Time Taken: 10-20 minutes

## 🔹 Range Sum Query - Immutable

Actually, this is a pretty easy problem to solve.

We need to **find the sum between two indices** — `left` and `right` — for a given array.

---

### 🔸 Naive Approach

- We can solve it by using a simple `while` loop:

```cpp
int sum = 0;
while (left <= right) {
    sum += arr[left];
    left++;
}
return sum;

```

- This approach has **O(n)** time complexity per query.
- It's already optimal *for one-time queries*, but...

---

### ⚠️ Problem

> The array is initialized once in the constructor,
> 
> 
> but the `sumRange()` function is called **multiple times**.
> 

So calculating the sum every time using a loop becomes inefficient.

---

### ✅ Optimized Approach: Prefix Sum

We can **precompute the prefix sum** of the array once during construction.

This way, the loop runs just one time, and every future query is handled in **O(1)** time.

---

### 🔧 Prefix Array Creation

If we are given:

```cpp
arr = {1, 2, 3, 4}

```

We create a prefix array like this:

```cpp
prefix = {1, 3, 6, 10}

```

Each element at index `i` in the prefix array stores the **sum of all elements from index `0` to `i`**.

---

### 📌 Querying Sum Using Prefix

To calculate `sumRange(left, right)`:

```cpp
if (left == 0)
    return prefix[right];
else
    return prefix[right] - prefix[left - 1];

```

---

### 🧪 Examples

```cpp
sumRange(0, 3) → returns prefix[3] = 10
sumRange(1, 3) → returns prefix[3] - prefix[0] = 10 - 1 = 9

```

> The elements between index 1 and 3 are 2 + 3 + 4 = 9 — which is correct.
> 

---

### 🧠 Final Thought

So we simply return the precomputed value.

This turns a repeated O(n) solution into a **single O(n) preprocessing + O(1) per query**,

which is much better when there are **many queries**.

You can also refer to the Notion page about prefix sum for more examples and use-cases.