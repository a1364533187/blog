---
layout: post
author: 武儿
title: 二叉树的定义
category: 技术
tag: [软件]
---

# 二叉树的定义
## c语言对二叉树的定义
{% highlight js %}
//定义二叉树结构
typedef int DataType;

typedef struct BiTNode
{
	DataType data;
	struct BiTNode *lchild, *rchild;
}BiTNode, *BiTree;
{% endhighlight %}

## java语言定义二叉树
java内部类的使用
class BinaryTree {  
	  
    public Node root;  
      
    /** 
     *  
     * 内部节点类 
     * @author yhh 
     */  
    private class Node{  
        private Node left;  
        private Node right;  
        private int data;  
        public Node(int data){  
            this.left = null;  
            this.right = null;  
            this.data = data;  
        }  
    }  
}
