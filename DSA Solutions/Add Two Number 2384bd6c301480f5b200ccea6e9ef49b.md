# Add Two Number

Difficulty: medium
 : Yes
: July 22, 2025
Problem: linked list, math
Time Taken: 10-20 minutes

## 🧠 **Add Two Numbers — Notes**

### ❌ **Initial (Incorrect/Bad) Approach**

- **Idea**: Convert both linked lists to strings, reverse them, convert to numbers, add, then convert back to a linked list.

```cpp
string a = "", b = "";
// extract digits and reverse
// convert to long double
// add them and convert back to string

```

- **Problems**:
    - Precision issues (`long double` or even `long long` can't handle very large numbers).
    - Not scalable (linked list can have **hundreds of digits**).
    - Violates constraints — must simulate digit-by-digit addition like manual math.

### ✅ **Correct Approach**

- **Idea**: Simulate elementary school addition.
- Traverse both linked lists simultaneously.
- Add digit by digit, keeping track of carry.
- Create a **new linked list** to store the result.

```cpp
while (l1 || l2 || carry) {
    int val1 = l1 ? l1->val : 0;
    int val2 = l2 ? l2->val : 0;
    int sum = val1 + val2 + carry;
    carry = sum / 10;
    curr->next = new ListNode(sum % 10);
    curr = curr->next;
    l1 = l1 ? l1->next : nullptr;
    l2 = l2 ? l2->next : nullptr;
}

```

### 🔍 **Why use `while (l1 || l2 || carry)`?**

- **`l1 || l2`** — traverse until both lists are finished.
- **`carry`** — edge case where there's leftover carry after the last digit.
    
    🔹 **Example**:
    
    ```
    l1 = [9], l2 = [9] → 9 + 9 = 18 → write 8, carry 1
    But both l1 and l2 are now nullptr, still carry = 1
    Need to process one more digit → 0 + 0 + 1 = 1
    Final result: [8, 1]
    
    ```
    

---

## 🧩 **Key Takeaways**

- ✅ Don't try to turn it into a math problem — **treat it as linked list simulation**.
- ➕ Carry is essential — handle it as a third condition in your loop.
- 🔗 Always **build a new linked list** — the input lists shouldn't be mutated.
- 🚫 Avoid numeric overflows — don’t convert entire linked lists into one number.

---

## 🛠️ **Your Improvements**

- ✅ Recognized your first approach was a workaround.
- ✅ Wrote clean code for the correct approach.
- ✅ Understood carry logic and traversal correctly.
- 🔁 Came back and revisited it, solidifying your understanding.