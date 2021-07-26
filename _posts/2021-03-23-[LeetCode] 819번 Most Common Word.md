---
title: "[LeetCode] Most Common Word"
categories: 
- LeetCode
tags:
- 문자열
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given a string `paragraph` and a string array of the banned words `banned`, return *the most frequent word that is not banned*. It is **guaranteed** there is **at least one word** that is not banned, and that the answer is **unique**.

The words in `paragraph` are **case-insensitive** and the answer should be returned in **lowercase**.

## 예제

**Example 1:**

```
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```

**Example 2:**

```
Input: paragraph = "a.", banned = []
Output: "a"
```

## 조건

> - `1 <= paragraph.length <= 1000`
> - paragraph consists of English letters, space `' '`, or one of the symbols: `"!?',;."`.
> - `0 <= banned.length <= 100`
> - `1 <= banned[i].length <= 10`
> - `banned[i]` consists of only lowercase English letters.

## 답 

### 풀이 1

생각이 가는대로 풀었던 첫 풀이.

```python
from collections import Counter
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        paragraph = paragraph.lower()
        nparagraph = []

        for p in paragraph.split():
            sub = ""
            for i in p:
                if not i in ['"', '!', '?', "'", ',', ';', '.']:
                    sub += i
                elif i == ",":
                    if sub:
                        nparagraph.append(sub)
                        sub = ""
            if sub:
                nparagraph.append(sub)
        cnt = Counter(nparagraph)

        for c in cnt.most_common():
            if c[0] in banned:
                pass
            else:
                return c[0]
```

### 풀이 2

정규식을 활용해서 좀 더 간결하게 쓸 수 있는 풀이.

```python
from collections import Counter
import re
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        words = [word for word in re.sub(r'[^\w]', ' ', paragraph).lower().split() if word not in banned]
        
        cnt = Counter(words).most_common()
        
        return cnt[0][0]
```

