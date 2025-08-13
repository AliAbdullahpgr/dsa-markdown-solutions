# Contains Duplicate II

Difficulty: easy
 : Yes
: June 30, 2025
Problem: array, hashtable/freq method, sliding window
Time Taken: 10-20 minutes

### 🔄 Naive Two Loop Approach (❌ Runtime Error / TLE)

- really easy to solve problem using two for loops
- finding two elements from i and j
- and check if `nums[i] == nums[j]` and `abs(i - j) <= k`
- if that is true then return true
- but this gives runtime error (TLE) which is really bad

```cpp
for(int i = 0; i < nums.size(); i++) {
    for(int j = i + 1; j < nums.size(); j++) {
        if(nums[i] == nums[j] && abs(i - j) <= k) {
            return true;
        }
    }
}
return false;

```

---

### ✅ Optimization with Sliding Window + HashSet

- in order to optimize it what we should do is:
    - do things
    - do what we need to use: **sliding window approach**
- which sliding window? fixed sized sliding window
- as the window size `k` is given
- we just need to traverse each `k` elements
- while keeping our window size `k`
- if you have solved **find duplicate** question
- you would know how to solve this problem duh duh
- it’s solved through a **hashset**

---

### 🪟 Sliding Window with HashSet

- so what we do is:
    - window size = `k`
    - hashset to keep track of elements in current window

```cpp
bool containsNearbyDuplicate(vector<int>& nums, int k) {
    unordered_set<int> window;

    for (int i = 0; i < nums.size(); i++) {
        // first check the condition to be true
        if (window.count(nums[i])) return true;

        // add current element to the hashset
        window.insert(nums[i]);

        // if hashset is larger than k, remove element at i-k
        if (window.size() > k) {
            window.erase(nums[i - k]);
        }
    }

    return false;
}

```

---

### 💡 Where We Get the Hint From?

- the **hint** is: `abs(i - j) ≤ k`
- which is basically the **size of the window**
- it means that our elements lie in a window of size `k`

> like if the window size is 3 → the difference between duplicate elements should be at most 3
> 

---

### 🧠 Summary (as per your tone)

- so yeah just keep removing our previous element and keep adding the new one
- and boom problem solved
- it's basically a hashset + sliding window combo
- if the set already has an element → return true
- otherwise keep going
- sliding window helps maintain distance `k`

---

Let me know if you want this in a **competitive programming style** (messy, no comments, tight code).