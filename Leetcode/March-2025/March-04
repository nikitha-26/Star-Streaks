# *1780. Check if Number is a Sum of Powers of Three*

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/longest-increasing-subsequence-1587115620/1)  

## **Problem Description**

Given an integer `n`, return `true` if it is possible to represent `n` as the sum of distinct powers of three. Otherwise, return `false`.

An integer `y` is a power of three if there exists an integer `x` such that `y == 3^x`.

### **Example 1:**

#### **Input:**
```python
n = 12
```

#### Output:
```python
true
```

#### Explanation:
`12 = 3^1 + 3^2`.

### Example 2:

#### Input:
```python
n = 91
```

#### Output:
```python
true
```

#### Explanation:
`91 = 3^0 + 3^2 + 3^4`.

### Example 3:

#### Input:
```python
n = 21
```

#### Output:
```python
false
```

---

### Constraints:
- \(1 \leq n \leq 10^7\)

---

## Approach

The key observation is that we can check if a number `n` can be represented as the sum of distinct powers of 3 by repeatedly dividing it by 3. If at any point, the remainder when dividing by 3 is 2, then it's impossible to represent the number as a sum of distinct powers of three, so we return `False`. If we successfully divide `n` by 3 and never get a remainder of 2, we return `True`.

### Algorithm Steps:
1. Iterate while `n > 0`:
   - If `n % 3 == 2`, return `False`.
   - Otherwise, divide `n` by 3.
2. Return `True` when the loop ends.

### Time Complexity:
- **O(log₃ n)**: The number is divided by 3 in each iteration, and the number of divisions is proportional to the logarithm of the number to base 3.

### Space Complexity:
- **O(1)**: No additional space is used.

---

## Code (Python)

```python
class Solution:
    def checkPowersOfThree(self, n: int) -> bool:
        while n > 0:
            if n % 3 == 2:
                return False
            n = n // 3
        return True
```

---

## Explanation

In this approach, we repeatedly divide `n` by 3. If the remainder is `2` at any point, it means `n` cannot be expressed as the sum of distinct powers of 3 because the only valid remainders when dividing by 3 are 0 and 1. If we finish dividing `n` and don't encounter a remainder of 2, it means `n` can indeed be expressed as such a sum.

---

## Example Walkthrough:

### Example 1:
#### Input: `n = 12`

- `12 % 3 = 0` (Valid, continue)
- `12 // 3 = 4`
- `4 % 3 = 1` (Valid, continue)
- `4 // 3 = 1`
- `1 % 3 = 1` (Valid, continue)
- `1 // 3 = 0`
- We reach `n = 0`, return `True`.

#### Output: `True`

### Example 2:
#### Input: `n = 91`

- `91 % 3 = 1` (Valid, continue)
- `91 // 3 = 30`
- `30 % 3 = 0` (Valid, continue)
- `30 // 3 = 10`
- `10 % 3 = 1` (Valid, continue)
- `10 // 3 = 3`
- `3 % 3 = 0` (Valid, continue)
- `3 // 3 = 1`
- `1 % 3 = 1` (Valid, continue)
- `1 // 3 = 0`
- We reach `n = 0`, return `True`.

#### Output: `True`

### Example 3:
#### Input: `n = 21`

- `21 % 3 = 0` (Valid, continue)
- `21 // 3 = 7`
- `7 % 3 = 1` (Valid, continue)
- `7 // 3 = 2`
- `2 % 3 = 2` (Invalid, return `False`).

#### Output: `False`

---

## Visitor Count

<p align="center">
  <img src="https://profile-counter.glitch.me/YOUR_GITHUB_USERNAME/count.svg" />
</p>

---

**⭐ If you find this repository helpful, please give it a star! ⭐**
```
