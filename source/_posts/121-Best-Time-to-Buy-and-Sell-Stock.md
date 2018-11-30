---
title: 121. Best Time to Buy and Sell Stock
date: 2018-06-05 22:29:30
tags:
---

## Question
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

## Analysis
我的想法 O(n^2), 用两个loop 去检查当前位置的最大profit， 再用一个loop比较取得最大的profit

可以通过记录当前最小值来减少时间复杂度 O(n)


## Solution
```Java
// O(n)
public int maxProfit(int[] prices) {
    if (prices == null || prices.length == 0) return 0;
    int max = 0;
    int sofarMin = prices[0];
    
    for (int i = 1; i < prices.length; i++) {
        max = Math.max(max, prices[i] - sofarMin);
        if (prices[i] < sofarMin) {
            sofarMin = prices[i];
        }
    }
    return max;
}

// O(n ^ 2)
public int maxProfit(int[] prices) {
    int[] profit = new int[prices.length];
    
    for (int i = 0; i < prices.length; i++) {
        int max = 0;
        for (int j = i+1; j < prices.length; j++) {
            max = Math.max(prices[j]-prices[i], max);
        }
        profit[i] = max;
    }
    
    int maxProfit = 0;
    for (int i = 0; i < prices.length; i++) {
        maxProfit = Math.max(profit[i], maxProfit);
    }
    
    return maxProfit;
}
```