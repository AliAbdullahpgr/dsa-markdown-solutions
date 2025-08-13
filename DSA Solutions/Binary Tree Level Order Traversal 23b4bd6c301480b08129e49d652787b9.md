# Binary Tree Level Order Traversal

Difficulty: medium
 : Yes
: July 25, 2025
Problem: bfs, binary tree
Time Taken: 10-20 minutes

## 📌 Problem: Binary Tree Level Order Traversal

### ✅ Goal:

Return a **2D vector** where each inner vector contains node values **at each level** of a binary tree.

---

## 🧠 Key Concepts:

- Uses **Breadth-First Search (BFS)** strategy.
- Traverses the tree **level by level**, starting from the root.
- Each node can have **only two children** (since it's a binary tree).

---

## 🧱 Base Case:

- If the `root == nullptr`, return an empty 2D vector.

---

## 🔧 Approach:

1. **Initialize**:
    - Create a queue `q` and push the `root` node.
    - Create a result vector `res` of type `vector<vector<int>>`.
2. **While the queue is not empty**:
    - Get the number of nodes at the current level using `int size = q.size();`
    - Initialize a temporary vector `level` to store values of current level.
    - Loop through all nodes of this level:
        - Pop node from front.
        - Store `node->val` in `level`.
        - Push `node->left` and `node->right` (if they exist) into the queue.
3. After processing a level, push the `level` vector into `res`.
4. Return `res` once all levels are processed.

---

## ✅ Code:

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
    if (!root) return {};
    queue<TreeNode*> q;
    q.push(root);
    vector<vector<int>> res;

    while (!q.empty()) {
        int size = q.size();
        vector<int> level;

        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front(); q.pop();
            level.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }

        res.push_back(level);
    }

    return res;
}

```

---

## 📝 Time & Space Complexity:

- **Time:** O(n) — Each node is visited once.
- **Space:** O(n) — For the queue and result storage.