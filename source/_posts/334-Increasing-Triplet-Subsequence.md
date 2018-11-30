---
title: 334. Increasing Triplet Subsequence
date: 2018-06-06 21:37:40
tags: [Array]
categories: [LeetCode, Array]
---
## Question
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:
> Return true if there exists i, j, k, such that arr[i] < arr[j] < arr[k] <= n-1 else return false

## Analysis
需要找到最小的和中间的，满足最小的 永远 小于中间的，
1. 当 `nums[i] < small` 其实我们并不关心，我们只关心此时是否有比中间值更大的数
2. 当 `small < nums[i] < mid` 此时更新中间值mid，原来 `small mid` -> `small mid nums[i]`  -> `small old_mid mid`
3. 当 `small < mid < nums[i]`  此时找到triplet sequence

## Compleixty
Time: O(n)
Space: O(1)

## Solution
``` Java
public boolean increasingTriplet(int[] nums) {
    int small = Integer.MAX_VALUE, big = Integer.MAX_VALUE;
    for (int n : nums) {
        if (n <= small) {
            small = n;
        } else if (n <= big) {
            big = n;
        } else {
            return true;
        }
    }
    return false;    
}
```