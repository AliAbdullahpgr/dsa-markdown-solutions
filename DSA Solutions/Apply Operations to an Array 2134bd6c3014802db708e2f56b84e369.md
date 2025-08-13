# Apply Operations to an Array

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 10-20 minutes

## Apply Operations to an Array

**Problem - My Explanation**

I think the "performing action" part of this problem is really easy to understand and can be implemented quite easily.

The **real tricky part** is moving all the zeros to the back of the array.

---

### 🧠 First Approach (My Initial Thought)

- Use another array.
- First, collect all the **non-zero** values.
- Then, add all the **zero** values at the end of the new array.
- This works, but I unexpectedly spent a lot of time on it — mostly because I forgot some syntax related to `vector`.

```cpp
vector<int> arr(size); // Initializes vector with 'size' elements, all set to 0.

```

- If we do something like `arr = {0}`, it adds `0` to **all** its elements (important to remember).

---

### 💡 Second Approach (Pointer Index – From the Internet)

- Use an index pointer starting at `0`.
- Traverse the array:
    - If a non-zero value is encountered:
        - Store it at `arr[index]`.
        - Increment `index++`.
- After the loop:
    - From `index` to `arr.size()`, set the remaining elements to `0`.

```cpp
int index = 0;
for (int i = 0; i < arr.size(); i++) {
    if (arr[i] != 0) {
        arr[index] = arr[i];
        index++;
    }
}
for (int i = index; i < arr.size(); i++) {
    arr[i] = 0;
}

```

---

### ✅ Final Thoughts

- This is the **most optimal solution** in terms of:
    - **Time Complexity:** `O(n)`
    - **Space Complexity:** `O(1)`
- I actually found this approach online and tried implemented it myself.
- Honestly, it was a **pretty easy problem**, and I **don’t know why I spent so much time on it** 😅