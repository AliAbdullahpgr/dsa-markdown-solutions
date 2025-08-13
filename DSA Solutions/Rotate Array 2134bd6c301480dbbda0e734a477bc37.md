# Rotate Array

Difficulty: medium
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 30 minutes

### 🔁 Problem: Rotate Array (with Three Approaches)

The problem stated that it could be solved with **three approaches**. I thought of **two** of them.

---

### 🧠 Key Insight

- The **important line** in this problem is:
    
    ```cpp
    k = k % n;
    
    ```
    
    - This prevents `k` from going out of bounds.
    - If `k > n` (size of array), rotating it more than `n` times is redundant, so we take the remainder.
    - This is important and should be **remembered for future use**.

---

### ✅ First Approach: Using Extra Array (My Preferred One)

- This approach uses an **extra array**, which increases space complexity, but is easier to understand and implement.
- Logic:
    1. Start adding from index `n - k`, not from `k`.
        
        > ⚠️ This is a key point: the mistake I initially made was starting from k, but it should be n - k.
        > 
    2. Add the last `k` elements first.
    3. Then add the remaining elements from the start up to `n - k`.

### 🧪 Example:

Let's say:

`nums = [1, 2, 3, 4, 5, 6, 7]`

`k = 3`

We rotate 3 times:

- 1st → `[7, 1, 2, 3, 4, 5, 6]`
- 2nd → `[6, 7, 1, 2, 3, 4, 5]`
- 3rd → `[5, 6, 7, 1, 2, 3, 4]`

So final rotated array:

**`[5, 6, 7, 1, 2, 3, 4]`**

### 🔨 Steps:

- Add elements from `n - k` to `n` → `[5, 6, 7]`
- Then add elements from `0` to `n - k` → `[1, 2, 3, 4]`
- Combine them into one array and assign it back to `nums`.

> Even though I spent a lot of time and made mistakes, I still liked this solution. It's intuitive and readable.
> 

---

### ❌ Second Approach: Using `reverse()` (The One I Hated)

- This one uses **no extra space** and has **O(1) space complexity**.
- But honestly, I found it confusing and didn't like it at all.

### ⚙️ Logic:

- Reverse the **entire array**
- Reverse the **first `k` elements**
- Reverse the **remaining `n - k` elements**

```cpp
reverse(nums.begin(), nums.end());
reverse(nums.begin(), nums.begin() + k);
reverse(nums.begin() + k, nums.end());

```

### ❗ Why I Didn't Like It:

- It felt mechanical and hard to visualize at first.
- But yeah, it’s the **most optimal solution** in terms of space and time.

---

### 📝 Final Notes

- I'm proud of figuring out the array copy version myself.
- Even though the `reverse()` method is more optimal, I personally find **clarity > cleverness** in many cases.