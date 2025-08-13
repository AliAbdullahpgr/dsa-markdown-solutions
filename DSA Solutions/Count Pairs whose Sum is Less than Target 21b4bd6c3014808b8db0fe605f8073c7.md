# Count Pairs whose Sum is Less than Target

Difficulty: easy
 : Yes
: June 23, 2025
Problem: array, two pointers
Time Taken: 20 minutes

## 📝 Notes: Counting Pairs with Two Pointers (`nums[i] + nums[j] < target`)

### 🔸 Problem Statement

Given a sorted or unsorted array `nums` and a `target`, count the number of **unique pairs** `(i, j)` where `i < j` and:

nums[i]+nums[j]<targetnums[i] + nums[j] < target

---

### 🔸 Two Pointer Technique (Sorted Input)

### ✅ Steps:

1. **Sort** the array.
2. Initialize two pointers:
    - `left = 0`
    - `right = nums.size() - 1`
3. While `left < right`:
    - Calculate `sum = nums[left] + nums[right]`
    - If `sum < target`:
        - All values from `nums[left+1]` to `nums[right]` paired with `nums[left]` are also valid.
        - So add `right - left` to the count.
        - Move `left++`
    - Else:
        - Move `right--` (because the sum is too big or equal)

---

### 📌 Key Intuition

- Since the array is sorted, `nums[right] >= nums[i]` for all `i` from `left+1` to `right`.
- So if `nums[left] + nums[right] < target`, then all smaller sums like `nums[left] + nums[right-1]`, `nums[left] + nums[right-2]`, ... will **also** be less than target.

---

### 📐 Formula

If:

nums[left]+nums[right]<target nums[left] + nums[right] < target

Then:

Count+=(right−left) {Count} += (right - left)

This represents the number of valid pairs with `nums[left]`.

---

### 💡 Why Not Use `abs(left - right)`?

You experimented with:

```cpp
count += abs(left - right);

```

It worked only because `left < right` is always true in the loop. But:

- `abs()` hides intent and may hide bugs.
- `right - left` is clearer and slightly faster.
- Use `abs()` only for understanding — not in final code.

✅ **Best practice**:

```cpp
count += right - left;

```

---

### 🔍 Visual Example

```cpp
nums = [1, 2, 3, 4, 5]
target = 7

left = 0 (1), right = 4 (5)
sum = 1 + 5 = 6 < 7 ✅

→ valid pairs:
(1,2), (1,3), (1,4), (1,5)
→ count += right - left = 4

```

---

### ❌ Common Mistake

Doing only `count++` when `sum < target`:

```cpp
if (sum < target) {
    count++;  // ❌ wrong
}

```

This misses all other valid combinations.

---

### 🧠 Definition Recap (Final Understanding)

> If the sum of the smallest (nums[left]) and largest (nums[right]) elements is less than target, then all pairs (nums[left], nums[i]) for i ∈ (left+1 to right) are also valid.
> 

So:

Count+=right−left {Count} += right - left