---
title: 对称二叉树
date: 2020-08-17
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 对称二叉树


给定一个二叉树，检查它是否是镜像对称的。  

 

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:  


## 进阶：  

你可以运用递归和迭代两种方法解决这个问题吗？  
## 代码 
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    public boolean check(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        if (p == null || q == null) {
            return false;
        }
        return p.val == q.val && check(p.left, q.right) && check(p.right, q.left);
    }
}


```

