---
title: 134. Gas Station
date: 2018-06-04 02:34:14
tags: [Array, Greedy]
categories: [LeetCode, Array]
---

## Question
There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

Note:

If there exists a solution, it is guaranteed to be unique.
Both input arrays are non-empty and have the same length.
Each element in the input arrays is a non-negative integer.

## Analysis
一开始想的是dfs，因为感觉很像dfs，从第一个点开始尝试看能不能走通，（**未完成**）


**Discussion**
1. 很容易想到，如果 总gas < 总cost，return -1；
2. 如果前面所有 gas-cost 加起来小于0， 那么前面的gas stattion都不能作为start postion

## Compleixty
Time：O(n)
Space: O(1)

## Solution
```Java
public int canCompleteCircuit(int[] gas, int[] cost) {
    int tank = 0;
    for(int i = 0; i < gas.length; i++)
        tank += gas[i] - cost[i];
    if(tank < 0)
        return - 1;

    int start = 0;
    int accumulate = 0;
    for (int i = 0; i < gas.length; i++) {
        accumulate += gas[i] - cost[i];
        if(accumulate < 0){
            start = i + 1;
            accumulate = 0;
        }
    }
    
    return start;
}
```
