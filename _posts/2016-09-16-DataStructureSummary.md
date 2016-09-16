---
layout: post
author: 武儿
title: 数据结构的一小波总结
category: 技术
tag: [软件]
---


# 利用了周末的时间仔细的研究了一下栈，队列，链表，树，二叉树，图的实现，看的收获还是很大的。我用java重写了这些结构的实现，一直看的C语   言版本，用java来重写对数据结构理解更深了
	<br/>
# 栈和队列的实现，我采用的基本结构**ArrayList**, 实现很简单，这里就不写了
	<br/>
# 链表的实现很值得一提，在这里对象的引用与指针的概念，值得去深究一下。
这里给出链表的java实现
	<br/>
<h2>首先定义一个链表的节点结构</h2>
{% highlight js %}
	//先定义一个节点对象
class Node{
	//数据域
	public Object data;
	//指针域
	public Node link;
	
	public Node(){
		this.data = null;
		this.link = null;
	}
	
	public Node(Object obj){
		this.data = obj;
		this.link = null;
	}
}
{% endhighlight %}

<br/>
然后我们开始创建我们的链表
{% highlight js %}
//定义一个单端链表   理解单链表的头节点与指针
class LinkedList{
	//定义一个头节点
	public Node header;
	//定义一个指向指向当前节点的指针
	public Node Current;
	//定义单链表的长度
	public  int count;
	
	//初始化单链表
	public LinkedList(){
		count = 0 ;
		//造一个头节点
		header = new Node("Header");
		header.link = null;
		
		//当前的指针指向头节点
		Current = header;
	}
	
	//打印单链表
	public void PrintList(){
		Current = header;
		while(Current.link!=null){
			System.out.println(Current.link.data);
			Current = Current.link;
		}
	}
	
	//给单链表添加节点
	public void addNodeToTail(Object obj){
		Node n = new Node(obj);
		Current.link = n;
		Current = Current.link;
		count++;
	}
	
	//把单链表清空
	public void listEmpty(){
		//将头节点指向空
		header.link = null;
		//将链表指针指向头节点
		Current = header;
	}
	
	//删除第i个位置的元素
	public void delNodeByNum(int i){
		if(i<0||i>count-1){
			System.out.println("删除第i个位置元素无效。。");
			return;
		}
		//将Current指向头节点
		Current = header;
		int index = -1;                                                     
		//找到第i个元素的前一个位置
		while(index !=i-1){
			Current = Current.link;
			index++;
		}
		
		Current.link = Current.link.link; 
		count--;
	}
	
	//在第i个位置添加元素
	public void AddNodeByNum(int i,Object obj){
		if(i<0||i>count-1){
			System.out.println("插入的位置无效。。");
			return;
		}
		//将current指针指向头节点
		Current = header;
		
		//找到要插入元素的前一个位置
		int index = -1;
		while(index != i-1){
			Current  = Current.link;
			index++;
		}
		
		//开始添加元素了
		Node n = new Node(obj);
		n.link = Current.link;
		Current.link = n;
		
		count++;
		
	}
}
{% endhighlight %}
