# Reverse Linked List

Difficulty: easy
 : Yes
: July 9, 2025
Problem: linked list, two pointers
Time Taken: 10-20 minutes

### 🔄 Problem: Reverse a Singly Linked List

We are given the `head` of a singly linked list, and we need to **reverse** the list so that the head becomes the tail, and vice versa.

---

### ✅ Base Case:

- If the list is empty (`head == nullptr`), return `nullptr` immediately.

```cpp
if (!head) return nullptr;

```

---

### 🧠 Intuition Behind the Algorithm

We need to **reverse the pointers** in the list.

### So we use:

- `curr` → to point to the **current node**
- `prev` → to point to the **previous node** (initially `nullptr`)
- `next` → to temporarily store the **next node**

### Steps inside the loop:

- Save `curr->next` into `next` before breaking it.
- Reverse the link by setting `curr->next = prev`
- Move `prev` forward to `curr`
- Move `curr` forward to `next`

---

### 🔁 While Loop Explanation

- Keep looping while `curr` is not `nullptr`
- Each time, do:
    1. `next = curr->next;` → Save next node
    2. `curr->next = prev;` → Reverse pointer
    3. `prev = curr;` → Move prev to current
    4. `curr = next;` → Move curr to next

---

### ✅ Final Return:

- Once the loop ends, `prev` will be at the **new head** of the reversed list.

---

### 🧾 Final Code:

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head) return nullptr;

        ListNode* curr = head;
        ListNode* prev = nullptr;

        while (curr) {
            ListNode* next = curr->next;  // 1. Save next
            curr->next = prev;            // 2. Reverse link
            prev = curr;                  // 3. Move prev
            curr = next;                  // 4. Move curr
        }

        return prev;  // New head of reversed list
    }
};

```

---

### 📌 Key Takeaways:

- This is an **iterative solution** to reverse a singly linked list.
- Space complexity is **O(1)** (constant space), since no extra data structure is used.
- Time complexity is **O(n)**, where n is the number of nodes in the list.
- Always keep `prev`, `curr`, and `next` updated in each iteration.