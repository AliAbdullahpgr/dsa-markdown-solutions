# Merge Two Sorted Linked Lists

Difficulty: medium
 : Yes
: July 11, 2025
Problem: linked list
Time Taken: 10-20 minutes

### ✅ **Problem: Merge Two Sorted Linked Lists**

You are given two sorted linked lists. Your task is to merge them into one sorted list **without modifying the original lists**, using **new nodes**.

---

### ✅ **What You Did Right**

- Created a dummy node to simplify list construction.
- Used a `dummy` pointer to build the list.
- Handled the remaining nodes of `list1` and `list2` separately.
- Returned `head->next` to skip the dummy node.
- Correctly used `new ListNode(val)` to allocate new nodes (deep copy).

---

### ❌ **Mistakes & Fixes**

### 🔴 **Mistake 1: Uninitialized Pointer**

```cpp
ListNode* head;
ListNode* dummy = head;

```

- ❌ `head` was uninitialized (undefined memory).
- 🛠️ Fix: Properly initialize it with a dummy node:
    
    ```cpp
    ListNode* head = new ListNode();  // safe dummy node
    
    ```
    

---

### 🔴 **Mistake 2: Unsafe condition in loop**

```cpp
while (list1 || list2) {
    if (list1->val <= list2->val) { ... }
}

```

- ❌ You tried to access `.val` without checking if `list1` or `list2` was `nullptr`.
- 🛠️ Fix: Only enter the loop when **both lists are non-null**:
    
    ```cpp
    while (list1 && list2) { ... }
    
    ```
    
- Then, handle the rest in separate loops.

---

### 🔴 **Mistake 3: Returning the dummy node**

```cpp
return head;

```

- ❌ Would include the dummy node (value 0) in your result.
- 🛠️ Fix: Skip it:
    
    ```cpp
    return head->next;
    
    ```
    

---

### 🧠 **Lessons Learned**

1. **Always initialize pointers** before dereferencing.
2. **Null-check before accessing `.val`** or `>next`.
3. **Use dummy nodes** to simplify list problems.
4. When building a new list, **deep copy** nodes instead of reusing original ones unless allowed.
5. Returning `dummy->next` is a common trick to return the built list cleanly.

---