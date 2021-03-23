---
title: "[LeetCode] Group Anagrams"
categories: 
- LeetCode
tags:
- 문자열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## 예제

**Example 1:**

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**Example 2:**

```
Input: strs = [""]
Output: [[""]]
```

**Example 3:**

```
Input: strs = ["a"]
Output: [["a"]]
```

## 조건

> - 1 <= strs.length <= $10^4$
> - 0 <= strs[i].length <= 100
> - `strs[i]` consists of lower-case English letters.

## 답 

### 풀이 1

정렬했을 때 같은 값을 갖게 되도록 해야한다. 따라서 정렬 후, join을 사용해서 나온 값을 key로 하고 해당 word를 value로 한다.

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = collections.defaultdict(list)
        
        for word in strs:
            anagrams[''.join(sorted(word))].append(word)
            
        answer = []
        return list(anagrams.values())
```



