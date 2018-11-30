---
title: 56. Merge Intervals
date: 2018-06-07 12:37:16
tags: [Array]
categories: [LeetCode, Array]
---

## Question
Given a collection of intervals, merge all overlapping intervals.

## Analysis
1. 需要按Interval得start排序，以确保不会出现 `[4,5],[1,2] -> [1,5]` 的情况
2. 遍历intervals的数组 用一个temp记录interval，当出现overlap时，进行merge，
`if (newInterval.start <= temp.end) {
                temp.start = Math.min(temp.start, newInterval.start);
                temp.end = Math.max(temp.end, newInterval.end);
            }`
3. 没有overlap时，将temp添加到result的list里，并且将新的interval赋值给temp
4. 将最后一个Interval字段加入结果

## Complexity
Time: O(nlogn) since Collections.sort

## Solution
``` Java
public List<Interval> merge(List<Interval> intervals) {
    if (intervals.size() <= 1) return intervals;
    List<Interval> res = new ArrayList<>();
    intervals.sort(Comparator.comparingInt(o -> o.start));
    Interval temp = intervals.get(0);
    for (int i = 1; i < intervals.size(); i++) {
        Interval newInterval = intervals.get(i);
        if (newInterval.start <= temp.end) {
            temp.start = Math.min(temp.start, newInterval.start);
            temp.end = Math.max(temp.end, newInterval.end);
        } else {
            res.add(temp);
            temp = newInterval;
        }
    }   
    res.add(temp);
    return res;
}
```