# Common Mistakes (Syntax)

: No

---

### ⚠️ Most Common Mistakes I Make

- When going from `n` to `0` in a loop,
    
    I do `i++` instead of `i--`.
    
    ```cpp
    // ❌ Wrong
    for (int i = n; i >= 0; i++) {
        // logic
    }
    
    // ✅ Correct
    for (int i = n; i >= 0; i--) {
        // logic
    }
    
    ```
    

---

- While traversing through a 2D array and pushing values into another 2D array,
    
    I write `array.push_back(first, second)` instead of `array.push_back({first, second})`.
    
    ```cpp
    vector<pair<int, int>> array;
    
    // ❌ Wrong
    array.push_back(first, second);
    
    // ✅ Correct
    array.push_back({first, second});
    
    ```
    

---

I keep repeating these and it messes things up sometimes, especially during contests or while debugging.