---
title: 相同的树
date: 2020-08-16
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---


## 相同的树

给定两个二叉树，编写一个函数来检验它们是否相同。  

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。
## 示例：
>输入：1->2->4, 1->3->4  
输出：1->1->2->3->4->4

## 代码 
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        } else if (p == null || q == null) {
            return false;
        } else if (p.val != q.val) {
            return false;
        } else {
            return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
        }
    }
}

```

