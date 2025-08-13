# Merge Sorted Array

Difficulty: easy
 : Yes
: June 15, 2025
Problem: array, two pointers
Time Taken: 10-20 minutes

Got it, Ali — thanks for the clarification. You're saying:

- You're **talking about the classic “Merge Sorted Array” problem** (like [LeetCode 88](https://leetcode.com/problems/merge-sorted-array/)).
- You realized its **approach is the same as your notes** on **“Merge Two Sorted 2D Arrays”**, which you've written in your **Notion LeetCode template**.
- The difference is only in **structure (1D vs 2D arrays)**, but the **core two-pointer merge logic is identical**.

### 🔁 **Merge Sorted Array Insight**

> The approach to Merge Sorted Array (like nums1 and nums2) is basically the same as merging two sorted 2D arrays (as noted in my Notion LeetCode template).
> 
- ✅ **Only difference** is that:
    - Here we use a **temporary 1D vector `res`** to store results.
    - Then finally assign: `nums1 = res;`
- ✅ Time complexity = `O(n + m)`
- ✅ Space complexity = `O(n + m)`
    
    > where n = nums1 size, m = nums2 size
    > 

---

### 🛑 Mistake I Made on 2nd Try

- I was looping till `nums1.size()` and `nums2.size()`, which is **wrong**.
- The problem **clearly gives you `m` and `n`**, i.e., number of values to consider from `nums1` and `nums2`.
- You should only loop while `i < m` and `j < n`.

---

### ✅ Two Pointer Approach Steps

- Use `i = 0`, `j = 0`
- Loop while `i < m && j < n`
    - If `nums1[i] == nums2[j]` → add sum to result
    - If `nums1[i] < nums2[j]` → add `nums1[i]` to result
    - Else → add `nums2[j]` to result
- Add remaining values from either array
- Final assignment: `nums1 = res;`

---

### 💡 You were right — same concept applies to both:

- Whether it’s:
    - `vector<int>` for `Merge Sorted Array`
    - or `vector<vector<int>>` for `Merge Two Sorted 2D Arrays`
        
        → The **logic doesn’t change**, just the **data shape** does.
        

Let me know if you want a memory-optimized version (like in-place merge for LeetCode 88), or just want to keep this note structured for your documentation.