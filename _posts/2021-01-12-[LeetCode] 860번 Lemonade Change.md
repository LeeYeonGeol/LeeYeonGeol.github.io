---
title: "[LeetCode] 860번 Lemonade Change"
categories: 
- LeetCode
toc: true   #Table Of Contents 목차 
use_math: true
toc_sticky: true
---

## 문제

At a lemonade stand, each lemonade costs `$5`. 

Customers are standing in a queue to buy from you, and order one at a time (in the order specified by `bills`).

Each customer will only buy one lemonade and pay with either a `$5`, `$10`, or `$20` bill. You must provide the correct change to each customer, so that the net transaction is that the customer pays $5.

Note that you don't have any change in hand at first.

Return `true` if and only if you can provide every customer with correct change.

## 예제

**Example 1:**

```
Input: [5,5,5,10,20]
Output: true
Explanation: 
From the first 3 customers, we collect three $5 bills in order.
From the fourth customer, we collect a $10 bill and give back a $5.
From the fifth customer, we give a $10 bill and a $5 bill.
Since all customers got correct change, we output true.
```

**Example 2:**

```
Input: [5,5,10]
Output: true
```

**Example 3:**

```
Input: [10,10]
Output: false
```

**Example 4:**

```
Input: [5,5,10,10,20]
Output: false
Explanation: 
From the first two customers in order, we collect two $5 bills.
For the next two customers in order, we collect a $10 bill and give back a $5 bill.
For the last customer, we can't give change of $15 back because we only have two $10 bills.
Since not every customer received correct change, the answer is false.
```

## 조건

> **Note:**
>
> - `0 <= bills.length <= 10000`
> - `bills[i]` will be either `5`, `10`, or `20`.

## 풀이과정

### 내 풀이

```python
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        change = dict()
        change[5] = 0
        change[10] = 0
        for i in bills:
            bill = 5*change[5] + 10*change[10]
            if i == 5:
                change[5] += 1
            elif i == 10:
                if change[5] == 0:
                    return False
                else:
                    change[5] -= 1
                    change[10] += 1
            else:
                if change[10] >= 1:
                    if change[5] >= 1:
                        change[10] -= 1
                        change[5] -= 1
                    else:
                        return False
                else:
                    if change[5] >= 3:
                        change[5] -= 3
                    else:
                        return False               
        return True
```

### 다른 풀이

```python
class Solution:
    def lemonadeChange(self, bills):
        five = ten = 0
        for num in bills:
            if num == 5:
                five += 1
            elif num == 10 and five:
                ten += 1
                five -= 1
            elif num == 20 and five and ten:
                five -= 1
                ten -= 1
            elif num == 20 and five >= 3:
                five -= 3
            else:
                return False
        return True
```
