# Remove Nth Node

Difficulty: medium
 : Yes
: July 10, 2025
Problem: linked list, stack/queue, two pointers
Time Taken: 30 minutes

# Remove Nth Node From End of List - Solution Analysis

## Problem Understanding

- Remove the nth node from the end of a singly linked list
- Return the head of the modified list
- Examples: `[1,2,3,4,5], n=2` → `[1,2,3,5]` (remove node 4)

## My Approach: Two-Pass with Position Conversion

### Core Strategy

1. **Find the total length** of the linked list
2. **Convert the problem**: "nth from end" → "kth from start"
    - Formula: `k = length - n`
3. **Use two-pointer technique** to traverse to the target position
4. **Remove the node** using: `prev->next = curr->next`

### Implementation Breakdown

```cpp
// Step 1: Calculate total length
int length = 0;
ListNode* curr = head;
while(curr) {
    curr = curr->next;
    length++;
}

// Step 2: Handle edge case - removing head node
if(n == length) {
    head = head->next;
    return head;
}

// Step 3: Convert position (nth from end → kth from start)
n = length - n;

// Step 4: Traverse to find node before target
int count = 0;
ListNode* prev = head;
curr = head;
while(curr && count < n) {
    prev = curr;
    curr = curr->next;
    count++;
}

// Step 5: Remove the target node
if(count == n) {
    prev->next = curr->next;
}

```

## Key Insights & Difficulties Faced

### 1. **Position Conversion Logic**

- **Challenge**: Understanding how to convert "nth from end" to "kth from start"
- **Solution**: `k = length - n`
- **Example**: List `[1,2,3,4,5]`, remove 2nd from end (node 4)
    - `length = 5`, `n = 2`
    - `k = 5 - 2 = 3` → remove 3rd node from start (0-indexed)

### 2. **Edge Case: Removing Head Node**

- **Challenge**: When `n == length`, we need to remove the first node
- **Problem**: Regular two-pointer logic doesn't work for head removal
- **Solution**: Special case handling:
    
    ```cpp
    if(n == length) {    head = head->next;    return head;}
    
    ```
    

### 3. **Two-Pointer Traversal**

- **Challenge**: Correctly positioning `prev` and `curr` pointers
- **Key insight**:
    - `prev` should point to the node **before** the one to delete
    - `curr` should point to the node **to be deleted**
- **Removal technique**: `prev->next = curr->next` (bypass the target node)

### 4. **Off-by-One Errors**

- **Challenge**: Getting the correct position calculations
- **Solution**: Careful tracking of `count` variable and loop conditions

## Algorithm Complexity

- **Time Complexity**: O(n) - Two passes through the list
- **Space Complexity**: O(1) - Only using a few pointers

## Debugging Process

1. **Initial bug**: Didn't handle head removal case
2. **Fix**: Added special condition `if(n == length)`
3. **Testing**: Verified with edge cases like single node and head removal

## Alternative Approaches

- **One-pass solution**: Two pointers with gap of `n` nodes
- **Stack-based**: Push all nodes, then pop `n` times
- **My approach**: Two-pass with position conversion

## Lessons Learned

1. **Always consider edge cases** (especially head node operations)
2. **Position conversion** can simplify complex problems
3. **Two-pointer technique** is versatile for linked list problems
4. **Dry running** helps catch logical errors early

## When to Use This Approach

- When you need to understand the problem step-by-step
- When debugging complex pointer logic
- When position conversion makes the problem clearer
- Good for learning fundamental linked list operations