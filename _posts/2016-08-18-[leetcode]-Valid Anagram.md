---
layout: post
author: 武儿
title: 【leectode】：Valid Anagram(有效的字谜)
category: 技术
tag: [总结]
---

Valid Anagram

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

# Note:
You may assume the string contains only lowercase alphabets.

## method 1
利用小写字母只有26个，统计s字符串中每个字母的个数，再与t中的字母相比较，判断最后s与t是否相等

{% highlight js %}
public class Solution {
    	 public boolean isAnagram(String s, String t) {
		 if(s.length()!=t.length()){
			 return false;
		 }
		 int[] abcs =new int[26];
		 for (int i = 0; i < s.length(); i++) {
			abcs[s.charAt(i)-'a']++;
		 }
		 
		 for (int i = 0; i < t.length(); i++) {
			--abcs[t.charAt(i)-'a'];
		}
		 
		 for (int i = 0; i < abcs.length; i++) {
			if(abcs[i]!=0){
				return false;
			}
		}
		 return true;
	 }
}
{% endhighlight %}

## method 2
对字符串s与t进行排序，排完序后，判断字符串s与t是否相等
{% highlight js %}
class Solution {
	public boolean isAnagram(String s, String t) {
	    char[] sChar = s.toCharArray();
	    char[] tChar = t.toCharArray();
	    Arrays.sort(sChar);
	    Arrays.sort(tChar);
	    return Arrays.equals(sChar, tChar);
	}
}
{% endhighlight %}

## method 3
超时，但是最容易想出，判断s中的每个字符是否在t中能找到，核心定义一个数组大小等于t,判断该数组是否每一位都等于1，若是，则满足条件
{% highlight js %}
public boolean isAnagram(String s, String t) {
    	if(s.length()!=t.length()){
    		return false;
    	}
    	int[] tts = new int[s.length()];
        for (int i = 0; i < s.length(); i++) {
			for (int j = 0; j < t.length(); j++) {
				if(tts[j]==0&&(s.charAt(i)==t.charAt(j))){
					tts[j]=1;
					break;
				}
			}
		}
        int sumn=0;
        for (int i = 0; i < tts.length; i++) {
			if(tts[i]==1){
				sumn++;
			}
		}
        if(sumn>=s.length()){
        	return true;
        }
        return false;
    }
{% endhighlight %}

