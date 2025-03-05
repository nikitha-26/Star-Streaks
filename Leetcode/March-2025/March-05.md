# *2579. Count Total Number of Colored Cells*

The problem can be found at the following link: [Question Link](https://leetcode.com/problems/count-total-number-of-colored-cells/)

## **Problem Description**

There exists an infinitely large two-dimensional grid of uncolored unit cells. You are given a positive integer `n`, indicating that you must do the following routine for `n` minutes:

- At the first minute, color any arbitrary unit cell blue.
- Every minute thereafter, color blue every uncolored cell that touches a blue cell.

Return the number of colored cells at the end of `n` minutes.

![image](https://github.com/user-attachments/assets/71c3a5f9-abf5-4daa-a052-b12cf3b5470d)



### Example 1:

#### Input:
```python
n = 1
```

#### Output:
```python
1
```

#### Explanation:
After 1 minute, there is only 1 blue cell, so we return 1.

### Example 2:

#### Input:
```python
n = 2
```

#### Output:
```python
5
```

#### Explanation:
After 2 minutes, there are 4 colored cells on the boundary and 1 in the center, so we return 5.

---

## **Approach**

The problem follows a pattern where, starting from a single colored cell, new cells are added around it in a symmetric manner each minute. Observing the pattern, the number of colored cells at each step follows this formula:

- At `n = 1`: `1`
- At `n = 2`: `1 + 4 = 5`
- At `n = 3`: `5 + 8 = 13`
- At `n = 4`: `13 + 12 = 25`
- ...

We can derive the formula:

\[ f(n) = f(n-1) + 4 \times (n-1) \]

This results in two possible approaches: **Recursion** and **Mathematical Formula**.

### **Algorithm Steps**

#### **Solution 1: Recursive Approach**
1. Define a function `f(n)` where:
   - If `n == 1`, return `1` (base case).
   - Otherwise, return `4 * (n-1) + f(n-1)`.
2. Call `f(n)` to get the result.

#### **Solution 2: Mathematical Formula**
1. Observe the pattern: `f(n) = 1 + 2 * n * (n-1)`.
2. Return the calculated result directly.

---

## **Code (Python)**

### **Solution 1: Recursive Approach**
```python
class Solution:
    def coloredCells(self, n: int) -> int:
        def f(n):
            if n == 1:
                return 1
            return 4 * (n - 1) + f(n - 1)
        return f(n)
```

#### **Time Complexity**:
- **O(n)**: Recursion goes from `n` down to `1`, leading to `O(n)` recursive calls.

#### **Space Complexity**:
- **O(n)**: Due to recursive function call stack.

---

### **Solution 2: Mathematical Formula (Optimized Solution)**
```python
class Solution:
    def coloredCells(self, n: int) -> int:
        return 1 + 2 * n * (n - 1)
```

#### **Time Complexity**:
- **O(1)**: Uses a direct formula to compute the result in constant time.

#### **Space Complexity**:
- **O(1)**: No extra space is used apart from a few variables.

---

## **Explanation of the Mathematical Formula**

Observing the pattern, the total number of colored cells after `n` minutes follows this formula:

\[ f(n) = 1 + 2 \times n \times (n-1) \]

Where:
- `1` accounts for the initial cell at `n = 1`.
- `2 * n * (n-1)` accounts for the additional cells added in each step.

Using this formula, we can compute the answer in **constant time** without recursion.

---

### **Example Walkthrough**

#### Example 1:
##### Input:
```python
n = 1
```
##### Output:
```python
1
```
##### Explanation:
Only the starting cell is colored.

#### Example 2:
##### Input:
```python
n = 2
```
##### Output:
```python
5
```
##### Explanation:
- Minute 1: `[1]` (one colored cell)
- Minute 2: `[5]` (one center + four surrounding cells)

Using the formula:
\[ 1 + 2 \times 2 \times (2 - 1) = 5 \]

#### Example 3:
##### Input:
```python
n = 3
```
##### Output:
```python
13
```
##### Explanation:
- Minute 1: `[1]`
- Minute 2: `[5]`
- Minute 3: `[13]`

Using the formula:
\[ 1 + 2 \times 3 \times (3 - 1) = 13 \]

---

## **Summary of Time and Space Complexities**

| Approach | Time Complexity | Space Complexity |
|----------|----------------|------------------|
| **Recursive Approach** | O(n) | O(n) |
| **Mathematical Formula** | O(1) | O(1) |

### **Final Thoughts**
- The recursive approach is easy to understand but inefficient for large `n`.
- The formula-based approach is optimal and should be preferred for performance reasons.
- **Use the mathematical approach for competitive programming and interviews.** 🚀

