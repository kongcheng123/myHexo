---
title: 最大收益问题
date: 2017-12-26 22:46:24
tags:
- 算法
---
>leetcode 第121题 

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:
```
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```
Example 2:
```
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```
解法:
```
/**
 * @author xy
 * @date 2017/12/26 22:23
 *
 * 121. Best Time to Buy and Sell Stock
 *
 * Say you have an array for which the ith element is the price of a given stock on day i.
 *
 * If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.
 *
 * Example 1:
 * Input: [7, 1, 5, 3, 6, 4]
 * Output: 5
 *
 * max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
 * Example 2:
 * Input: [7, 6, 4, 3, 1]
 * Output: 0
 *
 * In this case, no transaction is done, i.e. max profit = 0.
 */
public class leetcode_121 {
    public static void main(String[] args) {
        int[] a = {7, 6, 4, 3, 1};
        System.out.println(maxProfit(a));
    }

    //复杂度为O(n2),容易超时
    public static int maxProfit(int[] prices) {
        int max = 0;
        for(int i = 0;i < prices.length;i++){
            for(int j = i;j < prices.length;j++){
                if(prices[j]-prices[i] > max){
                   max = prices[j]-prices[i];
                }
            }
        }
        return max;
    }

    //网上做法，复杂度为O(n)
    public int maxProfit_2(int prices[]) {
        int minprice = Integer.MAX_VALUE;
        int maxprofit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minprice) {
                minprice = prices[i];
            }
            else if (prices[i] - minprice > maxprofit) {
                maxprofit = prices[i] - minprice;
            }
        }
        return maxprofit;
    }
}

```
