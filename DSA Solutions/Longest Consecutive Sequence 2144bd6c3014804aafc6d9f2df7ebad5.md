# Longest Consecutive Sequence

Difficulty: medium
 : Yes
: June 16, 2025
Problem: array, hashtable/freq method
Time Taken: 30 minutes

### Problem

---

### My Approach:

- First, we need to create an `unordered_set` to store only the **unique values** from the array.
- We also want **O(1)** search time for checking if a value exists in the array — this is why a set is ideal.

```cpp
unordered_set<int> s(nums.begin(), nums.end());

```

> I learned that we can directly insert all elements from the vector into a set like this using the constructor unordered_set<int>(arr.begin(), arr.end()).
> 

---

### 🔁 Core Logic:

- This problem looks **deceptively easy** at first — just sort the array and check if `arr[i] + 1 == arr[i+1]` to find a sequence.
- But it explicitly **asks for O(n) time complexity**, which rules out sorting (which is O(n log n)).

---

### 🔍 Finding the Sequence:

- Instead of **starting from every element**, we only start a sequence when:

```cpp
if (set.find(num - 1) == set.end())

```

> This means num is the start of a sequence because num - 1 doesn't exist.
> 

---

### 🔄 Expand the Sequence:

- Now we keep two variables:
    - `current = num`
    - `count = 1` (length of the sequence)
- We keep incrementing them as long as the next number exists:

```cpp
while (set.find(current + 1) != set.end()) {
    current++;
    count++;
}

```

- Keep track of the **maximum sequence length**:

```cpp
maxLength = max(maxLength, count);

```

---

### ⚠️ Struggles I Had:

- My **initial mistake** was trying to start a sequence from every element. That made things inefficient and harder to manage.
- I also misunderstood the part where we check `set.find(num - 1) == set.end()` — this is **crucial** to **avoid redundant checks**.
- The **biggest confusion** I had was with the **while loop**. I thought:
    
    > "If the while loop runs multiple times, doesn't that make it O(n²)?"
    > 
    
    But after deeper thinking and checking examples, I realized:
    
    - Every element is only **visited once**, even if the loop is nested inside a `for` loop.
    - That’s why it stays **O(n)** overall — it’s like amortized time complexity.

---

### 🧠 Final Insight:

This was a classic **set + greedy sequence** problem.

Once you get that the `num - 1` check helps **start sequences**, it all clicks.

Just track the **longest** one using `max()` — clean, efficient, and within time constraints.