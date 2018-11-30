---
title: 219. Contians Duplicate II
date: 2018-06-04 22:43:29
tags: [Array, HashSet]
categories: [LeetCode, Array]
---
## Question
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

## Analysis
同样使用HashSet去重复，这次多了一个条件只有在k个以内的值才算重复，所以当i>k是nums[i-k-1]需要在Set里被移除，不再作为重复。

## Complexity
Time: O(n)

## Solution
```Java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    HashSet<Integer> set = new HashSet<>();
    for (int i = 0; i < nums.length; i++) {
        if (i>k) set.remove(nums[i-k-1]);
        if (!set.add(nums[i])) return true;
    }
    return false;
}
```