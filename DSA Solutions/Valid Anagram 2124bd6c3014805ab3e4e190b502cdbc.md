# Valid Anagram

Difficulty: easy
 : Yes
: June 14, 2025
Problem: hashtable/freq method, sort, string
Time Taken: 5 minutes

## Two Approaches to Solve Valid Anagram

### 1. Sorting Approach

The first approach involves sorting both strings s and t, then comparing them character by character. If any mismatch is found, the strings are not anagrams.

```
bool isAnagram(string s, string t) {
    sort(s.begin(), s.end());
    sort(t.begin(), t.end());
    return s == t;
}

```

Time Complexity: O(n log n) due to sorting operation

### 2. HashMap Approach

A more efficient approach uses two hashmaps to store character frequencies:

```
bool isAnagram(string s, string t) {
    unordered_map<char, int> sMap;
    unordered_map<char, int> tMap;
    
    // Count frequencies
    for(char c : s) sMap[c]++;
    for(char c : t) tMap[c]++;
    
    // Compare frequencies
    for(auto pair : sMap) {
        if(tMap[pair.first] != pair.second)
            return false;
    }
    return sMap.size() == tMap.size();
}

```

Time Complexity: O(n)
Space Complexity: O(n) is higher

It can also be solved using frequency array method or array counting method