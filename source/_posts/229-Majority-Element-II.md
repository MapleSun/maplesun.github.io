---
title: 229. Majority Element II
date: 2018-06-04 16:28:57
tags: [Array, HashMap, Boyer-Moore majority vote Algorithm]
categories: [LeetCode, Array]
---

## Question
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

Note: The algorithm should run in linear time and in O(1) space.

## Analysis

Method 1 HashMap:

use HashMap to record how many time each element appear

Method 2 Boyer-Moore majority vote Algorithm:






## Solution

``` Java
// Method 1 HashMap
public List<Integer> majorityElement(int[] nums) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int n : nums) {
        if (!map.containsKey(n)) {
            map.put(n, 1);
        } else {
            map.put(n, map.get(n) + 1);
        }
        
    }
    List<Integer> res = new ArrayList<>();
    for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
        if (entry.getValue() > nums.length / 3) {
            res. add(entry.getKey());
        }
    }

    return res;
}


// Method 2 Boyer-Moore majority vote Algorithm
public List<Integer> majorityElement(int[] nums) {  
    int num1 = 0, num2 = 1;  
    int count1 = 0, count2 = 0;  
    for(int num: nums) {  
        if (count1 == 0) {  
            num1 = num;  
            count1 = 1;  
        } else if (num1 == num) {  
            count1 ++;  
        } else if (count2 == 0) {  
            num2 = num;  
            count2 = 1;  
        } else if (num2 == num) {  
            count2 ++;  
        } else {  
            count1 --;  
            count2 --;  
            if (count1 == 0 && count2 > 0) {  
                num1 = num2;  
                count1 = count2;  
                num2 = 0;  
                count2 = 0;  
            }  
        }  
    }  
    if (count1 > 0) {  
        count1 = 0;  
        for(int num: nums) if (num1 == num) count1 ++;  
    }  
    if (count2 > 0) {  
        count2 = 0;  
        for(int num: nums) if (num2 == num) count2 ++;  
    }  
    List<Integer> results = new ArrayList<>();  
    if (count1*3>nums.length) results.add(num1);  
    if (count2*3>nums.length) results.add(num2);  
    return results;  
} 
```



