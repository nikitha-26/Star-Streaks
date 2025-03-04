# *2460. Apply Operations to an Array*

The problem can be found at the following link: [Question Link](https://leetcode.com/problems/apply-operations-to-an-array/)

## **Problem Description**

You are given a **0-indexed** array `nums` of size `n` consisting of non-negative integers.

You need to apply `n - 1` operations to this array where, in the `i`-th operation (0-indexed), you will apply the following on the `i`-th element of `nums`:

- If `nums[i] == nums[i + 1]`, then multiply `nums[i]` by 2 and set `nums[i + 1]` to 0.
- Otherwise, you skip this operation.

After performing all the operations, shift all the `0`'s to the end of the array.

For example, the array `[1,0,2,0,0,1]` after shifting all its `0`'s to the end, is `[1,2,1,0,0,0]`.

Return the resulting array.

### Example 1:

#### Input:
```python
nums = [1,2,2,1,1,0]
```

#### Output:
```python
[1,4,2,0,0,0]
```

#### Explanation:
We do the following operations:
- i = 0: `nums[0]` and `nums[1]` are not equal, so we skip this operation.
- i = 1: `nums[1]` and `nums[2]` are equal, we multiply `nums[1]` by 2 and change `nums[2]` to 0. The array becomes `[1,4,0,1,1,0]`.
- i = 2: `nums[2]` and `nums[3]` are not equal, so we skip this operation.
- i = 3: `nums[3]` and `nums[4]` are equal, we multiply `nums[3]` by 2 and change `nums[4]` to 0. The array becomes `[1,4,0,2,0,0]`.
- i = 4: `nums[4]` and `nums[5]` are equal, we multiply `nums[4]` by 2 and change `nums[5]` to 0. The array becomes `[1,4,0,2,0,0]`.

After that, we shift the `0`'s to the end, which gives the array `[1,4,2,0,0,0]`.

### Example 2:

#### Input:
```python
nums = [0,1]
```

#### Output:
```python
[1,0]
```

#### Explanation:
No operation can be applied, we just shift the `0` to the end.

---

## Approach

### **Concept of the Approach:**

The problem consists of two parts:
1. Apply operations on consecutive elements where values are equal.
2. Move all the zeros to the end while maintaining the relative order of the non-zero elements.

In the first step, for each pair of consecutive elements `nums[i]` and `nums[i+1]`, we check if they are equal. If so, we multiply `nums[i]` by 2 and set `nums[i+1]` to 0. This simulates the operation described in the problem.

In the second step, we need to move all the zeros to the end. To do this, we iterate over the array and place all non-zero elements at the beginning, followed by all the zeros.

### **Algorithm Steps:**
1. Traverse the array and apply the operation on consecutive elements where `nums[i] == nums[i+1]` by multiplying `nums[i]` by 2 and setting `nums[i+1]` to 0.
2. Create a new list where all non-zero elements are at the beginning, followed by zeros.
3. Return the modified list.

### **Time Complexity:**
- **O(n)**: We iterate over the array twice: once to apply operations and once to move non-zero elements. Thus, the time complexity is **O(n)**, where `n` is the length of the array.

### **Space Complexity:**
- **O(1)**: The space complexity is constant because we are modifying the array in place (no extra space is used apart from a few variables).

---

## **Code (Python)**

### Solution 1: In-place modification with swap logic.

```python
class Solution:
    def applyOperations(self, nums: List[int]) -> List[int]:
        count = 0
        # Apply operations on consecutive elements
        for i in range(len(nums)-1):
            if nums[i] == nums[i+1]:
                nums[i] = nums[i] * 2
                nums[i+1] = 0
        
        # Move non-zero elements to the front
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[i], nums[count] = nums[count], nums[i]
                count += 1
        return nums
```

#### **Time Complexity**:
- **O(n)**: We loop through the array once to perform operations and another time to move non-zero elements to the front.
- **n** is the length of the array.

#### **Space Complexity**:
- **O(1)**: The space complexity is constant because we modify the input array in place.

---

### Solution 2: Using list comprehension for zero shifting.

```python
class Solution:
    def applyOperations(self, nums: List[int]) -> List[int]:
        count = 0
        # Apply operations on consecutive elements
        for i in range(len(nums)-1):
            if nums[i] == nums[i+1]:
                nums[i] = nums[i] * 2
                nums[i+1] = 0
        
        # Move non-zero elements to the front
        result = [num for num in nums if num != 0]  # Collect all non-zero numbers
        result.extend([0] * (len(nums) - len(result)))  # Append the necessary zeros
        
        return result
```

#### **Time Complexity**:
- **O(n)**: We iterate through the list twice: once to apply operations and once to create a new list with non-zero values followed by zeros. Both steps take linear time.
- **n** is the length of the array.

#### **Space Complexity**:
- **O(n)**: The space complexity is **O(n)** because we are creating a new list to hold the result (non-zero elements followed by zeros).

---

### Solution 3: Java solution with in-place operations.

```java
class Solution {
    public int[] applyOperations(int[] nums) {
        for(int i = 0; i < nums.length - 1; i++) {
            if(nums[i] == nums[i+1]) {
                nums[i] *= 2;
                nums[i+1] = 0;
            }
        }

        int index = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] != 0) {
                int temp = nums[index];
                nums[index] = nums[i];
                nums[i] = temp;
                index++;
            }
        }
        return nums;
    }
}
```

#### **Time Complexity**:
- **O(n)**: We loop through the array twice: once to apply operations and once to move non-zero elements to the front.
- **n** is the length of the array.

#### **Space Complexity**:
- **O(1)**: The space complexity is constant because the solution modifies the array in place.

---

## **Explanation**

1. We iterate over the array from index `0` to `n-2` (because we're checking `nums[i]` and `nums[i+1]`). 
   - If `nums[i] == nums[i+1]`, we multiply `nums[i]` by 2 and set `nums[i+1]` to 0.
2. After the first loop, we have handled the operations, and now we need to move all the non-zero elements to the beginning of the array. 
   - We do this by using the `count` variable to track the index where the next non-zero element should be placed.
3. We swap the current non-zero element with the element at the `count` position, then increment the `count`.
4. Finally, the array is returned with all zeros at the end.

---

## Example Walkthrough:

### Example 1:
#### Input: `nums = [1,2,2,1,1,0]`

- **Operation 1**: `nums[0] != nums[1]` → Skip.
- **Operation 2**: `nums[1] == nums[2]` → Multiply `nums[1]` by 2 and change `nums[2]` to 0. Array becomes `[1,4,0,1,1,0]`.
- **Operation 3**: `nums[2] != nums[3]` → Skip.
- **Operation 4**: `nums[3] == nums[4]` → Multiply `nums[3]` by 2 and change `nums[4]` to 0. Array becomes `[1,4,0,2,0,0]`.
- **Operation 5**: `nums[4] == nums[5]` → Multiply `nums[4]` by 2 and change `nums[5]` to 0. Array becomes `[1,4,0,2,0,0]`.

After the operations, move the zeros:
- Non-zero elements: `[1, 4, 2]`
- Final result: `[1, 4, 2, 0, 0, 0]`

#### Output: `[1,4,2,0,0,0]`

### Example 2:
#### Input: `nums = [0,1]`

- No operation is possible. 
- Move the zeros: Final result is `[1, 0]`.

#### Output: `[1,0]`

---

This solution works efficiently with a time complexity of **O(n)** and space complexity of **O(1)** (or **O(n)** for Solution 2 with list comprehension). It handles the problem constraints well and ensures that the operations are applied sequentially as required.
``` 

### Summary of Time and Space Complexities:

1. **Solution 1 (In-place modification with swap)**:
   - **Time Complexity**: O(n)
   - **Space Complexity**: O(1)
   
2. **Solution 2 (Using list comprehension for zero shifting)**:
   - **Time Complexity**: O(n)
   - **Space Complexity**: O(n)

3. **Solution 3 (Java solution with in-place operations)**:
   - **

Time Complexity**: O(n)
   - **Space Complexity**: O(1)
