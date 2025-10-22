## Problem Summary
The problem is to find all possible subsets (the power set) of an integer array `nums`, which may contain duplicates.

## Logic to Solve
The solution involves backtracking to generate all possible subsets. The approach can be summarized as follows:
1. Sort the array to handle duplicates efficiently.
2. Use a recursive backtracking function to generate all possible subsets.
3. At each step, consider two choices:
   - Include the current element in the subset.
   - Exclude the current element from the subset.
4. Continue exploring all possible combinations recursively.
5. Finally, return the list of valid subsets.

## Step-by-Step Analysis
1. **Initialization**:
   - Initialize an empty array to store the result subsets.
2. **Backtracking**:
   - Use a recursive backtracking function to generate all possible subsets.
   - At each step, consider two choices:
     - Include the current element in the subset by adding it to the current subset.
     - Exclude the current element from the subset.
   - Continue exploring all possible combinations recursively.
3. **Base Case**:
   - If the index reaches the length of the array, add the current subset to the result list.
4. **Result**:
   - The result list contains all valid subsets.

## Pseudocode
```
function subsets(nums):
    result = []
    nums.sort()
    
    function backtrack(start, subset):
        result.push(subset.slice())
        
        for i from start to nums.length - 1:
            if i > start && nums[i] === nums[i - 1]:
                continue
            subset.push(nums[i])
            backtrack(i + 1, subset)
            subset.pop()
    
    backtrack(0, [])
    return result
```

## JavaScript Solution
Here is the implementation of the above logic in JavaScript:

```javascript
function subsets(nums) {
    const result = [];
    nums.sort((a, b) => a - b); // Sort to handle duplicates
    
    function backtrack(start, subset) {
        result.push(subset.slice());
        
        for (let i = start; i < nums.length; i++) {
            if (i > start && nums[i] === nums[i - 1]) {
                continue; // Skip duplicates
            }
            subset.push(nums[i]);
            backtrack(i + 1, subset);
            subset.pop();
        }
    }
    
    backtrack(0, []);
    return result;
}

// Example usage:
console.log(subsets([1, 2, 2])); // Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
console.log(subsets([1, 2, 3])); // Output: [[],[1],[1,2],[1,2,3],[1,3],[2],[2,3],[3]]
```

### Explanation
- The `subsets` function initializes an empty array `result` to store the result subsets.
- It sorts the input array `nums` to handle duplicates efficiently.
- It defines a `backtrack` function to recursively generate all possible subsets.
- The `backtrack` function takes parameters `start` and `subset`, representing the current index to start from and the current subset being explored, respectively.
- At each step, it adds the current subset to the result list.
- It iterates over the remaining elements of the array, skipping duplicates, and recursively explores all possible combinations.
- Finally, it returns the list of valid subsets.