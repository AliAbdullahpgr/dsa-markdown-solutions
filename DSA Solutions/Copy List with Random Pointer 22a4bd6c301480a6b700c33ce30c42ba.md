# Copy List with Random Pointer

Difficulty: medium
 : Yes
: July 8, 2025
Problem: linked list
Time Taken: 20-25 minutes

this **Copy List with Random Pointer** problem can feel confusing at first because of the extra `random` pointer. But once you get the intuition behind using a hashmap to create a mapping between the original and copied nodes, the solution becomes clean and logical.

---

Here’s a breakdown of your solution with clarity, focusing especially on:

```cpp
copy = oldToCopy[curr];

```

---

### 🔁 Problem Recap

Each node has:

- `val`: the value of the node.
- `next`: pointer to the next node.
- `random`: pointer to **any node** in the list (or `nullptr`).

You want to **deep copy** this list. Meaning, create a new list where:

- All `val` are copied.
- `next` and `random` point to **new nodes**, not old ones.

---

### 🧠 Core Idea

Use a **hashmap** to keep track of which copied node corresponds to which original node:

```cpp
unordered_map<Node*, Node*> oldToCopy;

```

This way, any time you see a pointer (`next` or `random`) in the original list, you can easily find the corresponding pointer in the new list.

---

### ✅ Step-by-Step Explanation

### ✅ Step 1: First loop — Create nodes and map them

```cpp
Node* curr = head;
while(curr){
    copy = new Node(curr->val);
    oldToCopy[curr] = copy;
    curr = curr->next;
}

```

- You walk through the original list.
- For each original node (`curr`), create a **new node** with the same value.
- Store the mapping: `original → copy` in the hashmap.

**Example:**

```cpp
original list:  1 → 2 → 3
hashmap: {
  [Node(1)] → [Node(1')],
  [Node(2)] → [Node(2')],
  [Node(3)] → [Node(3')]
}

```

---

### ✅ Step 2: Second loop — Assign `next` and `random`

```cpp
curr = head;
while(curr){
    copy = oldToCopy[curr]; // 🔍 This line
    copy->next = oldToCopy[curr->next];
    copy->random = oldToCopy[curr->random];
    curr = curr->next;
}

```

- `copy = oldToCopy[curr];`
    
    🔹 This retrieves the **copied node** corresponding to the current `curr` node in the original list.
    
    So now:
    
    - `curr` is a node in the **original** list.
    - `copy` is the **corresponding node** in the **copied** list.
- Then we set the pointers of the copied node:
    
    ```cpp
    copy->next = oldToCopy[curr->next];
    copy->random = oldToCopy[curr->random];
    
    ```
    
    🔹 `oldToCopy[curr->next]` gives you the copy of the node that `curr->next` points to.
    
    🔹 `oldToCopy[curr->random]` gives you the copy of the node that `curr->random` points to.
    

---

### 🔚 Final Step

Return the head of the copied list:

```cpp
return oldToCopy[head];

```

---

### 📦 Full Code Again (Clean)

```cpp
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;

    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};

class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> oldToCopy;
        Node* curr = head;

        // Step 1: Copy all the nodes and store mapping
        while(curr) {
            Node* copy = new Node(curr->val);
            oldToCopy[curr] = copy;
            curr = curr->next;
        }

        // Step 2: Assign next and random pointers
        curr = head;
        while(curr) {
            Node* copy = oldToCopy[curr];
            copy->next = oldToCopy[curr->next];
            copy->random = oldToCopy[curr->random];
            curr = curr->next;
        }

        return oldToCopy[head];
    }
};

```

---

### 💡 Summary

- **Why `copy = oldToCopy[curr]`?**
    - To access the **copied version** of the current node (`curr`), so we can assign its `next` and `random`.
- **Key insight:**
    - The original and new lists are **synchronized** via the hashmap — allowing fast access to any corresponding copy node.

![image.png](Copy%20List%20with%20Random%20Pointer%2022a4bd6c301480a6b700c33ce30c42ba/image.png)