---
title: 80. Remove Duplicates from Sorted Array II
date: 2018-06-02 12:27:39
tags: [Array, Two Pointers]
categories: [LeetCode, Array]
---

## Question
Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

## Analysis
This question is the follow-up of [Remove-Duplicates-from Sorted Array](../26-Remove-Duplicates-from-Sorted-Array/index.html).

### Two situation
1. nums[fast] == nums[fast - 1]
    1. cnt < 2: 
        - nums[cur++] = nums[f] (legal state)
        - cnt++
    2. cnt >= 2: 
        - cur doesn't move
        - cnt++
2. nums[fast] == nums[fast - 1]
    - nums[cur++] = nums[f]
    - cnt reset, cnt = 1

**本来在legal state这个部分没有想明白这里为什么需要交换, 本来认为legal state，cnt没有到2 所以只要cur++就可以了。 但在下面的情况**
```
test case[0,0,1,1,1,1,2,3,3] 过不了。
WA: [0,0,1,1,2,3,2]
[0,0,1,1,2,1,2,3,3] cnt = 1
         c     f
[0,0,1,1,2,3,2,3,3] cnt = 1 此时cnt还没有增加，如果只是cur++则出现WA，
           c     f         

```
因为即使相同，第二个3没有在正确的位置上，换句话说就是**只要是legal的就要换到正确的位置上因为fast的位置是不确定的, 正确的位置总是cur+1**

## Complexity
Time Complexity: O(n)

## Solution
``` Java
public int removeDuplicates(int[] nums) {
    if (nums.length < 2) return nums.length;
    int cur = 1;
    int cnt = 1;
    for (int f = 1; f < nums.length; f++) {
        if (nums[f] == nums[f - 1]) {
            if (cnt < 2) {
                nums[cur++] = nums[f];
            }
            cnt++;
        } else {
            nums[cur++] = nums[f];
            cnt = 1;
        }
    }
    return cur;
}
```