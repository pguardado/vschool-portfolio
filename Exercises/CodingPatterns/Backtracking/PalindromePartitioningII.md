## Problem Summary

The problem is to find the minimum number of cuts needed to partition a given string `s` into substrings such that each substring is a palindrome.

## Logic to Solve

The solution involves dynamic programming to determine the minimum cuts needed for palindrome partitioning. The approach can be summarized as follows:

1. Use dynamic programming to preprocess the string and store whether each substring is a palindrome.
2. Initialize an array `cuts` to store the minimum cuts needed at each index of the string.
3. Iterate through each index of the string and consider all possible substrings ending at that index.
4. If a substring is a palindrome, update the minimum cuts at the current index based on the minimum cuts at the start of the palindrome plus one.
5. After iterating through all indices, the value at the last index of the `cuts` array represents the minimum cuts needed for palindrome partitioning.

## Step-by-Step Analysis

1. **Preprocessing**:
   - Use dynamic programming to preprocess the string and store whether each substring is a palindrome.
2. **Initialization**:
   - Initialize an array `cuts` to store the minimum cuts needed at each index.
   - Initialize `cuts[i]` to `i` for all `i` from 0 to `n-1`, where `n` is the length of the string.
3. **Dynamic Programming**:
   - Iterate through each index `i` of the string.
   - Consider all possible substrings ending at index `i` and check if each substring is a palindrome.
   - If a substring is a palindrome, update `cuts[i]` based on the minimum cuts at the start of the palindrome plus one.
4. **Result**:
   - The value at the last index of the `cuts` array represents the minimum cuts needed for palindrome partitioning.

## Pseudocode

```
function minCut(s):
    n = length of s
    isPalindrome = 2D array of size n x n initialized to false
    cuts = array of size n initialized to n

    for i from 0 to n-1:
        for j from 0 to i:
            if s[j] == s[i] and (i - j <= 1 or isPalindrome[j+1][i-1]):
                isPalindrome[j][i] = true

    for i from 0 to n-1:
        if isPalindrome[0][i]:
            cuts[i] = 0
        else:
            for j from 0 to i-1:
                if isPalindrome[j+1][i]:
                    cuts[i] = min(cuts[i], cuts[j] + 1)

    return cuts[n-1]
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function minCut(s) {
  const n = s.length;
  const isPalindrome = Array.from({ length: n }, () => Array(n).fill(false));
  const cuts = new Array(n).fill(n);

  for (let i = 0; i < n; i++) {
    for (let j = 0; j <= i; j++) {
      if (s[j] === s[i] && (i - j <= 1 || isPalindrome[j + 1][i - 1])) {
        isPalindrome[j][i] = true;
      }
    }
  }

  for (let i = 0; i < n; i++) {
    if (isPalindrome[0][i]) {
      cuts[i] = 0;
    } else {
      for (let j = 0; j < i; j++) {
        if (isPalindrome[j + 1][i]) {
          cuts[i] = Math.min(cuts[i], cuts[j] + 1);
        }
      }
    }
  }

  return cuts[n - 1];
}

// Example usage:
console.log(minCut("aab")); // Output: 1
console.log(minCut("a")); // Output: 0
```

### Explanation

- The `minCut` function preprocesses the string to determine whether each substring is a palindrome and calculates the minimum cuts needed for palindrome partitioning.
- It initializes a 2D array `isPalindrome` to store whether each substring is a palindrome.
- It initializes an array `cuts` to store the minimum cuts needed at each index of the string.
- It iterates through each index of the string to check all possible substrings and updates `isPalindrome`.
- It then iterates through each index again to calculate the minimum cuts based on palindrome substrings.
- The value at the last index of the `cuts` array represents the minimum cuts needed for palindrome partitioning.
