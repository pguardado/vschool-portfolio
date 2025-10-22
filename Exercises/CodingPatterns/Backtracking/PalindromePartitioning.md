## Problem Summary

The problem is to partition a given string `s` such that every substring of the partition is a palindrome. The goal is to return all possible palindrome partitionings of `s`.

## Logic to Solve

The solution involves using recursion and backtracking to explore all possible partitions of the string and check if each substring is a palindrome. The approach can be broken down into the following steps:

1. Use a helper function to check if a substring is a palindrome.
2. Use a recursive function to generate partitions by adding palindromic substrings to the current partition and recursively partitioning the remaining substring.
3. Backtrack to explore other possible partitions.

## Step-by-Step Analysis

1. **Palindrome Check**:
   - Create a function to check if a given substring is a palindrome.
2. **Initialization**:
   - Use an empty list to store the partitions.
3. **Recursion/Base Case**:
   - If the current index reaches the end of the string, add the current partition to the results list.
   - For each substring starting from the current index, check if it is a palindrome.
   - If it is, add the substring to the current partition and recursively call the function with the next index.
4. **Backtracking**:
   - After exploring a partition, remove the last added substring and explore the next possibility.

## Pseudocode

```
function partition(s):
    results = []

    function isPalindrome(substring):
        return substring == substring[::-1]

    function backtrack(start, currentPartition):
        if start == length of s:
            results.append(copy of currentPartition)
            return

        for end from start to length of s - 1:
            substring = s[start:end + 1]
            if isPalindrome(substring):
                currentPartition.append(substring)
                backtrack(end + 1, currentPartition)
                currentPartition.pop()  # backtrack

    backtrack(0, [])
    return results
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function partition(s) {
  const results = [];

  function isPalindrome(substring) {
    let left = 0;
    let right = substring.length - 1;
    while (left < right) {
      if (substring[left] !== substring[right]) {
        return false;
      }
      left++;
      right--;
    }
    return true;
  }

  function backtrack(start, currentPartition) {
    if (start === s.length) {
      results.push([...currentPartition]);
      return;
    }

    for (let end = start; end < s.length; end++) {
      const substring = s.substring(start, end + 1);
      if (isPalindrome(substring)) {
        currentPartition.push(substring);
        backtrack(end + 1, currentPartition);
        currentPartition.pop(); // backtrack
      }
    }
  }

  backtrack(0, []);
  return results;
}

// Example usage:
console.log(partition("aab"));
```

### Explanation

- The `partition` function initializes an empty array `results` to store the partitions.
- The `isPalindrome` function checks if a given substring is a palindrome by comparing characters from both ends towards the center.
- The `backtrack` function generates partitions starting from the `start` index.
  - If `start` equals the length of the string, a copy of `currentPartition` is added to `results`.
  - For each index from `start` to the end of the string, it checks if the substring from `start` to `end` is a palindrome.
  - If it is, the substring is added to `currentPartition`, and `backtrack` is called recursively with the next index (`end + 1`).
  - After the recursive call, the last added substring is removed to backtrack and explore the next substring.
- The initial call to `backtrack` starts with `start` equal to 0 and an empty `currentPartition`. The function returns `results` after all partitions are generated.
