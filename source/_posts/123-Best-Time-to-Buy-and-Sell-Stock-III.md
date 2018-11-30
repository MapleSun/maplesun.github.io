---
title: 123. Best Time to Buy and Sell Stock III
date: 2018-06-05 22:54:33
tags:
---

## Question

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).



https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/discuss/39615/My-explanation-for-O(N)-solution!

```
To understand the hidden logic, you have to understand what these 4 variables stand for.

sell2: Final profit.
buy2: Best profit so far, if you buy the stock not after Day i (2nd transaction).
sell1: Best profit so far, if you sell the stock not after Day i (1st transaction).
buy1: Minimum price to buy the stock.

The logic between buy1 and sell1 is quite straight forward. What you need to do is simply find a minimum price to buy and sell it some days after.
Of course, sell1 won't update if the profit is not greater than before even if you buy the stock at a lower price. Let's assume you sell the stock at Day a to get the greatest profit for the 1st transaction, which stores in sell1.

Now comes the trick. Assume you find a better deal at Day b, sell1 get updated. So you have 2 choice for buy2:

not update buy2, you still sell your stock at Day a. Nothing changed.
update buy2 with new sell1, which means you sell the stock at Day b.
buy2 = sell1 - price[i] means you sell you stock at Day b and buy it at Day i. And Day i is definitely not early than Day b, which is the hidden logic.
```
## Solution
```Java

public int maxProfit(int[] prices) {
    int sell1 = 0, sell2 = 0, buy1 = Integer.MIN_VALUE, buy2 = Integer.MIN_VALUE;
    for (int i = 0; i < prices.length; i++) {
        buy1 = Math.max(buy1, -prices[i]);
        sell1 = Math.max(sell1, buy1 + prices[i]);
        buy2 = Math.max(buy2, sell1 - prices[i]);
        sell2 = Math.max(sell2, buy2 + prices[i]);
    }
    return sell2;
}


```