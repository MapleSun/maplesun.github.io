---
title: 189. Rotate Array
date: 2018-06-02 20:32:40
tags: [Array, Two Pointers]
categories: [LeetCode, Array]
---

## Question
Given an array, rotate the array to the right by k steps, where k is non-negative.

## Analysis
k = k mod nums.length
First, according the example hint, rotate the number at the end to the front. It works but it is too slow.


**Another way, use reverse**
input:  [1,2,3,4,5,6,7] k = 3
output: [5,6,7,1,2,3,4]

### Reverse the bold part
0. [1,2,3,4,5,6,7]
1. [**4,3,2,1**,5,6,7]
2. [4,3,2,1,**7,6,5**]
3. [**5,6,7,1,2,3,4**]


## Complexity
Time Complexity: O(n)
Space Complexity: O(1)

## Solution
``` Java
// Solution
public void rotate(int[] nums, int k) {
    if (nums.length < 2) return;
    int n = nums.length;
    k = k % n;
    reverse(nums, 0, n - k - 1);
    reverse(nums, n - k, n - 1);
    reverse(nums, 0, n - 1);
    return;
}

public void reverse(int[] nums, int start, int end) {
    while (start <= end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}


//TLE
public void rotate(int[] nums, int k) {
    if (nums.length < 2) return;
    int n = nums.length;
    k = k % n;
    while (k > 0) {
        // last index
        int temp = nums[n - 1];
        for (int i = n - 1; i > 0; i--) {
            nums[i] = nums[i-1];
        }
        nums[0] = temp;
        k--;
    }
    return;
}

```