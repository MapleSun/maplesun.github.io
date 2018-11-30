---
title: 217. Contains Duplicate
date: 2018-06-04 22:38:49
tags: [Array, HashSet]
categories: [LeetCode, Array]
---


## Question
Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

## Analysis
简单的用HashSet 去重复，add method O(1), contains method O(1).

## Complexity
Time: O(n)

## Solution
``` Java
public boolean containsDuplicate(int[] nums) {
    HashSet<Integer> set = new HashSet<>();
    for (int n : nums) {
        if (set.contains(n)) {
            return true;
        } else {
            set.add(n);
        }
    }
    return false;
}
```