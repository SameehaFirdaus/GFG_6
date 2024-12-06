# GFG_6
---
Difficulty: Medium
Source: 160 Days of Problem Solving
Tags:
  - Arrays
  - Greedy
  - Two Pointers
---
# 🚀 _Day 6. Majority Element II_ 🧠
  
The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/majority-vote)


## 💡 **Problem Description:**

You are given an array of integers `arr[]` where each number represents a vote for a candidate. Return the candidates that have votes greater than one-third of the total votes. If there's no majority vote, return an empty array.  

**Note:** The answer should be returned in an increasing order.

## 🔍 **Example Walkthrough:**

**Input:**  
`arr[] = [2, 1, 5, 5, 5, 5, 6, 6, 6, 6, 6]`  
**Output:**  
`[5, 6]`

**Explanation:**  
5 and 6 occur more than `n / 3` times in the array.

**Input:**  
`arr[] = [1, 2, 3, 4, 5]`  
**Output:**  
`[]`

**Explanation:**  
No candidate occurs more than `n / 3` times.

### Constraints:
- `1 <= arr.size() <= 10^6`
- `-10^9 <= arr[i] <= 10^9`

## 🎯 **My Approach:**

1. **Boyer-Moore Voting Algorithm**:  
   - The problem can be efficiently solved using the Boyer-Moore Voting Algorithm to find the top two candidates with the potential to exceed `n / 3` votes.  
   - First, identify the two potential majority elements.  
   - Then, verify their counts to ensure they actually exceed the threshold.  
   - This approach reduces the problem to a linear pass through the array.

2. **Steps:**  
   - Traverse the array to find two majority candidates (`num1` and `num2`) using count variables.  
   - Traverse again to count occurrences of the candidates and validate the result.  
   - Ensure the final output is sorted to meet the problem requirements.

## 🕒 **Time and Auxiliary Space Complexity**📝

- **Expected Time Complexity:** O(n), where `n` is the size of the array. The algorithm requires two linear scans of the array, making it efficient.  
- **Expected Auxiliary Space Complexity:** O(1), as we use only a constant amount of additional space.

## 📝 **Solution Code**
## Code (Python)

```python
class Solution:
    def findMajority(self, arr):
        num1, num2, c1, c2 = None, None, 0, 0
        n = len(arr)
        for x in arr:
            if x == num1:
                c1 += 1
            elif x == num2:
                c2 += 1
            elif c1 == 0:
                num1 = x
                c1 = 1
            elif c2 == 0:
                num2 = x
                c2 = 1
            else:
                c1 -= 1
                c2 -= 1
        c1, c2 = 0, 0
        for x in arr:
            if x == num1:
                c1 += 1
            elif x == num2:
                c2 += 1
        res = []
        if c1 > n // 3:
            res.append(num1)
        if c2 > n // 3:
            res.append(num2)
        res.sort()
        return res
```
