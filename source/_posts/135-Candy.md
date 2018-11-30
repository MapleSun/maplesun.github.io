---
title: 135. Candy
date: 2018-06-07 00:31:26
tags:
---
## Question
There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.
What is the minimum candies you must give?

## Analysis
基本的，每个孩子最少要拿到一枚糖，
从左往右如果`ratings[i] < ratings[i+1]` 第i+1th孩子 应该 拿到ith 孩子的糖 + 1
从右往左`ratings[i-1] > ratings[i]` 并且 i-1th 孩子的糖少于 ith孩子 第i-1th孩子 应该 拿到ith 孩子的糖 + 1

## Complexity
Time: O(n)
Space: O(n)

## Solution
```Java
public int candy(int[] ratings) {
    int sum = 0;
    int[] a = new int[ratings.length];
    for (int i = 0; i < a.length; i++) {
        a[i] = 1;
    }
    for (int i = 0; i < ratings.length - 1; i++) {
        if (ratings[i+i] > ratings[i]) {
            a[i+1] = a[i] + 1;
        }
    }

    for (int i = ratings.length - 1; i > 0; i--) {
        if (ratings[i-1] > ratings[i]) {
            if (a[i-1] < (a[i] + 1)) {
                a[i-1] = a[i] + 1;
            }
        }
    }
    for (int i = 0; i < a.length; i++) {
        sum += a[i];
    }

    return sum;
}
```