# Minimum Number of Operations to Convert Time

Difficulty: easy
 : Yes
: June 28, 2025
Problem: array, greedy
Time Taken: 30 minutes

Absolutely, Ali. Here's a **complete, structured breakdown** of your **journey through this problem**, including:

- Your original thought process

# Notes: Convert Time Using Minimum Operations

---

## ✅ Problem Summary:

Convert a given `current` time to a `correct` time using the fewest operations.

Each operation can **add**:

- 60 minutes
- 15 minutes
- 5 minutes
- 1 minute

---

## ✅ Goal:

Minimize the number of operations to reach the correct time from the current time.

---

## 🧩 Step-by-Step Breakdown of Your Journey

---

### 🔹 **Attempt 1: Naive Logic — Separate Hours & Minutes**

### Code:

```cpp
int diff1 = hours_diff;
int diff2 = minutes_diff;
int total = diff1;
while (diff2>0) {
    if (diff2 - 15 >= 0)
        diff2 -= 15, total++;
    else if (diff2 - 1 >= 0)
        diff2 -= 5, total++;
    else
        diff2--, total++;
}

```

### Mistakes:

- ✅ You broke the problem into hours and minutes, which is a good instinct.
- ❌ But logic like `diff2 - 1 >= 0` followed by `diff2 -= 5` caused **wrong behavior** — subtracting 5 even when less than 5 remains.
- ❌ Didn’t use a clean greedy loop over steps.
- ❌ Mixed logic: checking for `>= 1` but subtracting 5.

---

### 🔹 **Attempt 2: Coin-Change Intuition, but Flawed Total Update**

```cpp
int total = 0;
while (minutes>0) {
    if(minutes/60>=1){
        minutes%=60, total = minutes/60;
    }else if (minutes / 15 >=1)
        minutes %= 15, total = minutes/15;
    ...
}

```

### Mistakes:

- ✅ Used minutes instead of hours + minutes separately — **great step forward**.
- ❌ Used `total =` instead of `total +=` — **overwriting total** instead of accumulating operations.
- Result: Wrong answer (like 6 instead of 32)

---

### 🔹 **Attempt 3: Fixed Assignment Bug, Used `+=` Properly**

```cpp
while (minutes>0) {
    if(minutes/60>=1){
        total += minutes/60;
        minutes %= 60;
    } else if (...) ...
}

```

### ✅ Improvements:

- ✅ Logic fixed by using `+=` correctly.
- ✅ Clean greedy breakdown.
- ✅ Correct output (e.g., 32 for `00:00` to `23:59`).

---

### 🔹 **Final Optimization: Clean, Loop-based Greedy**

You also accepted the more refined solution using a loop over denominations:

```cpp
for (int step : {60, 15, 5, 1}) {
    total += minutes / step;
    minutes %= step;
}

```

### ✅ Pros:

- Concise, readable, clean.
- Follows greedy pattern properly.
- Matches top-rated solutions.

---

## ✅ Your Final (Fully Working) Solution

```cpp
class Solution {
public:
    int convertTime(string current, string correct) {
        int diff1 = 0;
        int diff2 = 0;

        string s = correct.substr(0, 2);
        string s1 = correct.substr(3, 2);
        diff1 = stoi(s);
        diff2 = stoi(s1);
        s = current.substr(0, 2);
        s1 = current.substr(3, 2);
        diff1 -= stoi(s);
        diff2 -= stoi(s1);
        int minutes = (diff1 * 60) + diff2;
        int total = 0;
        while (minutes > 0) {
            if (minutes / 60 >= 1) {
                total += minutes / 60;
                minutes %= 60;
            } else if (minutes / 15 >= 1) {
                total += minutes / 15;
                minutes %= 15;
            } else if (minutes / 5 >= 1) {
                total += minutes / 5;
                minutes %= 5;
            } else {
                total++;
                minutes--;
            }
        }
        return total;
    }
};

```

---

## 🧠 What You Learned from This Journey

| # | Learning |
| --- | --- |
| ✅ | Break time into a consistent unit (minutes) for easier manipulation |
| ✅ | Use greedy algorithms when local optimal choices lead to global optimum |
| ✅ | Always **accumulate**, don’t overwrite values in loops (`+=` not `=`) |
| ❌ | Mistakes happen — off-by-one, typos, logic errors — but debugging grows your skill |
| ✅ | Use structured thinking (coin change style) for problems with multiple "step sizes" |
| ✅ | Dry running is crucial to catch subtle logic errors |
| ✅ | You grew from messy conditionals to clean greedy abstraction |

---

## 🏁 Summary

Your journey was **textbook growth**:

- Started with scattered logic and condition errors ✅
- Spotted a typo and corrected your own mistake ✅
- Refined into clean greedy breakdown ✅
- Verified correctness via dry runs ✅
- Reached FAANG-style optimal solution ✅

Would you like me to save this in your Greedy Patterns master note or make a printable PDF?