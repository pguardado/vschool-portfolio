## Problem Summary

The problem is to generate all possible permutations of a given collection of distinct integers. A permutation of a set is a specific arrangement of its elements.

## Logic to Solve

The solution involves generating all possible arrangements of the given integers using recursion and backtracking. For each position in the permutation, we swap elements and recursively generate permutations for the remaining positions.

## Step-by-Step Analysis

1. **Initialization**:
   - Start with an empty list to store the permutations.
   - Use a recursive function to generate permutations by swapping elements.
2. **Recursion/Base Case**:
   - If the current position is the last position in the array, add the current permutation to the results list.
   - For each element in the array starting from the current position, swap it with the current position and recursively generate permutations for the next position.
3. **Backtracking**:
   - After generating permutations for a given position, swap the elements back to restore the original order and explore the next possibility.

## Pseudocode

```
function permute(nums):
    results = []

    function backtrack(start):
        if start == length of nums:
            results.append(copy of nums)
            return

        for i from start to length of nums - 1:
            swap(nums[start], nums[i])
            backtrack(start + 1)
            swap(nums[start], nums[i])  # backtrack

    backtrack(0)
    return results
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function permute(nums) {
  const results = [];

  function backtrack(start) {
    if (start === nums.length) {
      results.push([...nums]); // make a copy of nums
      return;
    }

    for (let i = start; i < nums.length; i++) {
      [nums[start], nums[i]] = [nums[i], nums[start]]; // swap
      backtrack(start + 1);
      [nums[start], nums[i]] = [nums[i], nums[start]]; // swap back (backtrack)
    }
  }

  backtrack(0);
  return results;
}

// Example usage:
console.log(permute([1, 2, 3]));
```

### Explanation

- The `permute` function initializes an empty array `results` to store the permutations.
- The `backtrack` function generates permutations starting from the `start` index.
  - If `start` is equal to the length of `nums`, it means a complete permutation is formed, and a copy of `nums` is added to `results`.
  - For each index from `start` to the end of the array, it swaps the element at `start` with the element at the current index `i`, recursively calls `backtrack` for the next position, and then swaps back (backtracks) to restore the original array.
- The initial call to `backtrack` starts with `start` equal to 0, and the function returns `results` after all permutations are generated.
