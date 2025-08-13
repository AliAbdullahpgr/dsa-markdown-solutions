# Top K Frequent Elements

Difficulty: medium
 : Yes
: June 18, 2025
Problem: array, hashtable/freq method, sort
Time Taken: 1 hour+

### ❌ Couldn’t Come Up With a Solution On My Own

- I tried creating a **hashmap** with each element and its frequency — which *was* the right approach.
- But I couldn’t come up with a solution better than `O(n²)` to extract the top frequent elements from this hashmap.

---

### ✅ I Found Two Approaches That Work:

---

## **1️⃣ Frequency Sorting Method**

- First, create a hashmap `m` that maps each element to its frequency.
- Then, push each `(frequency, element)` pair into a vector of pairs or 2D vector.
- Reason: When we sort the vector, it sorts based on the **first element** of the pair, i.e., frequency.

```cpp
vector<pair<int, int>> freqVector;
for (auto [element, freq] : m) {
    freqVector.push_back({freq, element});
}

// Sort in descending order of frequency
sort(freqVector.rbegin(), freqVector.rend());

```

- Now, traverse the vector and take the top `k` elements (accessed by `freqVector[i].second`).
- ✅ **Time Complexity**: `O(n log n)` due to sorting.

---

## **2️⃣ Reverse Bucket Sort Approach** 🪣

> 🌟 This is the smarter and more efficient one.
> 
> 
> I like to call it the **"Reverse Bucket Sort"** because it's like bucket sort — but backward!
> 

### 🔧 How it works:

- Create a 2D vector (array of buckets) of size `n + 1`, where `n` is the size of the input array.
- Instead of storing frequency **at index = element**,
    
    we store **elements at index = frequency**.
    

```cpp
vector<vector<int>> buckets(nums.size() + 1);
for (auto [element, freq] : m) {
    buckets[freq].push_back(element);  // reverse bucket mapping
}

```

---

### 📊 Example:

Input: `nums = [1, 1, 2, 2, 3]`

Frequencies:

- 1 → 2 times
- 2 → 2 times
- 3 → 1 time

### Buckets Table (`index = frequency`):

| Frequency (Index) | Elements |
| --- | --- |
| 0 | - |
| 1 | [3] |
| 2 | [1, 2] |
| 3..n | [] |

---

### 🚀 Now, Traverse in Reverse:

- Traverse the `buckets` array **from end to start** (i.e., highest frequency to lowest).
- Keep collecting elements until we have `k` elements.

```cpp
vector<int> result;
for (int i = buckets.size() - 1; i >= 0 && result.size() < k; i--) {
    for (int num : buckets[i]) {
        result.push_back(num);
        if (result.size() == k) break;
    }
}

```

---

### ✅ Advantages:

- This is **almost genius** because:
    - It's clean.
    - The elements with higher frequency naturally appear at the back.
    - No sorting needed.
- ✅ **Time Complexity**: `O(n)` average — more efficient than the sorting method!

---