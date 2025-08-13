# Linked List Cycle

Difficulty: easy
 : Yes
: July 8, 2025
Problem: linked list, two pointers
Time Taken: 10-20 minutes

## 🌀 Floyd’s Cycle Detection (Tortoise and Hare)

### ✅ Problem:

**Detect if a singly linked list has a cycle.**

---

### 🧠 Concept:

Use two pointers:

- `slow`: moves 1 step at a time
- `fast`: moves 2 steps at a time

If the list has a cycle, they will **eventually meet**.

If not, `fast` will reach `nullptr`.

---

### ✅ Final Correct Code:

```cpp
class Solution {
    using Node = ListNode*;

public:
    bool hasCycle(ListNode* head) {
        if (!head) return false;

        Node slow = head;
        Node fast = head;

        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;

            if (slow == fast) return true;
        }

        return false;
    }
};

```

---

### ❌ Bug You Had:

```cpp
if (fast->next->next == nullptr) return false;

```

🔴 **Problem**: You accessed `fast->next->next` **without checking if `fast` and `fast->next` were non-null**.

This could cause a **segmentation fault** (crash) when `fast` reaches the end of a non-cyclic list.

---

### ✅ Fix:

Change the loop condition to:

```cpp
while (fast && fast->next)

```

This ensures:

- `fast->next->next` is safe
- The loop stops when the list ends (no cycle)

---

### 🔁 Why It Works:

If there's a cycle:

- `fast` eventually overlaps `slow` in the loop

If no cycle:

- `fast` reaches `nullptr`, and loop ends safely