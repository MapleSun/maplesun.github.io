---
title: 220. Contains Duplicate III
date: 2018-06-05 11:31:49
tags: [Array]
categories: [LeetCode, Array]
---

## Question
Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k.

## Analysis
和前两题有很大的区别，前两题的本质问题是在去重复。这题的改变了重复的性质，[-t, +t] 范围内的数都被认为是重复。

1. Brute Force: 暴力解法是可以解决问题的，但是会超时，Time Complexity: O(tn)

2. Using TreeSet: TreeSet 
> A NavigableSet implementation based on a TreeMap. The elements are ordered using their natural ordering, or by a Comparator provided at set creation time, depending on which constructor is used.
This implementation provides guaranteed log(n) time cost for the basic operations (add, remove and contains).

This implementation provides guaranteed log(n) time cost for the basic operations (add, remove and contains).

可以看到TreeSet是基于TreeMap实现的，线程不安全， TreeSet存储元素实际为TreeMap存储的键值对为<key,PRESENT>的key。因为是基于TreeMap实现的，本质是红黑树 Red-Black Tree，基本操作都是 log(n)

- Method：
    - ceiling(E e): Returns the least element in this set greater than or equal to the given element, or null if there is no such element.
    - floor(E e): Returns the greatest element in this set less than or equal to the given element, or null if there is no such element.


- 遍历方式
``` Java
// 顺序TreeSet：迭代器实现
Iterator iter = set.iterator();
while (iter.hasNext()) {
    System.out.println(iter.next());
    
}

// 顺序遍历TreeSet：foreach实现
for (Integer i : set) {
    System.out.println(i);
}

// 逆序遍历TreeSet：反向迭代器实现
Iterator iter1 = set.descendingIterator();
while (iter1.hasNext()) {
    System.out.println(iter1.next());
}
```

3. Bucket Sort
Bucketing means we map a range of values to the a bucket. 一个bucket对应的是0～t的范围。同时也要检查前后的bucket

## Solution
``` Java
// TLE Brute Force
public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    HashSet<Integer> set = new HashSet<>();
    for (int i = 0; i < nums.length; i++) {
        if (i > k) set.remove(nums[i-k-1]);
        for (int j = 0; j <= t; j++) {
            if (set.contains(nums[i]+j) || set.contains(nums[i]-j)) {
                return true;
            } else {
                set.add(nums[i]);
            }
        }
    }
    return false;
}


// TreeSet
public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    if (nums == null || k < 1 || t < 0) {
        return false;
    }
    TreeSet<Long> set = new TreeSet<>();
    
    for (int i = 0; i < nums.length; i++) {
        Long floor = set.floor((long)nums[i] + t);
        Long ceil = set.ceiling((long)nums[i] - t);
        if ((floor != null && floor >= nums[i]) 
            || (ceil != null && ceil <= nums[i])) {
            return true;
        }
        
        set.add((long)nums[i]);
        if (i >= k) {
            set.remove((long)nums[i - k]);
        }
    }
    
    return false;
}


// Bucket
public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    if (k < 1 || t < 0) return false;
    Map<Long, Long> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        long remappedNum = (long) nums[i] - Integer.MIN_VALUE;
        long bucket = remappedNum / ((long) t + 1);
        if (map.containsKey(bucket)
                || (map.containsKey(bucket - 1) && remappedNum - map.get(bucket - 1) <= t)
                    || (map.containsKey(bucket + 1) && map.get(bucket + 1) - remappedNum <= t))
                        return true;
        if (map.entrySet().size() >= k) {
            long lastBucket = ((long) nums[i - k] - Integer.MIN_VALUE) / ((long) t + 1);
            map.remove(lastBucket);
        }
        map.put(bucket, remappedNum);
    }
    return false;
}
```