---
title: 45 Jump Game II
date: 2018-06-05 22:05:45
tags:
---
## Question
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

**Note:**

You can assume that you can always reach the last index.


## Analysis
这一步能跳的范围是 i ~ i + nums[i], curFarthest 是之前所有点Max(i+nums[i]), 每次到达 i+nums[i] 发起另一个jump, curFarthest = i + nums[i]

## Complexity
Time: O(n)

## Solution
```Java
public class Solution {
    public int jump(int[] nums) {
        int curtStep = 0;
        int curtStepMaxReach = 0;
        int nextStepMaxReach = 0;
        for(int i = 0; i < nums.length - 1; i ++){
            nextStepMaxReach = Math.max(nextStepMaxReach, i + nums[i]);
            if(i == curtStepMaxReach){
                curtStep ++;
                curtStepMaxReach = nextStepMaxReach;
            }
        }
        return curtStep;
    }
}

```