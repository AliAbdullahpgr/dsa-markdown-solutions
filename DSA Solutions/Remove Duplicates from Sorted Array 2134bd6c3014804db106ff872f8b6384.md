# Remove Duplicates from Sorted Array

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 5 minutes

### Problem with this problem

This problem was really easy to code up since I had solved a similar one before.

- At first, I saw this as a hashtable problem.
- I just needed to take a hashset and add all the values into it.
- Since a hashset only stores unique values, any duplicates would be automatically removed.
- Then, I would add the values from the hashset back into the `nums` array.

### Drawback of This Approach

- This approach uses extra space for the hashset.
- Although it works, it's not optimal in terms of space complexity.

### A Better Approach

A better and easier-to-understand solution is:

- Create a separate array called `result`.
- Iterate through the `nums` array.
- For each element, check if `arr[i] != arr[i + 1]`. If so, add `arr[i]` to the `result` array.

### Important Edge Cases to Handle

Make sure to account for two things:

- When using `arr[i + 1]`, ensure:
    
    ```cpp
    i < nums.size() - 1
    
    ```
    
    This avoids going out of bounds during the last iteration.
    
- add the last `arr[i]` where `i = nums.size() - 1` to the `result` array as well.

### Final Step

- Return the size of the `result` array using `result.size()`.