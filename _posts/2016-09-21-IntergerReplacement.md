---
layout: post
author: 武儿
title: 【leetcode】 Integer Replacement
category: 技术
tag: [软件]
---
397. Integer Replacement

Given a positive integer n and you can do operations as follow:
<br/>
If n is even, **replace n with n/2**.
<br/>
If n is odd, you can replace n with **either n + 1 or n - 1**.
<br/>
What is the minimum number of replacements needed for n to become 1?

##Example 1:
{% highlight js %}
Input:
8

Output:
3

Explanation:
8 -> 4 -> 2 -> 1
{% endhighlight %}

##Example 2:
{% highlight js %}
Input:
7

Output:
4

Explanation:
7 -> 8 -> 4 -> 2 -> 1
or
7 -> 6 -> 3 -> 2 -> 1
{% endhighlight %}

#method 1
<br/>
需要一定的数学思维，一般是想不到的，但是某些地方还是很可取的。
这题思路就是：
<br/>
1. 偶数的话，直接砍半，再运算。
<br/>
2. 奇数的话，分两种情况，因为我们的目的是用最少的操作，所以，尾数分01, 和11的奇数要分别考虑：01的情况，需要直接-1，11的情况用+1，变成100然后再做会快很多。
<br/>
但是这里有个特殊的例子3，是-1的，要特殊处理，这样运算会快。
<br/>
另外，>>>和>>的区别在于，>>>是无符号位的位移，>>是有符号位的位移。
{% highlight js %}
	/********************************************************
		 * 5  二进制表示  101   1二进制   001       5&1 = 1   
		 * 8 二进制表示  1000  1二进制  0001       8&1 = 0
		 * 在这里发现没？   判断n是否为偶数    1.    n%2==0    2.    n&1==0
		 *           判断n是否为奇数     1.      n%2==1      2.     n&1==1 
		 */
	public int integerReplacement(int n) {
    	int count = 0;
    	while(n!=1){
    		if((n&1)==0){
    			n = n>>>1;
    		}
    		else if(n==3||((n>>>1)&1)==0){
    			n--;
    		}
    		else{
    			n++;
    		}
    		count++;
    	}
    	
    	return count;
    }
{% endhighlight %}

#method 2
<br/>
通用的解法就是递归，这个只要你想明白这个递归的过程。
同时要注意一点， Integer.MAX_VALUE = 2147483647  如果加1就溢出了.
{% highlight js %}
 public int integerReplacement(int n) {
    	//采用递归的方法     这里注意 Integer.MAX_VALUE = 2147483647  如果加一就溢出了
    	if(n == Integer.MAX_VALUE){
    		return 32;
    	}
    	if(n==1){
    		return 0;
    	}
    	if((n&1)==0){
    		return 1+integerReplacement(n/2);
    	}
    	else{
    		return Math.min(1+integerReplacement(n-1), 1+integerReplacement(n+1));
    	}
    }
{% endhighlight %}
