---
title: 42. Trapping Rain Water
date: 2018-06-06 20:56:30
tags: [Array]
categories: [LeetCode, Array]
---

## Question
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

Ex: [0,1,0,2,1,0,1,3,2,1,2,1]

1[example](http://www.leetcode.com/static/images/problemset/rainwatertrap.png)

## Analysis
首先，碰到这样的题目不要慌张，挨个分析每个A[i]能trapped water的容量，然后将所有的A[i]的trapped water容量相加即可

其次，对于每个A[i]能trapped water的容量，取决于A[i]左右两边的高度（可延展）较小值与A[i]的差值，即volume[i] = [min(left[i], right[i]) - A[i]] * 1，这里的1是宽度，如果the width of each bar is 2,那就要乘以2了

## Complexity
Time: O(n)
Space: O(n)

## Solution
``` Java
public int trap(int[] height) {
    if (height == null || height.length == 0) return 0;
    int[] left = new int[height.length];
    int[] right = new int[height.length];
    // int[] water = new int[height.length];
    int max, total = 0;
    max = height[0];
    left[0] = height[0];
    for (int i = 1; i < height.length; i++) {
        left[i] = Math.max(max, height[i]);
        max = Math.max(max, left[i]);
    }
    
    max = height[height.length - 1];
    right[height.length - 1] = height[height.length - 1];
    for (int i = height.length - 2; i >= 0; i--) {
        right[i] = Math.max(max, height[i]);
        max = Math.max(max, right[i]);
    }
    
    for (int i = 1; i < height.length-1; i++) {  
            int bit = Math.min(left[i], right[i]) - height[i];  
            if (bit > 0)  total += bit;  
        }  
    
    return total;
}
```