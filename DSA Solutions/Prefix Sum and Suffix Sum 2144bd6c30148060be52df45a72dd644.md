# Prefix Sum and Suffix Sum

Difficulty: basic
 : Yes
: June 16, 2025
Problem: prefixSum, theory
Time Taken: 30 minutes

### 🔹 Prefix Sum in DSA

Prefix Sum is a technique in DSA to calculate **range sum queries** or the **sum between two points** in an array.

We use a **prefix array** to precompute values so that we can answer queries efficiently in constant time.

---

### 📌 Example

If we have:

```cpp
array = {1, 2, 3, 4, 5}

```

Then the **prefix sum array** would be:

```cpp
prefix = {1, 3, 6, 10, 15}

```

---

### 🔹 Ways to Create a Prefix Array

### 🔸 Method 1: Prefix of the same size as the array

```cpp
vector<int> prefix(array.size());
prefix[0] = array[0];

for (int i = 1; i < array.size(); i++) {
    prefix[i] = prefix[i - 1] + array[i];
}

```

- This is straightforward and directly stores the running sum at each index.
- To get the sum from index `l` to `r`:

```cpp
int sum = prefix[r] - (l > 0 ? prefix[l - 1] : 0);

```

---

### 🔸 Method 2: Prefix of size `n + 1` (used in many DSA problems)

```cpp
vector<int> prefix(n + 1);
prefix[0] = 0;

for (int i = 1; i <= n; i++) {
    prefix[i] = prefix[i - 1] + nums[i - 1];
}

```

- This is helpful in problems where 1-based indexing is easier or when range queries start from index 1.
- To get the sum from index `l` to `r`:

```cpp
int sum = prefix[r + 1] - prefix[l];

```

---

### ✅ Benefits

- Preprocessing takes **O(n)** time.
- Each range sum query is answered in **O(1)** time.
- Useful in various problems: subarray sum, difference arrays, line sweep techniques, etc.

---

### 🔹 Suffix Sum in DSA

Similar to **prefix sum**, **suffix sum** is also used to solve DSA problems.

It is basically the **opposite of prefix sum**.

Instead of taking the sum from the start of the array to index `i`, **suffix sum takes the sum from index `i` to the end of the array**.

---

### ✅ Usage

- Used for **range sum queries**, especially when we want to get the sum from some index to the **end**.
- It's useful in problems where we need to process the array **from the back**.

---

### 📌 Example

If we have:

```cpp
arr = {1, 2, 3, 4, 5}

```

Then the **suffix sum array** will be:

```cpp
suffix = {15, 14, 12, 9, 5}

```

Here's how it's calculated:

- `suffix[4] = arr[4] = 5`
- `suffix[3] = suffix[4] + arr[3] = 5 + 4 = 9`
- `suffix[2] = suffix[3] + arr[2] = 9 + 3 = 12`
- `suffix[1] = suffix[2] + arr[1] = 12 + 2 = 14`
- `suffix[0] = suffix[1] + arr[0] = 14 + 1 = 15`

---

### 🔧 Code to Build Suffix Array

```cpp
vector<int> arr = {1, 2, 3, 4, 5};
int n = arr.size();
vector<int> suffix(n);

suffix[n - 1] = arr[n - 1];

for (int i = n - 2; i >= 0; i--) {
    suffix[i] = suffix[i + 1] + arr[i];
}

```

---

### 🧠 Key Formula

```cpp
suffix[i] = suffix[i + 1] + arr[i];

```

- Start from the back:
    
    `suffix[n - 1] = arr[n - 1]`
    
- Then move backwards until `i == 0`

---