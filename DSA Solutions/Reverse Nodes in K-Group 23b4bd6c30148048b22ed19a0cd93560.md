# Reverse Nodes in K-Group

Difficulty: hard
 : Yes
: July 25, 2025
Problem: linked list
Time Taken: 20-25 minutes

## ✅ Reverse Nodes in k-Group – Notes

### 🔹 Problem:

Reverse nodes in a linked list in groups of size `k`.

If the number of nodes at the end is less than `k`, **do not reverse** them.

---

### ⚙️ Step-by-Step Explanation

### 1. **Base Cases**

```cpp
if (!head || k == 1) return head;

```

- If the list is empty (`head == nullptr`), return it as is.
- If `k == 1`, there's nothing to reverse — just return `head`.

---

### 2. **Dummy Node Setup**

```cpp
ListNode* dummy = new ListNode(0);
dummy->next = head;
ListNode* groupPrev = dummy;

```

- Dummy node helps handle edge cases like changing the head of the list.
- `groupPrev` points to the **node before the group to be reversed**. Initially, it's the dummy node.

---

### 3. **Main Loop**

```cpp
while (true) {
    ListNode* kth = groupPrev;
    for (int i = 0; i < k && kth; i++) {
        kth = kth->next;
    }
    if (!kth) break;

```

- We move `kth` pointer **`k` steps forward** to find the end of the current group.
- If there are **fewer than `k` nodes**, we stop (no reversal).

---

### 4. **Prepare Pointers**

```cpp
ListNode* groupNext = kth->next;
ListNode* prev = groupNext;
ListNode* curr = groupPrev->next;

```

- `groupNext`: the node **after the current group**.
- `prev`: will be used during reversal — initially points to `groupNext`.
- `curr`: start of the group to be reversed.

---

### 5. **Reverse the Group**

```cpp
while (curr != groupNext) {
    ListNode* tmp = curr->next;
    curr->next = prev;
    prev = curr;
    curr = tmp;
}

```

- Standard **linked list reversal logic**:
    - Reverse links within the group.
    - `curr` moves forward, `prev` follows behind as the new head of the reversed part.

---

### 6. **Reconnect the Group**

```cpp
ListNode* tmp = groupPrev->next; // old head (now tail)
groupPrev->next = kth;           // connect to new head
groupPrev = tmp;                 // move to tail for next group

```

- Connect the previous part of the list to the new head (`kth`).
- Move `groupPrev` to the tail of the reversed group to repeat the process.

---

### 7. **Return the New Head**

```cpp
return dummy->next;

```

- Return the actual head of the modified list — skipping the dummy node.

---

### 🧪 Example: `head = [1,2,3,4,5], k = 2`

1st group: [1,2] → reversed to [2,1]

2nd group: [3,4] → reversed to [4,3]

Last node: [5] → remains as is

**Output:** `[2,1,4,3,5]`

---

### ✅ Key Takeaways:

- Using a dummy node simplifies list operations at the head.
- Make sure to move `kth` from `groupPrev` to avoid off-by-one errors.
- Reversal logic is same as standard list reversal, just within bounds.
- Carefully update pointers after each group to stitch everything back.