---
title: "[LeetCode] 35번 Search Insert Position"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

## 예제

**Example 1:**

```
Input: nums = [1,3,5,6], target = 5
Output: 2
```

**Example 2:**

```
Input: nums = [1,3,5,6], target = 2
Output: 1
```

**Example 3:**

```
Input: nums = [1,3,5,6], target = 7
Output: 4
```

**Example 4:**

```
Input: nums = [1,3,5,6], target = 0
Output: 0
```

**Example 5:**

```
Input: nums = [1], target = 0
Output: 0
```

## 조건

> **Constraints:**
>
> - `1 <= nums.length <= 10^4`
> - `-10^4 <= nums[i] <= 10^4`
> - `nums` contains **distinct** values sorted in **ascending** order.
> - `-10^4 <= target <= 10^4`

## 풀이과정

### 내 풀이

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        # target이 있는 경우
        for idx, i in enumerate(nums):
            if i == target:
                return idx
        # target이 없는 경우
        nums.append(target)
        nums.sort()
        return nums.index(target)
```

target이 있는 경우와 없는 경우 나누어서 진행하였다.

### 다른 풀이

```python
class Solution:
    def searchInsert(self, N: List[int], t: int) -> int:
        for i,n in enumerate(N):
            if n >= t:
                return i
        return len(N)
```

내 풀이에서 훨씬 간단해진 풀이. 왜 이런걸 생각못했을까...

```python
class Solution:
    def searchInsert(self, N: List[int], t: int) -> int:
        return bisect.bisect_left(N,t)
```

배열 이진 분팔 알고리즘인 bisect.bisect_left를 사용. 정렬된 순서를 유지하도록 N에 t를 삽입할 위치를 찾는다.