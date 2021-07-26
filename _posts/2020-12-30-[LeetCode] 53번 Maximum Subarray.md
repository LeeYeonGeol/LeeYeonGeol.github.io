---
title: "[LeetCode] 53번 Maximum Subarray"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

## 예제

**Example 1:**

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Example 2:**

```
Input: nums = [1]
Output: 1
```

**Example 3:**

```
Input: nums = [0]
Output: 0
```

**Example 4:**

```
Input: nums = [-1]
Output: -1
```

**Example 5:**

```
Input: nums = [-2147483647]
Output: -2147483647
```

## 조건

> **Constraints:**
>
> - `1 <= nums.length <= 2 * 104`
> - `-231 <= nums[i] <= 231 - 1`

## 풀이과정

### Kadane's Algorithm

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            if nums[i-1] > 0:
                nums[i] += nums[i-1]
        return max(nums)
```

Brute Force를 사용하면 O(N^2)의 시간복잡도를 가지지만 위 방법을 사용하면 O(N)으로도 풀 수 있다. 

이전 인덱스가 가질 수 있는 최대 부분합에 현재의 인덱스 값을 더한다면 현재 인덱스가 가질 수 있는 최대 부분합을 구할 수 있다. 그를 위해서는 이전 인덱스의 합이 0보다 크다면 더하고 그렇지 않다면 더하지 않는(초기화) 방법으로 진행한다.

## 참고자료

[Kadane's Algorithm (카데인 알고리즘)](https://medium.com/@vdongbin/kadanes-algorithm-카데인-알고리즘-acbc8c279f29)