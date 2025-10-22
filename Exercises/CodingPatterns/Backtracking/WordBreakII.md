## Problem Summary

The problem is to find all possible sentences that can be formed by adding spaces in a given string `s` such that each word formed after splitting by spaces is a valid word in the dictionary `wordDict`.

## Logic to Solve

The solution involves backtracking to generate all possible sentences. The approach can be summarized as follows:

1. Use a recursive backtracking function to generate all possible sentences.
2. At each step, consider all possible prefixes of the string and check if they are valid words in the dictionary `wordDict`.
3. If a valid word is found, recursively explore further by considering the remaining suffix of the string.
4. If the entire string is processed, add the current sentence to the result list.
5. Continue exploring all possible combinations recursively.
6. Finally, return the list of valid sentences.

## Step-by-Step Analysis

1. **Initialization**:
   - Initialize an empty array to store the result sentences.
2. **Backtracking**:
   - Use a recursive backtracking function to generate all possible sentences.
   - At each step, consider all possible prefixes of the string and check if they are valid words in the dictionary `wordDict`.
   - If a valid word is found, recursively explore further by considering the remaining suffix of the string.
   - If the entire string is processed, add the current sentence to the result list.
3. **Base Case**:
   - If the entire string is processed, add the current sentence to the result list.
4. **Result**:
   - The result list contains all valid sentences.

## Pseudocode

```
function wordBreak(s, wordDict):
    result = []

    function backtrack(index, sentence):
        if index === s.length:
            result.push(sentence.trim())
            return

        for i from index to s.length - 1:
            if wordDict.includes(s.substring(index, i + 1)):
                backtrack(i + 1, sentence + s.substring(index, i + 1) + ' ')

    backtrack(0, '')
    return result
```

## JavaScript Solution

Here is the implementation of the above logic in JavaScript:

```javascript
function wordBreak(s, wordDict) {
  const result = [];

  function backtrack(index, sentence) {
    if (index === s.length) {
      result.push(sentence.trim());
      return;
    }

    for (let i = index; i < s.length; i++) {
      const word = s.substring(index, i + 1);
      if (wordDict.includes(word)) {
        backtrack(i + 1, sentence + word + " ");
      }
    }
  }

  backtrack(0, "");
  return result;
}

// Example usage:
console.log(wordBreak("catsanddog", ["cat", "cats", "and", "sand", "dog"]));
// Output: ["cats and dog","cat sand dog"]
console.log(
  wordBreak("pineapplepenapple", [
    "apple",
    "pen",
    "applepen",
    "pine",
    "pineapple",
  ])
);
// Output: ["pine apple pen apple","pineapple pen apple","pine applepen apple"]
```

### Explanation

- The `wordBreak` function initializes an empty array `result` to store the result sentences.
- It defines a `backtrack` function to recursively generate all possible sentences.
- The `backtrack` function takes parameters `index` and `sentence`, representing the current index in the string and the current sentence, respectively.
- At each step, it considers all possible prefixes of the string and checks if they are valid words in the dictionary `wordDict`.
- If a valid word is found, it recursively explores further by considering the remaining suffix of the string.
- If the entire string is processed, it adds the current sentence to the result list.
- Finally, it returns the list of valid sentences.
