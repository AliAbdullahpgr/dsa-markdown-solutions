# Sort Array by Parity

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 5 minutes

### Sort Array by Parity

This question asks us to solve an array in terms of **parity**.

---

### 🔍 What is Parity?

This is very important to understand:

**Parity** means we need to sort the array in terms of **even and odd** numbers.

---

### 📋 What the Problem Asks

This problem specifically asks us to have the **evens in the front** and **odds in the back** of the array.

---

### 🚀 Approach – Two Pointer

We simply use the **two pointer** approach:

- Have an `i` pointer starting from `0`
- Have a `j` pointer starting from `nums.size() - 1`
- Iterate through the array until `i < j`

### 🔄 Inside the Loop:

- If `nums[i]` is even → skip
- Else if `nums[i]` is odd **and** `nums[j]` is even → swap them
- Else case → just decrement the value of `j`

---

### 🤔 Why This Approach Works

Because we know:

- We only need `i` to iterate through the first half of the array
- And `j` to handle the second half

---

### 🕒 Time Complexity

- It has a time complexity of **O(n)**