
---
layout: post
author: 武儿
title: 重写二叉树
category: 技术
tag: [软件]
---

一直觉得用java来创建二叉树有点麻烦，因为我想传入一组数，就可以创建好二叉树，而不只是一个节点一个节点的去创建二叉树，这种方式代码冗长，很shit。。
#这里给出二叉树的树的节点定义
{% highlight js %}
//定义一个树节点
class TreeNode{
	public Object data;
	public TreeNode lchild;
	public TreeNode rchild;
	
	public TreeNode(Object obj){
		this.data = obj;
		this.lchild = null;
		this.rchild = null;
		
	}
}
{% endhighlight %}

<br/>
然后我们开始创建我们的二叉树，创建二叉树采用顺序存储结构的方式，这样传入一组Object[]数组，就可以创建一棵二叉树，这感觉棒棒的。。
{% highlight js %}
//定义一棵树
class Tree{
	//定义一个树的头节点
	public TreeNode root;
	//定义一个指向当前树节点的指针，即引用
	private TreeNode current;

	public Tree(){
		root = null;
	}
	//创建一棵树    用顺序存储结构实现二叉树      用一个ArrayList来实现
	public void createTreeByOrder(Object[] objs){
		//定义一个ArrayList 来存储树的节点；
        ArrayList<TreeNode>  listNode = new ArrayList<TreeNode>();
        root = new TreeNode(objs[0]);
        listNode.add(root);
        current = root;
        for (int i = 0; i < objs.length/2; i++) {
			if(listNode.get(i)==null){
				continue;
			}
			else{
				current = listNode.get(i);
				if(2*i+1<objs.length){
					if(objs[2*i+1]==null){
						listNode.add(null);
					}
					else{
						TreeNode tnlnode = new TreeNode(objs[2*i+1]);
						current.lchild = tnlnode;
						listNode.add(tnlnode);
					}
					if(objs[2*i+2]==null){
						listNode.add(null);
					}
					else{
						TreeNode tnrnode = new TreeNode(objs[2*i+2]);
						current.rchild = tnrnode;
						listNode.add(tnrnode);
					}
				}
			}
		}
	}
}
{% endhighlight %}
<br/>
树的3种遍历方式
{% highlight js %}
//前序遍历二叉树
	public void preOrderTraverse(TreeNode root){
		if(root ==null){
			return;
		}
		else{
			System.out.print(root.data+"  ");
			preOrderTraverse(root.lchild);
			preOrderTraverse(root.rchild);
		}
	}
	
	//中序遍历
	public void inOrderTraverse(TreeNode root){
		if(root == null){
			return;
		}
		else{
			inOrderTraverse(root.lchild);
			System.out.print(root.data+"   ");
			inOrderTraverse(root.rchild);
		}
	}
	
	//后序遍历
	public void postOrderTraverse(TreeNode root){
		if(root == null){
			return;
		}
		else{
			postOrderTraverse(root.lchild);
			postOrderTraverse(root.rchild);
			System.out.print(root.data+"  ");
		}
	}
{% endhighlight %}







