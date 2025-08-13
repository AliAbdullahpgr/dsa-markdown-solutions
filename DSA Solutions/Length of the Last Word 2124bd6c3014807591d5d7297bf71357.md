# Length of the Last Word

Difficulty: easy
 : Yes
: June 14, 2025
Problem: string
Time Taken: 20 minutes

I solved this problem using two approaches:

### Approach 1: Reverse Iteration

The first approach involves iterating from the end of the string:

- Start counting from the end of the string
- Mark the first non-space character using a boolean flag
- Stop counting when encountering a space after finding characters
- Return the count

This is a simple O(n) This is the most optimized solution possible.

### Approach 2: Using StringStream

The second approach utilizes C++'s stringstream functionality. A stringstream can split a string into words, making it useful for processing sentences.

Here's how to implement it:

```cpp
stringstream ss(string); // Initialize stringstream with input string
string word;
while(ss >> word) {
    // Each iteration processes one word
}
return word.length(); // Returns length of last word

```

The stringstream automatically traverses through the string, storing each word in the 'word' variable. The final iteration contains the last word, whose length we return.t word