# Trapping Rainwater

Difficulty: hard
 : Yes
: June 24, 2025
Problem: array, prefixSum, two pointers
Time Taken: 1 hour+

### 🧠 My Thought Process on Trapping Rain Water

- I couldn’t come up with the full solution initially, so I watched just the **intuitive part** of a video.
- The guy said: *"Take leftMax and rightMax of each index"* — that gave me a clue.
- I created a function to find left and right max **for every index**, but:
    - It was **time-heavy**.
    - It gave a **Memory Limit Exceeded** error, because creating arrays for each index separately inside the function consumed too much space.

---

### 💡 Then I asked ChatGPT for a hint...

- It gave a useful idea: **create prefix and suffix arrays** to store:
    - `prefix[i]`: maximum height to the **left** of `i`
    - `suffix[i]`: maximum height to the **right** of `i`

---

### ✅ The Logic I Implemented

- For each index `i`, I calculated:
    
    ```cpp
    min(prefix[i], suffix[i]) - height[i]
    
    ```
    
- If this value is **greater than 0**, it means water can be trapped:
    
    ```cpp
    if (min(prefix[i], suffix[i]) - height[i] > 0)
        count += (min(prefix[i], suffix[i]) - height[i]);
    
    ```
    
- If it’s **less than 0**, it means **no water** is trapped — skip.

---

### 🔁 Understanding This More Deeply Helped Me Discover the Optimal Approach

Now here’s where it gets interesting — to understand the **two-pointer optimal approach**, I had to **deepen my understanding** of the prefix/suffix concept.

- Let's say the largest element is `5` and it's the **last** element.
- If you observe the `suffix[]`, it contains only that one max value at all positions after it.
- What does that tell us?
    - All elements **before the largest element** will have the **largest bar as rightMax**.
    - All elements **after it** will have it as **leftMax** (if we reverse the array).

---

### 🔨 Core Idea Behind the Optimal Two-Pointer Solution

- First, **find the index of the tallest bar**:
    
    ```cpp
    int peak = max_element(height.begin(), height.end()) - height.begin();
    
    ```
    
- Now do two separate passes:

### 👉 Left to Peak:

```cpp
int leftMax = 0;
for (int i = 0; i < peak; i++) {
    if (height[i] < leftMax) {
        water += leftMax - height[i];
    } else {
        leftMax = height[i];
    }
}

```

### 👉 Right to Peak:

- Start from the end and move **toward the peak**, but:
    - **Reset rightMax = 0** before this loop.
    - **Don't include** the peak again — skip it.

```cpp
int rightMax = 0;
for (int i = height.size() - 1; i > peak; i--) {
    if (height[i] < rightMax) {
        water += rightMax - height[i];
    } else {
        rightMax = height[i];
    }
}

```

- Finally, just return `water`.

---

### ✅ Why This Works

- We’re essentially **avoiding extra space** (like prefix/suffix arrays).
- We're not checking both directions at once, but rather breaking the problem at the **tallest peak**, which acts as a **barrier** between two valid trapping areas.
- **No overcounting**, because we skip the peak when processing from the back.

---

### 🎯 Final Thoughts

> This was a really interesting problem to solve.
> 
> 
> I made some mistakes, especially by not resetting `rightMax` and accidentally including the peak in both passes.
> 
> But figuring out how to optimize it by understanding the **core logic** made it super satisfying.
>