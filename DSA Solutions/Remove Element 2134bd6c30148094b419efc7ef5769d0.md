# Remove Element

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 10-20 minutes

### Two Approaches to Solve This Problem

- **First Approach:**
    
    Use another array to store all the values that are **not equal to `val`**, and return the size of that new array.
    
    This is the approach I initially coded.
    
- **Second (Better) Approach:**
    
    This one is more efficient and uses the **two-pointer technique**, which I wasn’t able to fully understand at first.
    
    Here's what I learned:
    
    - You need a pointer `k` that keeps track of where to place the next non-`val` element.
    - At the same time, use a pointer `i` to traverse the entire array.
    - The part that confused me was that **you don’t need to erase anything** from the array.
    - Even if the array contains multiple occurrences of `val`, you can **simply skip them**.
    - Whenever you find a value that is **not equal to `val`**, you **place it at index `k`**, like this:
        
        ```cpp
        nums[k++] = nums[i];
        
        ```
        
    - At the end, `k` represents the **number of elements not equal to `val`**, and you return that.

---