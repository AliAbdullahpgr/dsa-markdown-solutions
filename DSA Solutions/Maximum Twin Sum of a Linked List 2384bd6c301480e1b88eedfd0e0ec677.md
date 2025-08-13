# Maximum Twin Sum of a Linked List

Difficulty: medium
 : Yes
: July 22, 2025
Problem: linked list, stack/queue
Time Taken: 10-20 minutes

## ✅ Problem: Maximum Twin Sum of a Linked List

Given a **singly linked list of even length**, return the **maximum twin sum**.

Twin sum: `i-th node + (n - 1 - i)-th node`

---

## 🔍 Intuition & Insight

- Use a **stack** to reverse the list logic.
- First pass: push all node values to a stack.
- Second pass: start from the head and compute `curr.val + st.top()` (twin).
- Track max twin sum as we go.

---

## 🧠 Approach (Stack-Based)

1. **Push all elements** of the list onto a stack.
2. Reset `curr` to head.
3. For each node:
    - Pop top from stack.
    - Compute twin sum.
    - Update max twin sum.

---

## 💻 Code

```cpp
class Solution {
public:
    using Node = ListNode*;

    int pairSum(ListNode* head) {
        stack<int> st;
        Node curr = head;

        // Step 1: Push all values to stack
        while (curr) {
            st.push(curr->val);
            curr = curr->next;
        }

        // Step 2: Calculate twin sums
        curr = head;
        int M = INT_MIN;
        while (curr) {
            int sum = curr->val + st.top(); st.pop();
            M = max(M, sum);
            curr = curr->next;
        }

        return M;
    }
};

```

---

## 🧾 Time & Space Complexity

- **Time:** O(n) — two passes over the list
- **Space:** O(n) — stack stores all elements