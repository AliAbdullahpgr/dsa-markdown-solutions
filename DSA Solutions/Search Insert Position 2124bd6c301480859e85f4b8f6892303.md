# Search Insert Position

Difficulty: easy
 : Yes
: June 14, 2025
Problem: array, binary search
Time Taken: 20-25 minutes

The **O(n)** version of this problem is very easy to solve, as you only need to find the insert position of the `target` through a simple loop traversal and return the appropriate index based on whether the current element is greater or smaller.

However, the problem **explicitly states** that it should be solved in **O(log n)** time complexity.

---

### 🔍 What is O(log n)?

- **O(log n)** means the problem should be solved using **binary search**, not linear search.
- In binary search, we reduce the search space by half in each iteration, which makes it logarithmic in time complexity.

---

### 🧠 My Understanding and Attempt

I tried solving this problem using binary search, which is indeed how this problem is supposed to be solved.

Initially, I used the **exclusive binary search** pattern:

```cpp
int left = 0;
int right = nums.size(); // exclusive range
while (left < right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] < target) {
        left = mid + 1;
    } else {
        right = mid;
    }
}
return left;

```

Then I kept trying and thinking and tried different approaches and a found the correct one which is a real thing called **inclusive binary search**, which was harder for me to understand:

```cpp
int left = 0;
int right = nums.size() - 1; // inclusive range
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (nums[mid] == target) return mid;
    else if (nums[mid] < target) left = mid + 1;
    else right = mid - 1;
}
return left;

```

---

### 🧾 Key Learnings

- In **both cases**, whether you're using exclusive or inclusive binary search, you **return `left`** at the end.
- We should also **check if the target exists directly in the array** during the process (`if(nums[mid] == target)`).
- Although the **inclusive version** was more difficult for me to grasp at first, it’s a valid approach and commonly used.