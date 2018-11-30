---
title: 118. Pascal's Triangle
date: 2018-06-04 13:06:17
tags: [Array]
categories: [LeetCode, Array]
---

## Question
Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

## Analysis
除了0 和 i位固定为1， 

其他位置
- triangle[i][j] = triangle[i-1][j-1] + triangle[i-1][j-1]

## Complexity
Time: O(n)

## Solution
``` Java
public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> triangle = new ArrayList<>();
    if (numRows <= 0){
        return triangle;
    }
    for (int i = 0; i < numRows; i++) {
        List<Integer> row = new ArrayList<>();
        for (int j = 0; j < i + 1; j++) {
            if (j == 0 || j == i) {
                row.add(1);
            } else {
                row.add(triangle.get(i-1).get(j-1) + triangle.get(i-1).get(j));
            }
        } 
        triangle.add(row);  
    }
    return triangle;
}

```