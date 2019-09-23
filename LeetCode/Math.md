<span id = "00"></span>
## 基础		
 - [7	Reverse Integer]
 - [165	Compare Version Numbers]
 - [66. Plus One](#66-plus-one)
 - [8	String to Integer (atoi)]
 - [258	Add Digits]
 - [67	Add Binary]
 - [43	Multiply Strings]
 - [29	Divide Two Integers]
 - [69	Sqrt(x)]
 - [50	Pow(x, n)]
 - [367	Valid Perfect Square]
 - [365	Water and Jug Problem]
 - [204	Count Primes]
## Sum		
 - [1	Two Sum]
 - [167. Two Sum II](#167-two-sum-ii)
 - [15	3Sum]
 - [16	3Sum Closest]
 - [259	3Sum Smaller]
 - [18	4Sum]
 - [611. Valid Triangle Number](#611-valid-triangle-number)
## 很少考		
 - [231	Power of Two]
 - [326	Power of Three]
 - [342	Power of Four]
 - [372	Super Pow]
 - [233	Number of Digit One]
 - [319	Bulb Switcher]
 - [292	Nim Game]
 - [202	Happy Number]
 - [400	Nth Digit]
 - [263	Ugly Number]
 - [264	Ugly Number II]
 - [306	Additive Number]
 - [172	Factorial Trailing Zeroes]
 - [343	Integer Break]
 - [396	Rotate Function]
 - [390	Elimination Game]
 - [386	Lexicographical Numbers]
 - [357	Count Numbers with Unique Digits]
 - [360	Sort Transformed Array]
 - [397	Integer Replacement]
 - [368	Largest Divisible Subset]

## 66. Plus One

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

给定表示非负整数的非空数字数组，加上整数的1。

存储数字使得最高有效数字位于列表的开头，并且数组中的每个元素包含单个数字。

您可以假设整数不包含任何前导零，除了数字0本身。

**Example:1**

```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example:2**

```
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

---

### Python Solution
**分析：** 从后往前找到第一位不为 9 的数字加一返回数组即可，如果为 9 ，将这一位置 0 ，继续向前寻找。如果都为 9 ，则在数组头部插入 1 。

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        for i in range(len(digits)):
            if digits[~i] < 9:
                digits[~i] += 1
                return digits
            digits[~i] = 0
        digits.insert(0, 1)
        return digits
```

[返回目录](#00)

## 167. Two Sum II

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

给定已按升序排序的整数数组，找到两个数字，使它们相加到特定的目标数。
函数twoSum应返回两个数字的索引，以便它们加起来到目标，其中index1必须小于index2。

**Example**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

---

### Python Solution
**分析：**

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        i, j = 0,len(numbers) - 1
        while i < j:
            if numbers[i] + numbers[j] < target:
                i += 1
            elif numbers[i] + numbers[j] > target:
                j -= 1
            else:
                return i + 1, j + 1
```

[返回目录](#00)

## 611. Valid Triangle Number

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

给定一个由非负整数组成的数组，你的任务是计算从可以组成三角形的数组中选择的三元组的数量，如果我们将它们作为三角形的边长。

**Example**

```
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are:
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```

---

### Python Solution
**分析：** 这道题是中等难度的题，但其实是 Two Sum 类型题的变形。非常漂亮的解法，如果暴力法的话需要 O(n^3) 的时间复杂度，但是如果巧妙运用双指针，可以缩减为 O(n^2) 。我们按照从短到长将边设为 a, b, c 三边，排序后从最后取 c 的值，如果边 a 和边 b 的长度超过边 c 的长度，那么直接加上可能的个数 (b - a)，否则移动 a 使得相加之和变大。

```python
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()
        res = 0
        for c in range(len(nums) - 1, 1, -1):
            a, b = 0, c - 1
            while a < b:
                if nums[a] + nums[b] > nums[c]:
                    res += b - a
                    b -= 1
                else:
                    a += 1
        return res
```

[返回目录](#00)