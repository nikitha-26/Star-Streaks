# 2161. Partition Array According to Given Pivot
The problem can be found at the following link: [Question Link](https://leetcode.com/problems/partition-array-according-to-given-pivot)
## Problem Description

You are given a 0-indexed integer array `nums` and an integer `pivot`. Rearrange `nums` such that the following conditions are satisfied:

1. Every element less than `pivot` appears before every element greater than `pivot`.
2. Every element equal to `pivot` appears in between the elements less than and greater than `pivot`.
3. The relative order of the elements less than `pivot` and the elements greater than `pivot` is maintained.

More formally, consider every `pi`, `pj` where `pi` is the new position of the `i`-th element and `pj` is the new position of the `j`-th element. If `i < j` and both elements are smaller (or larger) than `pivot`, then `pi < pj`.

Return `nums` after the rearrangement.

### Example 1:

#### Input:
```python
nums = [9, 12, 5, 10, 14, 3, 10]
pivot = 10
```

#### Output:
```python
[9, 5, 3, 10, 10, 12, 14]
```

#### Explanation:
The elements 9, 5, and 3 are less than the pivot, so they are on the left side of the array.
The elements 12 and 14 are greater than the pivot, so they are on the right side of the array.
The relative ordering of the elements less than and greater than pivot is also maintained. [9, 5, 3] and [12, 14] are the respective orderings.

### Example 2:

#### Input:
```python
nums = [-3, 4, 3, 2]
pivot = 2
```

#### Output:
```python
[-3, 2, 4, 3]
```

#### Explanation:
The element -3 is less than the pivot, so it is on the left side of the array.
The elements 4 and 3 are greater than the pivot, so they are on the right side of the array.
The relative ordering of the elements less than and greater than pivot is also maintained. [-3] and [4, 3] are the respective orderings.

---

## Approach

The problem can be solved using a three-partition approach:
1. First, we create three separate lists:
   - A list for elements less than `pivot`.
   - A list for elements equal to `pivot`.
   - A list for elements greater than `pivot`.
2. After populating these lists, we concatenate them in the order of: `less + pivot + greater`.
3. This ensures that elements less than the pivot come first, followed by elements equal to the pivot, and finally, elements greater than the pivot, while preserving their relative order.

### Time Complexity:
- **O(n)**: We iterate over the list once to partition it into the three lists. `n` is the length of the input array.

### Space Complexity:
- **O(n)**: We create three separate lists to hold the values, which takes up extra space proportional to the size of the input array.

---

## Code (Python)

### Solution 1 (Using Separate Lists for Partitioning):
```python
class Solution:
    def pivotArray(self, nums: List[int], pivot: int) -> List[int]:
        less = []
        greater = []
        n = []
        for i in range(len(nums)):
            if nums[i] < pivot:
                less.append(nums[i])
            elif nums[i] > pivot:
                greater.append(nums[i])
            else:
                n.append(nums[i])
        return less + n + greater
```

### Solution 2 (Using List Comprehension):
```python
class Solution:
    def pivotArray(self, nums: List[int], pivot: int) -> List[int]:
        return [num for num in nums if num < pivot] + [num for num in nums if num == pivot] + [num for num in nums if num > pivot]
```

---

## Explanation

### Solution Explanation:

In both solutions, we divide the array into three parts:
1. **Less than pivot**: We append all the elements smaller than the `pivot`.
2. **Equal to pivot**: We append all the elements equal to `pivot`.
3. **Greater than pivot**: We append all the elements larger than the `pivot`.

By joining these three lists, we get the desired rearrangement of the array, maintaining the relative order of the elements.

---

## Example Walkthrough:

### Example 1:
#### Input:
```python
nums = [9, 12, 5, 10, 14, 3, 10]
pivot = 10
```

- Elements less than pivot: `[9, 5, 3]`
- Elements equal to pivot: `[10, 10]`
- Elements greater than pivot: `[12, 14]`

Concatenate the three lists: `[9, 5, 3] + [10, 10] + [12, 14]`

#### Output:
```python
[9, 5, 3, 10, 10, 12, 14]
```

### Example 2:
#### Input:
```python
nums = [-3, 4, 3, 2]
pivot = 2
```

- Elements less than pivot: `[-3]`
- Elements equal to pivot: `[2]`
- Elements greater than pivot: `[4, 3]`

Concatenate the three lists: `[-3] + [2] + [4, 3]`

#### Output:
```python
[-3, 2, 4, 3]
```

