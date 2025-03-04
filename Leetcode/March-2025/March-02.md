# 2570. Merge Two 2D Arrays by Summing Values

The problem can be found at the following link: [Question Link](https://leetcode.com/problems/merge-two-2d-arrays-by-summing-values)

## Problem Description

You are given two 2D integer arrays `nums1` and `nums2`.

- `nums1[i] = [idi, vali]` indicates that the number with the id `idi` has a value equal to `vali`.
- `nums2[i] = [idi, vali]` indicates that the number with the id `idi` has a value equal to `vali`.

Each array contains unique ids and is sorted in ascending order by id.

Merge the two arrays into one array that is sorted in ascending order by id, respecting the following conditions:

- Only ids that appear in at least one of the two arrays should be included in the resulting array.
- Each id should be included only once and its value should be the sum of the values of this id in the two arrays. If the id does not exist in one of the two arrays, then assume its value in that array to be 0.
- Return the resulting array. The returned array must be sorted in ascending order by id.

---

### Example 1:

#### Input:
```python
nums1 = [[1, 2], [2, 3], [4, 5]]
nums2 = [[1, 4], [3, 2], [4, 1]]
```

#### Output:
```python
[[1, 6], [2, 3], [3, 2], [4, 6]]
```

#### Explanation:
The resulting array contains the following:
- id = 1, the value of this id is 2 + 4 = 6.
- id = 2, the value of this id is 3.
- id = 3, the value of this id is 2.
- id = 4, the value of this id is 5 + 1 = 6.

---

### Example 2:

#### Input:
```python
nums1 = [[2, 4], [3, 6], [5, 5]]
nums2 = [[1, 3], [4, 3]]
```

#### Output:
```python
[[1, 3], [2, 4], [3, 6], [4, 3], [5, 5]]
```

#### Explanation:
There are no common ids, so we just include each id with its value in the resulting list.

---

## Approach

### Approach 1: Using `defaultdict` to Sum Values

1. Use a dictionary (`defaultdict`) to accumulate the sum of values for each id.
2. Iterate over both arrays and add the values for each id to the dictionary.
3. After processing both arrays, convert the dictionary into a list and sort it by id.

#### Time Complexity:
- **O(n + m)**: We process both arrays once (where `n` and `m` are the lengths of `nums1` and `nums2`, respectively).
- Sorting the dictionary will take \(O(k \log k)\) where `k` is the number of unique ids in the resulting array.

#### Space Complexity:
- **O(k)**: We use a dictionary to store the sum of values for each id.

### Code (Python):
```python
from collections import defaultdict

class Solution:
    def mergeArrays(self, nums1: List[List[int]], nums2: List[List[int]]) -> List[List[int]]:
        summed_values = defaultdict(int)
        for i, v in nums1:
            summed_values[i] += v
        for i, v in nums2:
            summed_values[i] += v
        result = [[i, v] for i, v in summed_values.items()]
        result.sort(key=lambda x: x[0])
        return result
```

---

### Approach 2: Using Two Pointers to Merge Arrays

1. Use two pointers to traverse both sorted arrays simultaneously.
2. Compare ids from both arrays and decide which one to add to the result.
3. If the ids match, sum the values and move both pointers forward.
4. After the traversal, append any remaining ids from either array to the result.

#### Time Complexity:
- **O(n + m)**: We process both arrays once (where `n` and `m` are the lengths of `nums1` and `nums2`).
- No sorting required, as arrays are already sorted.

#### Space Complexity:
- **O(n + m)**: We use space to store the resulting array.

### Code (Python):
```python
class Solution:
    def mergeArrays(self, nums1: List[List[int]], nums2: List[List[int]]) -> List[List[int]]:
        i, j = 0, 0
        result = []
        
        # Traverse both arrays with two pointers
        while i < len(nums1) and j < len(nums2):
            id1, val1 = nums1[i]
            id2, val2 = nums2[j]
            
            if id1 < id2:
                result.append([id1, val1])
                i += 1
            elif id2 < id1:
                result.append([id2, val2])
                j += 1
            else:
                result.append([id1, val1 + val2])
                i += 1
                j += 1
        
        # Add remaining elements from nums1
        while i < len(nums1):
            result.append(nums1[i])
            i += 1
        
        # Add remaining elements from nums2
        while j < len(nums2):
            result.append(nums2[j])
            j += 1
        
        return result
```

---

## Explanation

### Approach 1 Explanation:
- We use `defaultdict(int)` to initialize the sum of values for each id.
- We iterate through both `nums1` and `nums2`, adding the value of each id to the dictionary.
- After processing both arrays, we create a result list by extracting the dictionary values, and then sort it by the id.

### Approach 2 Explanation:
- We maintain two pointers `i` and `j` to traverse both `nums1` and `nums2`.
- We compare the ids at `nums1[i]` and `nums2[j]` to decide which id to add to the result array.
- If ids are equal, we sum their values and move both pointers forward.
- After the main loop, we append any remaining ids from either array.

---

## Example Walkthrough:

### Example 1:
#### Input:
```python
nums1 = [[1, 2], [2, 3], [4, 5]]
nums2 = [[1, 4], [3, 2], [4, 1]]
```

- After merging, we have:
  - id = 1: sum = 2 + 4 = 6
  - id = 2: sum = 3
  - id = 3: sum = 2
  - id = 4: sum = 5 + 1 = 6

#### Output:
```python
[[1, 6], [2, 3], [3, 2], [4, 6]]
```

### Example 2:
#### Input:
```python
nums1 = [[2, 4], [3, 6], [5, 5]]
nums2 = [[1, 3], [4, 3]]
```

- There are no common ids, so we just include each id with its value in the result.

#### Output:
```python
[[1, 3], [2, 4], [3, 6], [4, 3], [5, 5]]
```
