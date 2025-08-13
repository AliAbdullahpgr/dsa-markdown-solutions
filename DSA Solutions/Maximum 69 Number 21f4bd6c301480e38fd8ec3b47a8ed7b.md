# Maximum 69 Number

Difficulty: easy
 : Yes
: June 27, 2025
Problem: array, greedy
Time Taken: 5 minutes

## What Is a Greedy Algorithm?

A **greedy algorithm** builds up a solution piece by piece, always choosing the **locally optimal choice** at each step with the hope that it leads to a **globally optimal solution**.

> Once a decision is made, it's never changed (no backtracking or recursion like DP).
> 

---

## ✅ Characteristics of Greedy Problems

- You are asked to **maximize** or **minimize** something.
- Each decision is **independent** of the others.
- Once a choice is made, it cannot be **undone**.
- The solution is often found using a **single pass** or by **sorting + iteration**.
- There’s no **overlapping subproblems** like in dynamic programming.

---

## 🧩 Strategy for Solving Greedy Problems

1. **Understand the problem constraints**.
2. Look for a **greedy choice property**:
    
    > Can I make a choice that looks best now and never look back?
    > 
3. Simulate your idea on small test cases.
4. Prove (or at least intuitively argue) why your greedy choice works.
5. If greedy fails, try brute force or dynamic programming.

---

## 🧪 Classic Greedy Pattern in Code

```cpp
for (each step or index) {
    if (making this move gives me the best outcome) {
        make the move;
    }
}

```

---

## ✅ Example You’ve Already Solved: `maximum69Number`

```cpp
int maximum69Number(int num) {
    string k = to_string(num);
    for(int i = 0; i < k.size(); i++) {
        if(k[i] == '6') {
            k[i] = '9'; // greedy move: change the first '6' to '9'
            break;
        }
    }
    return stoi(k);
}

```

- Greedy move: change **first** '6' to '9' (leftmost has highest value).
- It’s greedy because: **locally best = globally best**.

---

## 🧠 Must-Practice Beginner Greedy Problems

| Problem | Platform | Why It’s Useful |
| --- | --- | --- |
| Maximum 69 Number | LeetCode | Basic greedy idea |
| Monotonic Array | LeetCode | Thinking about trends |
| Assign Cookies | LeetCode | Sorting + matching |
| Lemonade Change | LeetCode | Greedy with currency |
| Greedy Florist | HackerRank | Greedy + sorting |
| Jump Game | LeetCode | Greedy range extension |
| Gas Station | LeetCode | Local to global decision |
| Activity Selection | GFG | Classic greedy + intervals |

---

## 📺 Recommended Resource

- [**Take U Forward – Greedy Playlist on YouTube**](https://www.youtube.com/playlist?list=PLgUwDviBIf0qVw2U4U2JkBAa5oqkJcZ21)
    
    Covers real interview-style greedy problems from easy to hard.
    

---

## 🚀 Final Tips

- Always try **dry running** your greedy idea.
- Use brute force to cross-check your greedy solution.
- Not every problem is greedy — if your greedy idea fails on edge cases, consider **dynamic programming**.

---

Let me know if you want a printable PDF or flashcard version of this!