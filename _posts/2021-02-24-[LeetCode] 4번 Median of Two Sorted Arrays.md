---
title: "[LeetCode] 4번 Median of Two Sorted Arrays"
categories: 
- LeetCode
tags:
- Sort
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

**Follow up:** The overall run time complexity should be `O(log (m+n))`.

## 예제

**Example 1:**

```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

**Example 2:**

```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

**Example 3:**

```
Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000
```

**Example 4:**

```
Input: nums1 = [], nums2 = [1]
Output: 1.00000
```

**Example 5:**

```
Input: nums1 = [2], nums2 = []
Output: 2.00000
```

## 조건

> **Constraints:**
>
> - `nums1.length == m`
> - `nums2.length == n`
> - `0 <= m <= 1000`
> - `0 <= n <= 1000`
> - `1 <= m + n <= 2000`
> - `-106 <= nums1[i], nums2[i] <= 106`
>
> .

## 답

### 내 풀이

문제에서 시간 복잡도는 $O(log(m+n))$이라고 하였다. 이를 만족하는 [정렬 알고리즘](https://leeyeongeol.github.io/algorithm/Algorithm-%EC%A0%95%EB%A0%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98/)은 무엇이 있을까? 그렇다. 계수 정렬이다. 계수 정렬의 아이디어를 통해 해결한다. 원래는 양수에 대해서만 가능하지만 이 문제의 경우 음수도 고려해야 되기 때문에 양수와 음수 따로 리스트를 만들어서 음수는 부호변환을 통해 계산한다.

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        # nums1과 nums2 합치기
        arr = nums1 + nums2
 		
        # 양수와 음수를 계산하는 리스트
        dp_plus = [0] * (max(arr)+1)
        dp_minus = [0] * (abs(min(arr))+1)
        
        # 총 개수
        max_num = len(arr)
        
        # 양수와 음수 따로 저장
        for i in range(max_num):
            if arr[i] >= 0:
                dp_plus[arr[i]] += 1
            else:
                dp_minus[abs(arr[i])] += 1
        
        # 처음부터 개수를 확인해가면서 정렬된 리스트 생성 (음수는 역순)
        sol = []   
        for i in range(len(dp_minus)-1, 0, -1):
            for j in range(dp_minus[i]):
                sol.append(-i)
        for i in range(len(dp_plus)):
            for j in range(dp_plus[i]):
                sol.append(i)
        
        # 답 출력
        if max_num % 2 == 0:
            return float((sol[max_num//2]+sol[(max_num//2) - 1])/2)
        else:
            return float(sol[max_num//2])
```

![image](https://user-images.githubusercontent.com/48538655/108924585-3f023c00-767e-11eb-817c-fe919990a3cf.png)
