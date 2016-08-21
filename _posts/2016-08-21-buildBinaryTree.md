---
layout: post
author: 武儿
title: 建立二叉树
category: 技术
tag: [软件]
---

># 二叉树的建立

## ## c语言建立二叉树  注意二叉树使用的是指针的指针，也就是双重指针，为什么呢？因为我们要改变每个节点的指向，所以所要指针的指针，这里要对比链表的结构

{% highlight js %}
void CreateBiTree(BiTree *T)
{
	char c;
	scanf_s("%c", &c);
	if (' ' == c)
	{
		*T = NULL;
	}
	else
	{
		*T = (BiTNode *)malloc(sizeof(BiTNode));
		(*T)->data = c;
		CreateBiTree(&((*T)->lchild)); 
		CreateBiTree(&(*T)->rchild);
	}
}
{% endhighlight %}

## java语言建立二叉树
## java语言建立二叉树，改变节点的指向，这个比较麻烦，不过我们可以一个节点，一个节点的建立二叉树,我所见到的代码几乎都是这样的，这就不列举了。

># 再谈一下二叉搜索树的建立

##c语言建立二叉搜索树
{% highlight js %}

{% endhighlight %}

##java语言建立二叉搜索树
{% highlight js %}
 public void buildBSTree(Node node,int data){  

    	if(root == null){  
            root = new Node(data);  
        }else{  
            if(data < node.data){  
                if(node.left == null){  
                    node.left = new Node(data);  
                }else{  
                	buildBSTree(node.left,data);  
                }  
            }else{  
                if(node.right == null){  
                    node.right = new Node(data);  
                }else{  
                	buildBSTree(node.right,data);    //这儿运用到递归    核心
                }  
            }  
        }  
    }  
{% endhighlight %}
