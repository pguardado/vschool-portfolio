## Problem Summary

The problem is to count how many palindromic substrings are present in a given string.

## Logic to Solve

The solution involves expanding around each character to find all palindromic substrings. The approach can be summarized as follows:

1. Use a nested loop to iterate over each character in the string.
2. For each character, expand around it to find all palindromic substrings centered at that character.
3. Keep track of the count of palindromic substrings found.
4. Repeat this process for all characters in the string.
5. Finally, return the count of palindromic substrings.

## Step-by-Step Analysis

1. **Initialization**:
   - Initialize a variable to store the count of palindromic substrings.
2. **Expansion**:
   - Use a nested loop to iterate over each character in the string.
   - For each character, expand around it to find all palindromic substrings centered at that character.
   - Keep track of the count of palindromic substrings found.
3. **Result**:
   - The count of palindromic substrings represents the solution.

## Pseudocode

```
function countSubstrings(s):
    count = 0

    function expandAroundCenter(left, right):
        while left >= 0 && right < s.length && s[left] === s[right]:
            count++
            left--
            right++

    for i from 0 to s.length - 1:
        expandAroundCenter(i, i)   // For odd-length palindromes
        expandAroundCenter(i, i+1) // For even-length palindromes

    return count
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function countSubstrings(s) {
  let count = 0;

  function expandAroundCenter(left, right) {
    while (left >= 0 && right < s.length && s[left] === s[right]) {
      count++;
      left--;
      right++;
    }
  }

  for (let i = 0; i < s.length; i++) {
    expandAroundCenter(i, i); // For odd-length palindromes
    expandAroundCenter(i, i + 1); // For even-length palindromes
  }

  return count;
}

// Example usage:
console.log(countSubstrings("abc")); // Output: 3
console.log(countSubstrings("aaa")); // Output: 6
```

### Explanation

- The `countSubstrings` function initializes a variable `count` to store the count of palindromic substrings.
- It defines a `expandAroundCenter` function to expand around a center character and count the palindromic substrings.
- The `expandAroundCenter` function takes parameters `left` and `right`, representing the indices of the characters to expand around.
- It expands outward from the center character(s) and increments the count for each palindromic substring found.
- The main loop iterates over each character in the string and expands around it to find all palindromic substrings.
- Finally, it returns the count of palindromic substrings.
