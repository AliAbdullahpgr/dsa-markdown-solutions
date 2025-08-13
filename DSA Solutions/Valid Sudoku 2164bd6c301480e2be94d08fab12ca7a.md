# Valid Sudoku

Difficulty: medium
 : Yes
: June 18, 2025
Problem: array, hashtable/freq method, matrix
Time Taken: 30 minutes

## **Sudoku Validator: Thought Process**

---

### 🧠 **At First Glance**

- The problem looks really difficult at first.
- It seems that creating multiple loops would result in time complexity of **O(n²)** or even more.
- But in reality, the time complexity remains **O(1)** because the size of the Sudoku board is always **9×9**, a constant.

---

## 🧱 **Step-by-Step Strategy**

---

### 1️⃣ **Understand the Matrix**

- First, see the “Matrix” page on Notion (or revise matrix traversal).
- Understand how to traverse a matrix **row-wise**, **column-wise**, and in **3×3 sub-boxes**.

---

### 2️⃣ **Check Rows for Uniqueness**

- Traverse each row and check whether it has **unique digits** (ignoring `'.'`).
- Use a `set` to track the characters you've seen.

```cpp
unordered_set<char> s1;
for (int i = 0; i < 9; i++) {
    for (int j = 0; j < 9; j++) {
        if (board[i][j] != '.' && s1.find(board[i][j]) != s1.end()) {
            return false;
        }
        s1.insert(board[i][j]);
    }
    s1.clear();
}

```

> ❗️Mistake I made:
> 
> 
> I was also adding the character `'.'` into the set and checking it.
> 
> This causes false duplicates, since every row has multiple `'.'`.
> 

---

### 3️⃣ **Check Columns for Uniqueness**

- Similar logic as row check, but swap `i` and `j` to traverse columns.

```cpp
unordered_set<char> s2;
for (int i = 0; i < 9; i++) {
    for (int j = 0; j < 9; j++) {
        if (board[j][i] != '.' && s2.find(board[j][i]) != s2.end()) {
            return false;
        }
        s2.insert(board[j][i]);
    }
    s2.clear();
}

```

> ✅ Now we’ve confirmed both rows and columns have unique elements.
> 

---

### 4️⃣ **Check 3×3 Boxes**

- This seems like the hard part, but it's just another pattern.
- We run two loops with `i += 3` and `j += 3` to move box-by-box.
- Then we run a nested `3×3` traversal for each box.

```cpp
for (int i = 0; i < 9; i += 3) {
    for (int j = 0; j < 9; j += 3) {
        unordered_set<char> s3;
        for (int k = i; k < i + 3; k++) {
            for (int l = j; l < j + 3; l++) {
                if (board[k][l] != '.' && s3.find(board[k][l]) != s3.end()) {
                    return false;
                }
                s3.insert(board[k][l]);
            }
        }
    }
}

```

- We only need to make sure that `i` and `j` increment by 3 to cover all boxes.
- Inside, we use the classic **matrix traversal** logic.

---

## 🧮 **Time Complexity**

- Even though there are 3 loops (row, column, box), each cell is visited only a few times.
- Since the Sudoku board is always **9×9**, the operations are **constant**.

> ✅ Time Complexity: O(1)
> 
> 
> ✅ **Space Complexity: O(1)** (because each set holds at most 9 elements)
> 

---

### ✅ Summary

- ✔ Problem feels difficult initially, but breaks down easily.
- ✔ Always ignore `'.'` before inserting/checking sets.
- ✔ Use simple nested loops for each type of check.
- ✔ Time and space complexity stay constant.

---