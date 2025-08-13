# Find the Duplicate Number

Difficulty: medium
 : Yes
: June 23, 2025
Problem: array, two pointers
Time Taken: 1 hour+

Below is the file that contains what I wrote for visualization can be opened in excalidraw.com

[Untitled-2025-06-14-2344.excalidraw](Find%20the%20Duplicate%20Number%2021b4bd6c3014802aace7fa842a4e1cc0/Untitled-2025-06-14-2344.excalidraw)

## Find the Duplicate Number — Floyd's Cycle Detection

Really interesting problem to solve —

It’s an **easy problem** if you can use extra space, and a **hard one** if you can’t.

I solved it under two minutes using a `hashset`, but couldn’t come up with the **optimized approach** for this. Apparently, this problem uses **Floyd’s algorithm** (a.k.a **Tortoise and Hare**) to solve it. It’s **mainly a cycle detection problem** — just like the **cycle detection problem in linked lists**.

---

## 💡 Insight

We get this **twist**: even though every element in the array is between `1 to n` (with `n` being the size of the array), we can treat the array as a **pointer chain** — where:

```cpp
i -> nums[i]

```

Given:

```cpp
nums = [1, 3, 4, 2, 2]

```

The path looks like:

```
1 → 3 → 2 → 4 → 2 → 4 → ... // the point towards the index such as the 3 is at index 1 so 1 points towards 3. 2 is at index 3 so 3 points towards 2. 4 is at index 2 so 2 points towards 4 No here the fun part 2 is at index 2 is at index 4 so 2 points towards 4 and 4 again points towards the 2 here our cycle

```

There’s **clearly a cycle** between `2` and `4`.

---

## 📺 Shoutout to NeetCode

I watched **NeetCode’s video** on how to solve this problem —

Even he said he **couldn’t come up with this solution on his own**, which honestly made me feel better.

---

## 🐢🐇 How the algorithm works

- Take two pointers: `slow` and `fast`
- `slow` moves **1 step** at a time
- `fast` moves **2 steps** at a time

```cpp
int slow = 0;
int fast = 0;

while (true) {
    slow = nums[slow];
    fast = nums[nums[fast]];
    if (slow == fast) break; // they intersect inside the cycle
}

```

At **some point in the cycle**, they both intersect.

Now, if we only needed to detect the cycle — we’re done here.

But the question asks us to **find the duplicate value**.

---

## 🌀 Entry Point = Duplicate

The point where they intersect **may or may not be the start of the cycle**.

Here’s the main thing:

> The entry point of the cycle is the duplicate value, because it's the number that repeats itself — creating the loop.
> 

So we start a **new pointer `slow1` from `0`**, and keep moving it **1 step at a time**, along with the old `slow`, until they meet.

```cpp
int slow1 = 0;
while (slow1 != slow) {
    slow = nums[slow];
    slow1 = nums[slow1];
}
return slow;

```

---

## 🧮 The Math (for deeper understanding)

Let:

- `c = size of the cycle`
- `p = number of steps before entry into the cycle`
- `k = number of steps slow has moved inside the cycle before meeting fast`

Then:

### 🧾 Slow and Fast step count:

- Steps moved by `slow` = `p + k`
- Steps moved by `fast` = `2(p + k)`

### 🧾 Distance between fast and slow:

```
2(p + k) - (p + k) = p + k

```

So the difference = `p + k`

This difference must be a multiple of the cycle length:

```ruby
p + k ≡ 0 mod c //p + k must be divisible by the cycle length c
=> k ≡ -p mod c
=> k = c - p // then from the meeting point, we’re p steps away from the cycle entry.

```

Now, from the point where slow and fast met:

- Slow is `k` steps into the cycle
- So from that point, if we move both:
    - `slow` from index `k`
    - `slow1` from index `0`
        
        — both will meet after `p` steps at the **entry of the cycle**, which is the **duplicate**.
        

---

## ✅ Final Code

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;

        // Phase 1: Detect the cycle
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        // Phase 2: Find entry point of cycle = duplicate
        int slow1 = 0;
        while (slow1 != slow) {
            slow = nums[slow];
            slow1 = nums[slow1];
        }

        return slow;
    }
};
```

![image.png](Find%20the%20Duplicate%20Number%2021b4bd6c3014802aace7fa842a4e1cc0/image.png)

![image.png](Find%20the%20Duplicate%20Number%2021b4bd6c3014802aace7fa842a4e1cc0/image%201.png)