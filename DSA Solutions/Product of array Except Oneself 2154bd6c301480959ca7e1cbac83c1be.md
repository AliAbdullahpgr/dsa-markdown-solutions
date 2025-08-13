# Product of array Except Oneself

Difficulty: medium
 : Yes
: June 17, 2025
Problem: array, prefixSum
Time Taken: 30 minutes

## 🔹 Prefix Sum (Product Version) Problem Explanation

I learned the **prefix sum method** just to solve this problem.

I used **Type 1** in the Prefix Notion Page to solve it by making two arrays:

- A **prefix array**
- A **suffix array**

---

### 🧪 Example: Array = `{1, 2, 3, 4}`

- The **prefix** would be:

```cpp
prefix = {1, 2, 6, 24}

```

- And the **suffix** would be:

```cpp
suffix = {24, 24, 12, 4}

```

I thought dividing the larger value by the smaller one would get me the solution.

But the problem explicitly — and rightly so — **states not to use division**

since it causes **division by zero errors**.

---

### ✅ Correct Approach: Type 2 from the Prefix Notion Page

The correct way to solve this problem would be **Type 2** of the Prefix method.

- The size of the prefix is equal to the array.
- It's initialized with the value `1` because of how multiplication works.

```cpp
prefix[i] = prefix[i - 1] * nums[i - 1];

```

This approach gives the **product of elements before `i`**,

which is the real crux of the solution — **left ⟶ oneself ⟶ right**

We can simply return `left * right`.

---

### 🧠 Key Insight

Solving **left and right sum-difference problems** can be an eye-opener for this.

Coming back to the point:

- `prefix[i]` is the **product of elements to the left** of `nums[i]`
- That’s why it's **1-indexed** — so the prefix of `4` in `{1, 2, 3, 4}` is `1 * 2 * 3 = 6`

Similarly, we compute the **suffix**, which is the **product to the right** of `nums[i]`

- It's also **Type 2 suffix** from the Prefix Sum notion page.
- `suffix` is the same size as the array and initialized with `1`.

This is done to ensure `x * 1 = x`, and avoids undefined behavior.

So for the element `2` in array `{1, 2, 3, 4}`, the suffix is `3 * 4 = 12`.

---

### 🔚 Final Result

We simply return:

```cpp
result[i] = prefix[i] * suffix[i];

```

For `{1, 2, 3, 4}`, the result would be:

```cpp
result = {24, 12, 8, 6}

```

---

### ⏱️ Complexity

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n)`
    
    *(Can be optimized further)*
    

### Another Approach (Using Two Counters)

We use:

- `zeroCount` → to count the total number of **zeros** in the array
- `totalProduct` → to store the product of all **non-zero** elements

---

### 🔍 Logic:

- If `zeroCount > 1`:
    - All values in the result array will be **0**
    - Because every element’s product will include at least one zero
- If `zeroCount == 1`:
    - Only the element **which is zero** in the original array gets the `totalProduct`
    - All other elements will be 0 because their product includes that one zero
- If `zeroCount == 0`:
    - No zeros → normal case
    - For each element, just do: `totalProduct / num`

---

### 💻 Code:

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int totalProduct = 1;
        int zeroCount = 0;

        for (int num : nums) {
            if (num == 0) {
                zeroCount++;
            } else {
                totalProduct *= num;
            }
        }

        vector<int> result;

        for (int num : nums) {
            if (zeroCount > 1) {
                result.push_back(0);
            }
            else if (zeroCount == 1) {
                result.push_back(num == 0 ? totalProduct : 0);
            }
            else {
                result.push_back(totalProduct / num);
            }
        }

        return result;
    }
};

```

---

### 📦 Time & Space Complexity:

- **Time:** `O(n)` – One pass for product + one pass to build result
- **Space:** `O(n)` – For result array

---