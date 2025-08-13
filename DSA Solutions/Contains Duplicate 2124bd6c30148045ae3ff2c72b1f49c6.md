# Contains Duplicate

Difficulty: easy
 : Yes
: June 14, 2025
Problem: array, hashtable/freq method, sort
Time Taken: 5 minutes

Use a hashmap or hash set to keep track of elements in the array. Check if each element exists in the array using: 

```
if (set.find(nums[i]) != set.end()) {
    return false;  // duplicate found
}
set.insert(nums[i]);

```

Remember to add elements to the set only after checking. This is a straightforward problem I've solved multiple times before.