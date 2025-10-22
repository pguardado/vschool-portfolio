## Problem Summary

The problem is to find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

- Only numbers 1 through 9 are used.
- Each number is used at most once.

## Logic to Solve

The solution involves using backtracking to generate all possible combinations of `k` numbers from 1 to 9 that sum up to `n`. The approach can be summarized as follows:

1. Use a recursive function to generate combinations of `k` numbers.
2. Iterate through numbers from 1 to 9 and try adding them to the current combination if they haven't been used before.
3. Keep track of the current sum and the number of elements in the combination.
4. If the current sum equals `n` and the number of elements equals `k`, add the combination to the result list.
5. Otherwise, continue exploring other numbers by recursively calling the function with updated parameters.
6. Backtrack by removing the last added number from the combination before trying the next number.

## Step-by-Step Analysis

1. **Initialization**:
   - Initialize an empty array to store the result combinations.
2. **Backtracking**:
   - Use a recursive function to generate combinations of `k` numbers.
   - Iterate through numbers from 1 to 9.
   - If a number has not been used before, add it to the current combination and update the sum and count of elements.
   - If the sum equals `n` and the count equals `k`, add the combination to the result list.
   - Otherwise, recursively call the function with updated parameters to explore other numbers.
   - After exploring all possibilities with a number, backtrack by removing it from the combination.
3. **Base Case**:
   - If the count of elements exceeds `k` or the sum exceeds `n`, return from the function.

## Pseudocode

```
function combinationSum3(k, n):
    result = []

    function backtrack(start, count, sum, combination):
        if count === k and sum === n:
            result.push(combination.slice())
            return

        if count > k or sum > n:
            return

        for num from start to 9:
            if num not in combination:
                combination.push(num)
                backtrack(num + 1, count + 1, sum + num, combination)
                combination.pop()

    backtrack(1, 0, 0, [])
    return result
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function combinationSum3(k, n) {
  const result = [];

  function backtrack(start, count, sum, combination) {
    if (count === k && sum === n) {
      result.push([...combination]);
      return;
    }

    if (count > k || sum > n) {
      return;
    }

    for (let num = start; num <= 9; num++) {
      if (!combination.includes(num)) {
        combination.push(num);
        backtrack(num + 1, count + 1, sum + num, combination);
        combination.pop();
      }
    }
  }

  backtrack(1, 0, 0, []);
  return result;
}

// Example usage:
console.log(combinationSum3(3, 7)); // Output: [[1,2,4]]
console.log(combinationSum3(3, 9)); // Output: [[1,2,6],[1,3,5],[2,3,4]]
```

### Explanation

- The `combinationSum3` function initializes an empty array `result` to store the result combinations.
- It defines a `backtrack` function to recursively generate combinations of `k` numbers.
- The `backtrack` function takes parameters `start`, `count`, `sum`, and `combination`, representing the current starting number, the count of elements in the combination, the current sum, and the current combination, respectively.
- It iterates through numbers from `start` to 9 and tries adding each number to the current combination if it hasn't been used before.
- If the count of elements equals `k` and the sum equals `n`, the current combination is added to the `result` array.
- Otherwise, it continues exploring other numbers by recursively calling the `backtrack` function with updated parameters.
- After exploring all possibilities with a number, it backtracks by removing it from the combination before trying the next number.
