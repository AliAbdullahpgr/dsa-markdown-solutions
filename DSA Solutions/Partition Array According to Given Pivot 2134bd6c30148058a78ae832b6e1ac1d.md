# Partition Array According to Given Pivot

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 30 minutes

### My Solution to the Pivot Array Problem

```cpp
class Solution {
public:
    vector<int> pivotArray(vector<int>& nums, int pivot) {
        vector<int> arr;
        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] < pivot) {
                arr.push_back(nums[i]);
            }
        }
        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] == pivot) {
                arr.push_back(nums[i]);
            }
        }
        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] > pivot) {
                arr.push_back(nums[i]);
            }
        }
        return arr;
    }
};

```

---

### 💬 My Thoughts on This Solution

- This solution of mine is **so much better** — honestly, it feels superior.
- I initially tried solving it using the **two-pointer technique**, but it wasn’t possible in **O(1) space**.
    
    Swapping operations change the original positions of elements, and it just messes things up.
    

---

### 🔀 Alternative Approaches I Considered

- Creating three arrays:
    
    **`lessThan`**, **`equalTo`**, and **`greaterThan`**
    
    Then merging them at the end.
    
    > But my solution basically does this in a cleaner way without explicitly naming the arrays.
    > 
- The two-pointer solution I found later involves:
    - Creating a **`result`** array
    - Using two pointers `left` and `right`
    - Placing elements `< pivot` on the left
    - Placing elements `> pivot` on the right
    - Then inserting all elements `== pivot` just after the `left` section
    
    But honestly? **My approach is much simpler and more readable.**
    

---

### Final Reflection

- I spent **30 minutes** trying to solve this in a different way for no real gain.
- I’m glad I stuck to this version — it worked cleanly, it was readable, and it got the job done.
- It’s a great reminder: Sometime the first solution is the best one