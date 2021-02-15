---
title: "[LeetCode] 387번 First Unique Character in a String"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string, find the first non-repeating character in it and return its index. If it doesn't exist, return -1.

## 예제

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode"
return 2.
```

 ## 조건

> **Note:** You may assume the string contains only lowercase English letters.

## 풀이과정

### 내 풀이

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        ans = -1
        dict_dup = {}
        dict_index = {}
        for i in range(len(s)):
            if (s[i] in dict_dup) == True:
                dict_dup[str(s[i])] += 1
            else:
                dict_dup[str(s[i])] = 0
            dict_index[str(s[i])] = i
        
        for i in range(len(dict_dup)):
            if list(dict_dup.values())[i] == 0:
                return list(dict_index.values())[i]
        return ans
```

오늘 dict을 활용하는 것을 [13번 Roman to Integer](https://leeyeongeol.github.io/leetcode/python/LeetCode-13%EB%B2%88-Roman-to-Integer/)에서 공부하였다. 따라서 dict을 활용하여 문제를 풀어보았다. 중복을 세는 dict_dup와 index를 업데이트해주는 dict_index를 만든 뒤, 값을 저장한다. 그리고 값에 따라 결과를 리턴해준다.

또한 dict은 순서대로 저장되기 때문에 위의 방법이 가능했다. 다만, runtime에서 296ms로 그다지 좋게 나오진 않았다.

### 다른 풀이

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        """
        :type s: str
        :rtype: int
        """
        # build hash map : character and how often it appears
        count = collections.Counter(s)
        
        # find the index
        for idx, ch in enumerate(s):
            if count[ch] == 1:
                return idx     
        return -1
```

데이터 갯수를 셀 때 유용한 collections.Counter를 활용해서 나타나는 횟수를 구한다. 그 후, s 순서대로 for 문을 돌리면서 중복되지 않다면 인덱스를 반환한다.