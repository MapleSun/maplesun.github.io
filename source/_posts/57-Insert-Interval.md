---
title: 57. Insert Interval
date: 2018-06-07 12:16:26
tags: [Array]
categories: [LeetCode, Array]
---
## Question
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

## Analysis
先要找到目标interval，然后判断如何制作一个新的 newInterval
1. use a while loop to find the right interval 

- `while (i < intervals.size() && intervals.get(i).end < newInterval.start) `
2. 然后看现有的interval，改变现有的newInterval
- `while (i < intervals.size() && intervals.get(i).start <= newInterval.end)`
拿到两者间最小的start和最大的end确保interval最大 
- `newInterval = new Interval(
                Math.min(newInterval.start, intervals.get(i).start),
                Math.max(newInterval.end, intervals.get(i).end));`
3. 将newInterval加入result
4. 将剩下的interval加入result

## Complexity
Time：O(n)

## Solution
```Java
 public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
    List<Interval> result = new ArrayList<>();
    
    int i = 0;
    
    while (i < intervals.size() && intervals.get(i).end < newInterval.start) {
        result.add(intervals.get(i++));
    }
    
    while (i < intervals.size() && intervals.get(i).start <= newInterval.end) {
        newInterval = new Interval(
            Math.min(newInterval.start, intervals.get(i).start),
            Math.max(newInterval.end, intervals.get(i).end));
        i++;
    }
    
    result.add(newInterval);
    
    while (i <intervals.size()) result.add(intervals.get(i++));
    return result;
}    

```