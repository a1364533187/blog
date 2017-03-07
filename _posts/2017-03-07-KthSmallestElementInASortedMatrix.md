---
layout: post
author: 武儿
title: 求子集问题四种解法
category: 技术
tag: [软件]
---

#方法一 ： 二分查找是二维的二分查找，以及 方法二 优先队列(可以当作最大堆或者最小堆来使用，并且更灵活)
<br/>
#题目：
Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.
<br/>
Note: You may assume k is always valid, 1 ≤ k ≤ n**2.
{% highlight js %}
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
{% endhighlight %}

先介绍一种二维空间上的二分查找的写法
#method 1
先定义upper_bound()函数，来找到查找数的上界
二分查找1:  对矩阵每一行都进行upper_bound()的操作，求和，可求出大于查找数的个数len
二分查找2： 拿len和k比较，来调整查找数的范围
最后找到合适的查找数
{% highlight js %}
    class Solution1{
    //by 二分查找
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int small = matrix[0][0];
        int large = matrix[n-1][n-1];
        
        while(small<=large){
            int mid = small+(large-small)/2;
            int len = 0;   //每次求的len应该都赋予0
            for (int i = 0; i < matrix.length; i++) {
                //利用upper_bound去求每一行 > 查找值  的界限
                len += upper_bound(matrix[i], mid);
            }    //len 求出每一行 > mid 值的和
            if(len>=k){
                large = mid-1;
            }else{
                small = mid +1;
            }
        }
        
        return large +1;
    }
    
    /*********************************************************
     * 函数upper_bound()返回的在前闭后开区间查找的关键字的上界，
     * 如一个数组number序列1,2,2,4.upper_bound(2)后，
     * 返回的位置是3（下标）也就是4所在的位置,同样，如果插入元素大于数组中全部元素，
     * 返回的是last。（注意：此时数组下标越界！！）
     * 返回查找元素的最后一个可安插位置，也就是“元素值>查找值”的第一个元素的位置
     */
    
    public int upper_bound(int[] nums,int val){
        int start = 0;
        int end  = nums.length-1;
        while(start<=end){
            int mid  = start +(end-start)/2;
            if(nums[mid]<=val){
                start = mid+1;
            }else{
                end = mid-1;
            }
        }
        return end+1;
    }
} 
{% endhighlight %}

#method 2
   采用优先队列(可以灵活的当作最大堆或者最小堆使用)，行有序，列有序，行与行之间不一定有序
   但是数matrix[i][j]一定小于 matrix[i+1][j]及matrix[i][j+1] 
   每次弹出优先队列的首元素，同时添加matrix[i][j]的正下方的元素，
   和前方的元素(没有添加的情况下)，这样每次保证弹出的是最小值
{% highlight js %}
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        boolean[][] visited = new boolean[n][n];
        Comparator<MinNum>  cmp = new Comparator<MinNum>() {

            public int compare(MinNum o1, MinNum o2) {
                // TODO 自动生成的方法存根
                return o1.val - o2.val;
            }
        };
        PriorityQueue<MinNum> priQue = new  PriorityQueue<MinNum>(n*n,cmp);
    
        priQue.add(new MinNum(0, 0, matrix[0][0])); 
        visited[0][0] = true;
        while(k>1){   //这是弹出的第k个数就是我们的第k个最小值
            MinNum  mu  = priQue.poll();
            k--;
            if(mu.i+1<n &&visited[mu.i+1][mu.j]==false){
                priQue.add(new MinNum(mu.i+1, mu.j, matrix[mu.i+1][mu.j]));
                visited[mu.i+1][mu.j] = true;
            }
            if(mu.j+1<n && visited[mu.i][mu.j+1]==false){
                priQue.add(new MinNum(mu.i, mu.j+1, matrix[mu.i][mu.j+1]));
                visited[mu.i][mu.j+1] = true;
            }
        }
        return priQue.poll().val;
    }
}

class MinNum{
    int i;
    int j;
    int val;
    public MinNum(int i , int j ,int val) {
        // TODO 自动生成的构造函数存根
        this.i = i;
        this.j = j;
        this.val = val;
    }
}
{% endhighlight %}
