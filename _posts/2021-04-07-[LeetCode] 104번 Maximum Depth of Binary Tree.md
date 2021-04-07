---
title: "[LeetCode] Maximum Depth of Binary Tree"
categories: 
- LeetCode
tags:
- 트리
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

## 예제

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

**Example 2:**

```
Input: root = [1,null,2]
Output: 2
```

**Example 3:**

```
Input: root = []
Output: 0
```

**Example 4:**

```
Input: root = [0]
Output: 1
```

## 조건

- The number of nodes in the tree is in the range [0, $10^4$].
- `-100 <= Node.val <= 100`

## 답 

### 풀이 1

BFS를 활용한 풀이

```python
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
    	if root in None:
            return 0
        q = collections.deque([root])
        ans = 0
        
        while q:
            ans += 1
            for _ in range(len(q)):
                cur_root = q.popleft()
                if cur_root.left:
                    q.append(cur_root.left)
                if cur_root.right:
                    q.append(cur_root.right)
        return ans
```









