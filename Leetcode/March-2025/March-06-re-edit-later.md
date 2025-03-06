# 2965. Find Missing and Repeated Values

## Problem Statement
You are given a 0-indexed 2D integer matrix `grid` of size `n * n` with values in the range `[1, n^2]`. Each integer appears exactly once except a number `a`, which appears twice, and a number `b`, which is missing. The task is to find the repeating and missing numbers `a` and `b`.

Return a 0-indexed integer array `ans` of size `2` where `ans[0]` equals `a` and `ans[1]` equals `b`.

## Example 1:

### Input:
```python
grid = [[1,3],[2,2]]
```
### Output:
```python
[2,4]
```
### Explanation:
Number `2` is repeated and number `4` is missing, so the answer is `[2,4]`.

## Example 2:

### Input:
```python
grid = [[9,1,7],[8,9,2],[3,4,6]]
```
### Output:
```python
[9,5]
```
### Explanation:
Number `9` is repeated and number `5` is missing, so the answer is `[9,5]`.

---

## Approach

### **Concept of the Approach:**
1. **Frequency Counting:**
   - Traverse the grid and count occurrences of each number using a dictionary.
   - Identify the number that appears twice (repeated) and the number that does not appear at all (missing).

### **Algorithm Steps:**
1. Initialize a dictionary to store the frequency of each number in the grid.
2. Iterate through the grid and populate the dictionary.
3. Iterate from `1` to `n^2` to check:
   - Which number is missing (i.e., not present in the dictionary).
   - Which number appears twice (i.e., has a frequency of `2`).
4. Return the repeated and missing numbers as a list.

---

## **Code (Python)**

### Solution 1: Using a Dictionary for Frequency Counting

```python
from typing import List

class Solution:
    def findMissingAndRepeatedValues(self, grid: List[List[int]]) -> List[int]:
        n = len(grid)
        freq = {}

        # Store frequency of each number in the grid
        for row in grid:
            for num in row:
                freq[num] = freq.get(num, 0) + 1

        # Check numbers from 1 to n^2 to find missing and repeated values
        for num in range(1, n * n + 1):
            if num not in freq:
                missing = num  # Number not present in grid
            elif freq[num] == 2:
                repeat = num  # Number appears twice

        return [repeat, missing]
```

---

## **Time and Space Complexity Analysis**

### **Time Complexity:**
- **O(n^2)**: We iterate through the grid once (`O(n^2)`) and then iterate through numbers from `1` to `n^2` (`O(n^2)`). The operations inside these loops are constant time, making the overall complexity **O(n^2)**.

### **Space Complexity:**
- **O(n^2)**: The dictionary stores frequencies of numbers in the range `[1, n^2]`, which requires **O(n^2)** space.

---

This approach efficiently finds the missing and repeated numbers while maintaining a straightforward and readable implementation.

