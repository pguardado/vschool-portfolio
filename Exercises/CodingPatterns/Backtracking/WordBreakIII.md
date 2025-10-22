## Problem Summary

The problem is to count the number of sentences that can be formed by inserting spaces in a given string `s` such that each substring is a valid word according to the dictionary `wordDict`.

## Logic to Solve

The solution involves dynamic programming to count the number of sentences. The approach can be summarized as follows:

1. Use dynamic programming to create an array to store the number of sentences that can be formed up to each index of the input string.
2. Initialize the base cases of the dynamic programming array.
3. Iterate over each index of the input string and update the dynamic programming array based on the number of sentences that can be formed using the words in the dictionary.
4. Finally, return the count of sentences that can be formed using the entire input string.

## Step-by-Step Analysis

1. **Initialization**:
   - Initialize an array to store the number of sentences that can be formed up to each index of the input string.
2. **Base Cases**:
   - Initialize the first element of the dynamic programming array based on whether the substring up to that index is a valid word.
3. **Dynamic Programming**:
   - Iterate over each index of the input string and update the dynamic programming array based on the number of sentences that can be formed using the words in the dictionary.
4. **Result**:
   - Return the count of sentences that can be formed using the entire input string.

## Pseudocode

```
function wordBreak(s, wordDict):
    n = s.length
    dp = Array(n + 1).fill(0)
    dp[0] = 1

    for i from 1 to n:
        for word in wordDict:
            if s.substring(i - word.length, i) === word:
                dp[i] += dp[i - word.length]

    return dp[n]
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function wordBreak(s, wordDict) {
  const n = s.length;
  const dp = Array(n + 1).fill(0);
  dp[0] = 1;

  for (let i = 1; i <= n; i++) {
    for (const word of wordDict) {
      if (s.substring(i - word.length, i) === word) {
        dp[i] += dp[i - word.length];
      }
    }
  }

  return dp[n];
}

// Example usage:
console.log(wordBreak("catsanddog", ["cat", "cats", "and", "sand", "dog"])); // Output: 2
console.log(
  wordBreak("pineapplepenapple", [
    "apple",
    "pen",
    "applepen",
    "pine",
    "pineapple",
  ])
); // Output: 3
```

### Explanation

- The `wordBreak` function initializes an array `dp` to store the number of sentences that can be formed up to each index of the input string.
- It initializes the base cases of the dynamic programming array based on whether the substring up to that index is a valid word.
- It iterates over each index of the input string and updates the dynamic programming array based on the number of sentences that can be formed using the words in the dictionary.
- Finally, it returns the count of sentences that can be formed using the entire input string.
