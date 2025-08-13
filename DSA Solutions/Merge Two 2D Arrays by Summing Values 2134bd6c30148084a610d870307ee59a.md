# Merge Two 2D Arrays by Summing Values

Difficulty: easy
 : Yes
: June 15, 2025 → June 16, 2025
Problem: array, hashtable/freq method, two pointers
Time Taken: 25 minutes

Solved Using Two Approaches

### 🔹 **Approach 1: Using Hash Table**

I first tried solving it using a **hash table**. I took a hashmap like:

```cpp
unordered_map<int, int> map;

```

- I pushed the values of the first 2D array into it like `id_i : value_i` and so on.
- Then I looped through the second 2D array and summed up the same values as required by the problem statement, like:

```cpp
m[nums2[i][0]] += nums2[i][1];

```

- This piece of code is very important as it first finds the values with the same IDs in the hashmap and then adds up their values.
- I then pushed all the values of the hashmap into a 2D array.

Now, this piece of code was really difficult for me to understand and I didn’t know how to do that. Apparently, you can use the keys and values in the map as a pair, so I used a loop like:

```cpp
for (auto& pair : map) {
    result.push_back({pair.first, pair.second});
}

```

- Then at the end, I sorted this 2D array with respect to the IDs using a simple `sort()` function.

But this increases the **time complexity to `O(n log n)`**, so it's really not optimized, and its **space complexity is high too**.

---

### 🔹 **Approach 2: Using Two Pointers**

I searched and found a better approach using **two pointers**, which goes like this:

- Take two pointers `i` and `j` starting with `0`
    - `i` is for traversing `nums1`
    - `j` is for traversing `nums2`
- Iterate through a while loop until either `i` or `j` becomes greater than the size of the two 2D arrays.
- Use a condition to check:
    
    ```cpp
    if (nums1[i][0] == nums2[j][0])
    
    ```
    
    → then add up the values in the new array `result` with the same ID, and do:
    
    ```cpp
    i++; j++;
    
    ```
    
- Then check:
    
    ```cpp
    if (nums1[i][0] < nums2[j][0])
    
    ```
    
    → as it needs to be in sorted order, so `nums1[i]` will be pushed first.
    
- In the `else` part, `nums2[j]` will be pushed.

This approach is **many times better**, as it only has **time complexity `O(n)`** and no extra space is needed for a hash table.

---