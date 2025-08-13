# Find Minimum in Rotated Sorted Array

Difficulty: medium
 : Yes
: August 13, 2025
Problem: array, binary search
Time Taken: 25 minutes

## **1. Wrong base case check**

**Code:**

```cpp
if (end == 1) return nums[0];

```

or

```cpp
if (nums[start] < nums[end]) return nums[start];

```

**Issue:**

- `end == 1` is meaningless unless the array has exactly two elements.
- The second form is correct **only if** the array is already sorted, but you used it in a version where other logic didn’t account for rotation correctly.

**Lesson:**

Check `nums[start] < nums[end]` to detect already sorted arrays, but ensure your binary search handles all other rotations.

---

## **2. Out-of-bounds access**

**Code:**

```cpp
if (nums[mid - 1] > nums[mid]) { ... }

```

**Issue:**

When `mid == 0`, `nums[mid - 1]` is invalid.

**Lesson:**

Avoid direct neighbor comparisons in binary search unless you handle `mid == 0` and `mid == n - 1` explicitly. It’s safer to decide direction using `nums[mid]` vs `nums[end]`.

---

## **3. Skipping the minimum**

**Code:**

```cpp
else if (nums[mid] <= nums[end]) {
    end = mid - 1;
}

```

**Issue:**

- If `mid` is the actual minimum, `end = mid - 1` will skip over it.
- You must keep `mid` in the search space when it **could** be the answer → use `end = mid` instead.

**Lesson:**

When the mid value could still be the answer, don’t exclude it from the range — shrink the boundary towards it.

---

## **4. Infinite loop when `start == end`**

**Code:**

```cpp
while (start <= end) {
    ...
    else if (nums[mid] <= nums[end]) {
        end = mid; // if mid == end, no progress → infinite loop
    }
}

```

**Issue:**

- Using `<=` with `end = mid` can cause no movement when `mid == end`.

**Lesson:**

Use `while (start < end)` so the loop stops when `start == end`. This is the standard binary search pattern for finding a single point.

---

## **5. Wrong comparisons in dry runs**

From the `[3, 1, 2]` walkthroughs:

- You sometimes assumed `nums[mid] > nums[end]` when it was false or vice versa.
- This led to wrong boundary updates and incorrect results.

**Lesson:**

Dry run carefully with explicit `start`, `end`, `mid`, and value checks at each step. Write them down to spot logic errors.

---

## **6. Final working pattern**

**Correct structure:**

```cpp
int findMin(vector<int>& nums) {
    int start = 0, end = nums.size() - 1;
    while (start < end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] > nums[end]) {
            start = mid + 1;  // min in right half
        } else {
            end = mid;        // min in left half (or mid itself)
        }
    }
    return nums[start];
}

```

**Why it works:**

- The search space always shrinks.
- No out-of-bounds.
- Keeps potential minimum inside range.
- Handles all rotations, including no rotation.