# Rearrange Array Elements by Sign

Difficulty: medium
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 20 minutes

### Initial Approach

I tried solving this using the logic of the **"Sort Array by Parity II"** problem by:

- Taking two pointers:
    - `i` for even indexes.
    - `j` for odd indexes.
- The idea was:
    - If `nums[i]` is positive, add it to the result.
    - If `nums[j]` is negative, add it right after the positive one.
- Skip either pointer if the value at its index doesn't meet the condition.
- But I wasn’t able to conjure up a working solution using this logic.

---

### Using the Hint

I saw a hint that suggested dividing the array into two separate arrays:

- One for **positive numbers**.
- One for **negative numbers**.

Then construct the final result array:

- Use a loop like:
    
    ```cpp
    while (i < pos.size() && j < neg.size())
    
    ```
    
    - In each iteration, add `pos[i]`, then `neg[j]` to the result.
    - Increment both `i` and `j`.
- After the loop, handle any remaining elements in `pos` or `neg` by separate `while` loops:
    
    ```cpp
    while (i < pos.size()) result.push_back(pos[i++]);
    while (j < neg.size()) result.push_back(neg[j++]);
    
    ```
    
- Finally, return the result array.

---

### Time and Space Complexity

- **Time Complexity**: `O(n)`
- **Space Complexity**:
    - Let `p = pos.size()`, `n = neg.size()`, and `r = result.size()`
    - Then space complexity is: `O(p + n + r)`
    - Which is **higher than the optimal solution** in terms of space, but still acceptable and easy to understand.

Let me know if you want this formatted for Notion or turned into a code template.