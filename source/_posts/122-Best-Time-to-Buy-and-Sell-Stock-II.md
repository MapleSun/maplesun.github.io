---
title: 122. Best Time to Buy and Sell Stock II
date: 2018-06-05 22:43:42
tags:
---
## Question
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).


## Analysis
Sell and buy on the same day == not sell

## Complexity
Time: O(n)

## Solution
``` Java
public int maxProfit(int[] prices) {
    int profit = 0;
    for (int i = 1; i < prices.length; i++) {
        if (prices[i] - prices[i-1] > 0) {
            profit += prices[i] - prices[i-1];
        }
    }
    return profit;
}
```