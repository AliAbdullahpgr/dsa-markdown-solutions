# Lambda Function

Difficulty: basic
 : Yes
: June 19, 2025
Problem: theory

## 🧠 What is a Lambda Function in C++?

A **lambda function** is an **anonymous (unnamed)** function you can define inline.

It’s mostly used when:

- You want to pass simple logic to a function like `sort`, `for_each`, etc.
- You don’t want to define a separate named function.

---

### ✅ Basic Syntax:

```cpp
[captures] (parameters) -> return_type {
    // function body
};

```

👉 The `-> return_type` is optional if the compiler can deduce it.

Let’s simplify it:

```cpp
[](int a, int b) {
    return a + b;
}

```

This creates a function that takes two integers and returns their sum.

But it doesn’t run **unless** you call it.

---

### 🧪 Example 1: Lambda as a variable

```cpp
auto sum = [](int a, int b) {
    return a + b;
};

int result = sum(3, 5);  // result = 8

```

---

### 🧪 Example 2: Passing Lambda to `sort`

Let's say you have:

```cpp
vector<int> nums = {3, 1, 4, 1, 5};

```

And you want to sort in **descending** order. Normally, `sort(nums.begin(), nums.end())` sorts ascending.

With lambda:

```cpp
sort(nums.begin(), nums.end(), [](int a, int b) {
    return a > b;  // descending order
});

```

✅ The lambda `[](int a, int b) { return a > b; }` is passed directly to `sort()`.

---

## 📌 Important Concepts

### 1. **Capture List** `[]`

- This is used when your lambda wants to **use variables from outside** its body.
- Example:

```cpp
int threshold = 10;
auto isGreater = [threshold](int x) {
    return x > threshold;
};

```

Here, the lambda **captures** `threshold` from the outer scope.

---

### 2. **Parameter List** `(int a, int b)`

Just like normal functions.

---

### 3. **Return Type** `> bool` (Optional)

Most times C++ can figure it out on its own.

---

## 📦 Real Example: Sorting `vector<pair<int, int>>`

Imagine this:

```cpp
vector<pair<int, int>> p = {{2, 100}, {1, 200}, {2, 50}};

```

Sort by:

- Increasing `first`
- If `first` is equal, then decreasing `second`

```cpp
sort(p.begin(), p.end(), [](pair<int, int>& a, pair<int, int>& b) {
    if (a.first == b.first)
        return a.second > b.second;
    return a.first < b.first;
});

```

Here, the lambda:

- Takes two pairs `a` and `b`
- Applies the custom rule
- Returns `true` if `a` should come before `b`

---

## 🚀 Summary

| Part | Meaning |
| --- | --- |
| `[]` | Capture outside variables (can be empty) |
| `(int a, int b)` | Parameters like a normal function |
| `{ return ...; }` | Function body |
| `auto f = [](...) {...};` | Store it as a variable |
| `sort(..., [](...) {...});` | Pass it directly |

---

Let me know if you want a visual diagram, or to practice writing some!