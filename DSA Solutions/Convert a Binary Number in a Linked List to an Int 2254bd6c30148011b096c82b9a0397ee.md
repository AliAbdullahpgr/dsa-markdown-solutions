# Convert a Binary Number in a Linked List to an Integer

Difficulty: easy
 : Yes
: July 3, 2025
Problem: linked list
Time Taken: 10-20 minutes

## Notes: Convert Binary Number in a Linked List to Integer

---

### 🔧 Problem:

Given a singly linked list where each node contains a binary digit (0 or 1), convert the binary number to its decimal equivalent.

Example:

Linked list: `1 -> 0 -> 1`

Binary: `101`

Decimal: `5`

---

### ❌ Initial Strategy (Less Optimal):

- Traverse the list, extract all values into a string or array.
- Convert the binary string/array to decimal.
- ❗ **Drawbacks:**
    - More time and space consumption.
    - Less efficient (O(n) time + O(n) space).

---

### ✅ Optimized Strategy:

Use formula:

```cpp
res = res * 2 + head->val;

```

- Think of `res` as accumulating the binary number left to right.
- At each node:
    - Multiply `res` by 2 (left shift).
    - Add the current bit (`head->val`).
- Requires only **1 variable** and **1 pass**.

---

### 🧪 Dry Run Example:

Linked list: `1 -> 0 -> 1`

Binary: `101`

### Step-by-step:

- `res = 0`
- Read `1`: `res = 0 * 2 + 1 = 1`
- Read `0`: `res = 1 * 2 + 0 = 2`
- Read `1`: `res = 2 * 2 + 1 = 5`

✅ Output: `5`

---

### 🧠 Time & Space Complexity:

- **Time:** `O(n)` (traverse once)
- **Space:** `O(1)` (no extra memory used)

---

### 💻 Final Code (C++):

```cpp
class Solution {
public:
    int getDecimalValue(ListNode* head) {
        int res = 0;
        while (head) {
            res = res * 2 + head->val;
            head = head->next;
        }
        return res;
    }
};

```