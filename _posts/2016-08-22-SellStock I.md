---
layout: post
author: 武儿
title: 【leetcode】Best Time to Buy and Sell Stock I
category: 技术
tag: [软件]
---

Best Time to Buy and Sell Stock I
# 题意：
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

## Example 1:
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)

## Example 2:
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.

##  method 1
超时，我首先想到的方法，方法思想，将数组中每两个数都进行比较，运用两层for循环即可，这个方法不好，
时间复杂度O(n*n)，以后想到这种方法就应该再想更优化的方法
{% highlight js %}

class Solution {
    public int maxProfit(int[] prices) {
    	int maxPro = 0;
        for (int i = 0; i < prices.length-1; i++) {
			for (int j = i+1; j < prices.length; j++) {
				int profit = prices[j]-prices[i];
				if(profit>maxPro){
					maxPro = profit;
				}
			}
		}
        return maxPro;
    }
}

{% endhighlight %}

# method 2
**动态规划法**：从前向后遍历数组，记录当前出现过的最低价格，作为买入价格，并计算以当天价格出售的收益，
作为可能的最大收益，整个遍历过程中，出现过的最大收益就是所求。
{% highlight js %}

public class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length < 2) return 0;
        
        int maxProfit = 0;
        int curMin = prices[0];
        
        for (int i = 1; i < prices.length; i++) {
            curMin = Math.min(curMin, prices[i]);
            maxProfit = Math.max(maxProfit, prices[i] - curMin);
        }
        
        return maxProfit;
    }
}

{% endhighlight %}