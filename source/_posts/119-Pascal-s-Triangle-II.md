---
title: 119. Pascal's Triangle II
date: 2018-06-04 14:52:37
tags:
---
## Question

Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.

## Analysis
本来以为很简单的一道题，确卡了我半天，第一个错误时愚蠢的把prev的赋值放在了小循环里， 第二个错误是对ArrayList的set 和 add method 不够熟悉， 我的思路是用一个prev ArrayList去记录上一行的结果。
在这个过程中一定要学会ArrayList的set和addmethod的区别

- add
   - add(E e) Appends the specified element to the end of this list. 
   - add(int index, E element) Inserts the specified element at the specified position in this list.
- set
   - set(int index, E element) Replaces the element at the specified position in this list with the specified element.

**Discussion**
discussion里的大佬直接in place的去做，也是打开了新世界的大门。因为index 0 和 index i位永远是1。很明显的，计算下一行的时候需要上一行的值，如果从头修改肯定不行，下一位就缺少了[i-1][j-1]这个值。所以从尾部开始计算。**要在每次循环开始时补上最末尾的1。**

**j loop**:
> for(int j=i-1;j>0;j--) {res.set(j, res.get(j-1)+res.get(j));}

## Solution
``` Java
class Solution {
    // discussion
    public List<Integer> getRow(int rowIndex) {
        List<Integer> res = new ArrayList<Integer>();
        for(int i = 0;i<rowIndex+1;i++) {
                res.add(1);
                for(int j=i-1;j>0;j--) {
                    res.set(j, res.get(j-1)+res.get(j));
                }
        }
        return res;
    }
    // my solution
    public List<Integer> getRow(int rowIndex) {
        List<Integer> res = null;
        List<Integer> prev = new ArrayList<>();
        
        for (int i = 0; i <= rowIndex; i++) {
            res = new ArrayList<>();
            for (int j = 0; j < i + 1; j++) {
                if (j == 0 || j == i) {
                    res.add(1);
                } else {
                   res.add(prev.get(j-1) + prev.get(j));
                }
            }
            prev = res;
        }
        return res;
    }
}

```
