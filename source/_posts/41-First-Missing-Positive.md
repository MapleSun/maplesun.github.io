---
title: 41. First Missing Positive
date: 2018-06-03 11:16:14
tags: [Array, PriorityQueue]
categories: [LeetCode, Array]
---

## Question
Given an unsorted integer array, find the smallest missing positive integer.
Your algorithm should run in O(n) time and uses constant extra space.

## Analysis
一开始，没看答案写的。找第一个missing positive number，感觉正常的想法会是排序。但是题目要求是O(n) time.
Arrays.sort(nums) 是O(nlogn)，所以想到了PriorityQueue（其实也有问题，要求constant extra space）
PQ 的 insert time 是O(logn), loop 是O(n).
这个方法AC了但是不符合要求

看了discussion, 感觉所有的Array的题目基本都是要求Space Complexity, 而且这到题是在Array这个tag下面的，
希望你练习array的操作，PQ感觉有点作弊。

discussion的答案是用到index

### situation
1. 不需要改变位置, i++
    1. right place， nums[i] = i + 1
    2. no place to put
        - zero && negative value
        - nums[i] > nums.length over the array‘s length

2. nums[nums[i] - 1] != nums[i], 当现在数字不在正确位置上时，⚠️交换以后并不是保证这个位置的值就正确所以不能**i++**
    ```
    ex: 
    i = 4
    nums[4] = 4 + 1
    4 = nums[4] - 1
    i = nums[i] - 1
    ```
   
    - swap(nums[nums[i]-1], nums[i])



3. other i++;

## Complexity
Time: O(n)
Space: O(1)

## Solution
```Java
PriorityQueue<Integer> pq = new PriorityQueue<>();
for (int num : nums) {
    pq.offer(num);
}

int res = 1;
while (!pq.isEmpty()) {
    int num = pq.poll();
    if (num > 0) {
        if (num == res) {
            res++;
        } else if (num > res) {
            return res;
        }
    }
}
return res;
```

``` Java
public int firstMissingPositive(int[] nums) {
    int i = 0;
    while (i < nums.length) {
        if (nums[i] == i + 1 || nums[i] <= 0 || nums[i] >= nums.length){
            i++;  
        }  else if (/*nums[i] < nums.length && nums[i] != i + 1 &&*/ nums[nums[i] - 1] != nums[i]) {
            swap(nums, i, nums[i] - 1);
            //WA: i++;
        } else {
            i++;
        }
    }
    
    i = 0;
    while (i < nums.length && nums[i] == i+1) i++; 
    return i + 1;  
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}  
```