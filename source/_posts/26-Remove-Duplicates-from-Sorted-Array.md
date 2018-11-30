---
title: 26. Remove Duplicates from Sorted Array
date: 2018-06-02 10:50:13
tags: [Array, Two Pointers]
categories: [LeetCode, Array]
---
## Question
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.


## Analysis
Use two pointer:
1. record current index postion
2. iterate array and compare element with cur postion if the value is different replace the nums[cur++] = nums[fast]

## Complexity
Time Complexity: **O(n)**

## Solution
``` Java
    public int removeDuplicates(int[] nums) {
        if (nums.length < 2) return nums.length;
        int cur = 1;
        for (int fast = 1; fast < nums.length; ++fast) {
            if (nums[fast] != nums[fast-1]){
              nums[cur++] = nums[fast];  
            } 
        }
        return cur;
    }
```