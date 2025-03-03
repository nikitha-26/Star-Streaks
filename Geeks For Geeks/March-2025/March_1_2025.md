# **📌 Daily Coding Problem of the Day**

Welcome to the **Daily Coding POTD** repository! 🚀 This repo contains my solutions to daily coding problems from **GeeksforGeeks (GFG)** and **LeetCode**.

## 📂 Folder Structure

```
📦 Daily-Coding-POTD
 ┣ 📂 LeetCode
 ┃ ┣ 📂 YYYY-MM  (Year-Month)
 ┃ ┃ ┣ 📜 YYYY-MM-DD_ProblemName.py
 ┣ 📂 GFG
 ┃ ┣ 📂 YYYY-MM
 ┃ ┃ ┣ 📜 YYYY-MM-DD_ProblemName.py
 ┗ 📜 README.md
```

Each problem is named in the format:  
📌 `YYYY-MM-DD_ProblemName.py`

---

# 🔥 **Today's Problem - 1 March 2025**

## 📝 Problem: **[Decode The String](https://www.geeksforgeeks.org/problems/decode-the-string2444/1)**  

### **Problem Description**  
*Brief description of the problem in 1-2 lines.*

### **Example**  
#### **Input:**  
```
Example Input
```
#### **Output:**  
```
Example Output
```

---

## 🚀 My Solution (Python)  

```python

class Solution:
    def decodedString(self, s):
        stack=[]
        for item in s:
            if item=="]":
                curr=""
                while stack and stack[-1]!="[":
                    curr=stack.pop()+curr
                stack.pop()
                val=""
                while stack and stack[-1].isnumeric():
                    val=stack.pop()+val
                stack.append(curr*int(val))
            else:
                stack.append(item)
        ans=""
        while stack:
            ans=stack.pop()+ans
        return ans

```

---

## 📊 **Complexity Analysis**  
- **Time Complexity:** `O(?)`
- **Space Complexity:** `O(?)`

---

## 🏆 **Progress Log**

| Date       | GFG |
|------------|------------------|
| 01-03-2025 | Decode the string | 


---

## 💡 **How to Contribute?**  
If you have an optimized solution or an alternative approach, feel free to open a pull request! 🚀

---

## ⭐ **Let's Connect!**  
If you find this helpful, consider starring ⭐ this repository!  
For discussions or suggestions, feel free to reach out.  

<p align="center">
  <img src="https://profile-counter.glitch.me/your-github-username/count.svg" />
</p>

