## Problem Summary

The problem is to find all unique combinations of a given set of candidate numbers that sum up to a target number. Each candidate number can be used only once in each combination. The solution must ensure that the combinations are unique.

## Logic to Solve

The solution involves using recursion and backtracking to explore all possible combinations of the candidate numbers that add up to the target sum. To ensure uniqueness and handle duplicates:

1. Sort the candidate numbers.
2. Use a recursive function to build combinations by adding candidates to the current combination and checking if the sum matches the target.
3. If the sum exceeds the target, backtrack to explore other possibilities.
4. Skip duplicate candidates to avoid generating duplicate combinations.

## Step-by-Step Analysis

1. **Initialization**:
   - Sort the candidate numbers to handle duplicates and facilitate the backtracking process.
   - Use an empty list to store the combinations.
2. **Recursion/Base Case**:
   - If the current sum equals the target, add the current combination to the results list.
   - If the current sum exceeds the target, return to explore other possibilities.
   - For each candidate starting from the current index, add it to the current combination, update the sum, and recursively call the function with the updated parameters.
3. **Backtracking**:
   - After exploring a combination, remove the last added number and explore the next candidate.
   - Skip duplicate candidates by checking if the current candidate is the same as the previous one.

## Pseudocode

```
function combinationSum2(candidates, target):
    results = []
    candidates.sort()

    function backtrack(start, currentCombination, currentSum):
        if currentSum == target:
            results.append(copy of currentCombination)
            return

        if currentSum > target:
            return

        for i from start to length of candidates - 1:
            if i > start and candidates[i] == candidates[i - 1]:
                continue  # skip duplicates

            currentCombination.append(candidates[i])
            backtrack(i + 1, currentCombination, currentSum + candidates[i])
            currentCombination.pop()  # backtrack

    backtrack(0, [], 0)
    return results
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function combinationSum2(candidates, target) {
  const results = [];
  candidates.sort((a, b) => a - b);

  function backtrack(start, currentCombination, currentSum) {
    if (currentSum === target) {
      results.push([...currentCombination]);
      return;
    }

    if (currentSum > target) {
      return;
    }

    for (let i = start; i < candidates.length; i++) {
      if (i > start && candidates[i] === candidates[i - 1]) {
        continue; // skip duplicates
      }

      currentCombination.push(candidates[i]);
      backtrack(i + 1, currentCombination, currentSum + candidates[i]);
      currentCombination.pop(); // backtrack
    }
  }

  backtrack(0, [], 0);
  return results;
}

// Example usage:
console.log(combinationSum2([10, 1, 2, 7, 6, 1, 5], 8));
```

### Explanation

- The `combinationSum2` function initializes an empty array `results` to store the combinations and sorts the `candidates` array.
- The `backtrack` function generates combinations starting from the `start` index.
  - If the `currentSum` equals the `target`, a copy of `currentCombination` is added to `results`.
  - If the `currentSum` exceeds the `target`, the function returns to backtrack and explore other possibilities.
  - For each index from `start` to the end of the `candidates` array:
    - If the current candidate is the same as the previous one (to avoid duplicates), it skips the candidate.
    - Otherwise, the candidate at that index is added to `currentCombination`, and `backtrack` is called recursively with the next index (`i + 1`) and the updated `currentSum`.
    - After the recursive call, the last added candidate is removed to backtrack and explore the next candidate.
- The initial call to `backtrack` starts with `start` equal to 0, an empty `currentCombination`, and `currentSum` equal to 0. The function returns `results` after all combinations are generated.
