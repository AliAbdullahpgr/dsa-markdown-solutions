# Merge K Sorted Lists

Difficulty: hard
 : Yes
: July 22, 2025
Problem: heap, linked list
Time Taken: 1 hour+

## 📘 Ali's Notes: Merge k Sorted Linked Lists Using Min Heap

---

### ✅ **What the Problem Wants**

- You're given multiple (`k`) sorted linked lists.
- You need to merge them into **one sorted list**.

---

### 🧠 **How I Understand the Solution**

### 🔸 Step 1: Use a Min Heap to Always Give Me the Smallest Value

- I use a custom comparator:
    
    ```cpp
    struct myCmp {
        bool operator()(ListNode* &a, ListNode* &b) {
            return a->val > b->val;
        }
    };
    
    ```
    
- This makes sure `.top()` always gives me the **smallest node**, not the largest like in default `priority_queue`.

---

### 🔸 Step 2: Push All Starting Nodes (Heads) of the k Lists

- I go through each list:
    
    ```cpp
    for (auto root : lists) {
        if (root) pq.push(root);
    }
    
    ```
    
- This fills my min heap with the **first node of each list**, which are the current smallest values.

---

### 🔸 Step 3: Build the Merged List Using Head and Tail Pointers

- I keep a `head` and `tail` to build the new list.
- First time:
    
    ```cpp
    if (!head) {
        head = smallest;
        tail = smallest;
    }
    
    ```
    
- After that:
    
    ```cpp
    tail->next = smallest;
    tail = tail->next;
    
    ```
    

---

### 🔸 Step 4: Keep Updating the Heap with `smallest->next`

- After popping the current smallest node, I push its `next` node into the heap:
    
    ```cpp
    if (smallest->next) pq.push(smallest->next);
    
    ```
    
- This way, I'm **always keeping track of the next smallest options**.

---

### 🧠 My Mental Picture

- I’m standing in front of `k` sorted lines of people.
- I always pick the **smallest number** from the front of each line (min heap helps with that).
- When I pick someone (a node), I ask **who's behind him in his line**, and I add that person to the competition (heap).

---

### ✅ Time & Space

- **Time**: `O(N log k)` — Every node goes through the heap once.
- **Space**: `O(k)` — At most `k` nodes in the heap.

---

### ✨ Summary in My Own Words

- My comparator makes sure I always get the smallest node on top.
- I push all starting points into the heap.
- I assign the very first one as the head of my final list.
- I keep connecting nodes by keeping track of the `tail`.
- After picking a node, I add its next to the heap.
- I keep doing this until my heap is empty.
- In the end, I get a perfectly merged, sorted linked list.