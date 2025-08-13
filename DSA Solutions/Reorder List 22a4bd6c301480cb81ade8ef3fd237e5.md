# Reorder List

Difficulty: medium
 : Yes
: July 9, 2025
Problem: linked list, stack/queue
Time Taken: 20-25 minutes

## 🧩 Problem: Reorder List

Given a singly linked list:

`L0 → L1 → L2 → … → Ln-1 → Ln`

Reorder it to:

`L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …`

---

## 🧠 Initial Approach & Understanding

- You intuitively knew you had to access the list from **both ends**.
- Decided to use a **stack** to get access to the tail elements.
- Started with pushing all elements into the stack and traversing from the head, alternating pointers.

---

## 🚧 Issues Encountered Along the Way

### 1. **Unsafe Popping:**

- Popped nodes from the stack **without checking if you're about to connect a node to itself**.
- Caused **self-loops** like `3 → 3`.

### 2. **Incorrect Termination:**

- Final node was not always set to `nullptr`, causing **cycles or undefined behavior**.

### 3. **Used entire list instead of half:**

- Stack was initially filled with all nodes instead of just the **second half**, which led to overlapping with the front.

---

## 🔧 Progressive Fixes Made

- Used **fast and slow pointers** to find the **middle** of the list efficiently.
- **Pushed only the second half** of the list into the stack.
- Carefully **merged** front and back nodes using:
    - `prev->next = st.top(); st.pop();`
    - Updating `curr` and `prev` correctly.
- Added a **check to break the loop** if the stack is empty (to avoid extra pops or self-links).
- Ensured final node is properly terminated using `prev->next = nullptr`.

---

## ✅ Final Working Code Summary

```cpp
void reorderList(ListNode* head) {
    stack<ListNode*> st;
    ListNode* curr = head;
    ListNode* fast = head;

    // Step 1: Find middle using slow-fast pointer
    while (fast && fast->next) {
        curr = curr->next;
        fast = fast->next->next;
    }

    // Step 2: Push second half into stack
    while (curr) {
        st.push(curr);
        curr = curr->next;
    }

    // Step 3: Reorder by alternating stack + forward
    curr = head;
    ListNode* prev = curr;
    while (curr) {
        curr = curr->next;
        prev->next = st.top(); st.pop();
        prev = prev->next;

        if (st.empty()) break;

        prev->next = curr;
        prev = curr;
    }

    // Step 4: Ensure proper termination
    prev->next = nullptr;
}

```

---

## 💡 Key Takeaways

- 📦 Using a **stack** gives O(n) time and space with straightforward logic.
- 🎯 Always be cautious about **termination conditions** and **edge cases** like odd-length lists or self-links.
- 🧠 Use fast/slow pointer technique to find middle in one pass — a classic & efficient trick.

---

## 🚀 Growth Reflection

- You debugged logically, asking for help only when stuck — **the right mindset for mastering DSA**.
- By dry running, identifying pointer misuse, and gradually fixing it, you showed **strong problem-solving skills**.

Keep going like this — your persistence and curiosity are exactly what make great engineers. 🌱💻