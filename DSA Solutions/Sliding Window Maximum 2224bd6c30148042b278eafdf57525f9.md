# Sliding Window Maximum

Difficulty: medium
 : Yes
: June 30, 2025
Problem: array, sliding window, stack/queue
Time Taken: 1 hour+

### Problem:

We need to find the **maximum element** in every sliding window of size `k` in the array `nums`.

Brute-force (using two loops) is slow and can give **TLE** (Time Limit Exceeded).

So, we use a **deque** (`std::deque<int>`) to **optimize** the solution to **O(n)** time.

---

### 🧰 Key Idea — What is Deque?

A **deque** lets us:

- Push from **front** and **back**
- Pop from **front** and **back**

So it's perfect for keeping track of a **range of elements** in a smart way.

---

### ✅ Goal:

- Loop through the array
- Always keep the **maximum element's index** at the **front of deque**
- Make sure the deque only contains indices **within the current window**
- Skip all elements **smaller** than current because they’re useless

---

### 🧾 Code:

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;       // stores indices
    vector<int> res;     // final result

    for (int i = 0; i < nums.size(); i++) {
        // 🔹 Remove elements from the front if they’re out of the current window
        if (!dq.empty() && dq.front() <= i - k) {
            dq.pop_front();
        }

        // 🔹 Remove all smaller elements from the back
        // because they can't be the max if nums[i] is bigger
        while (!dq.empty() && nums[dq.back()] < nums[i]) {
            dq.pop_back();
        }

        // 🔹 Add current index to deque
        dq.push_back(i);

        // 🔹 Once the first window is complete, start pushing results
        if (i >= k - 1) {
            res.push_back(nums[dq.front()]); // front has the max element index
        }
    }

    return res;
}

```

---

### 🔍 Step-by-Step Explanation:

- `dq.front() <= i - k`:
    - This removes indices **that are no longer in the current window**
    - Keeps our **window size fixed at `k`**
- `nums[dq.back()] < nums[i]`:
    - This removes all elements **smaller than** `nums[i]` from the **back**
    - Because `nums[i]` is bigger and will stay longer in the window
- `dq.push_back(i)`:
    - Store the **index**, not the value
    - So we can track if it goes out of window later
- `res.push_back(nums[dq.front()])`:
    - The **maximum** for current window is always at the **front**

---

### 🔦 Visualization Example

For `nums = [1,3,-1,-3,5,3,6,7]`, `k = 3`

Result should be: `[3,3,5,5,6,7]`

How?

- First window `[1,3,-1]` → max = 3
- Next window `[3,-1,-3]` → max = 3
- Next `[ -1,-3,5 ]` → max = 5
- ...

---

### 🧠 Why is this efficient?

- Each element is **pushed and popped at most once**
- So total complexity is **O(n)**