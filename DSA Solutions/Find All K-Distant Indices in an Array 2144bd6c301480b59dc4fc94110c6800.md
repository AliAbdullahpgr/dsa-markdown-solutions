# Find All K-Distant Indices in an Array

Difficulty: easy
 : Yes
: June 16, 2025
Problem: array, two pointers
Time Taken: 10-20 minutes

### I hated this problem — seriously.

It’s listed as *Easy*, but it took more effort than expected.

Here’s the **best solution I could come up with** (and I wasn’t going to write another one).

The worst version of this could easily go as bad as **O(n²)**.

---

### My Thought Process:

- First, I created a `vector<int> keyIndex` to store all the indices where `nums[i] == key`.
- Then, I looped through the array from `i = 0` to `i < nums.size()` and:
    - For every index `i`, I looped through the `keyIndex` array.
    - If the condition `abs(i - keyIndex[j]) <= k` was satisfied **even once**, I pushed `i` into the `result` vector and broke out of the inner loop.

> Important: Since i - j can be either positive or negative, I used abs(i - j) to handle both directions.
> 

---

### ⚠️ The Confusing Part (for me):

The part that **tripped me up** was this line in the problem:

> “There exists at least one index j such that |i - j| <= k and nums[j] == key.”
> 

I initially thought **all conditions had to be satisfied**, but **just one match** is enough.

So once you find a single index `j` that satisfies it, you're good to go — push `i` into `result`.

---

### Final Note:

My approach might not be the most optimized (definitely not pure O(n)),

but it’s readable, works well within constraints, and avoids unnecessary complexity.

And honestly, readability saved me here.