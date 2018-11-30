---
title: 287. Find the Duplicate Number
date: 2018-06-07 00:09:09
tags: [Array, Two Pointer]
categories: [LeetCode, Array]
---
## Question
Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

## Analysis
全无头绪啊，discuss里是说把value做为下标，用快慢指针去找，~~如果有相同的值（duplicate)找过以后会形成环circle. Duplicate 肯定是circle的入口(entry point). ~~
当slow == fast的时候让其中一个从新从0开始，他们就会在entry point在遇到。

## Complexity
Time: O(n)
Space: O(1)

## Solution
```Java
public class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0, fast = 0;
        int len = nums.length;
        while (fast < len && nums[fast] < len) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) {
                slow = 0;
                while (slow != fast) {
                    slow = nums[slow];
                    fast = nums[fast];
                }
                return slow;
            }
        }
        return -1;
    }
    public int findDuplicate(int[] nums) {
        if (nums.length > 1)
        {
            int slow = nums[0];
            int fast = nums[nums[0]];
            while (slow != fast)
            {
                slow = nums[slow];
                fast = nums[nums[fast]];
            }

            fast = 0;
            while (fast != slow)
            {
                fast = nums[fast];
                slow = nums[slow];
            }
            return slow;
        }
        return -1;
    }
}
```