---
title: 二叉树的最大深度
date: 2020-08-13
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 多数元素

给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

## 示例1：
>输入: [3,2,3]  
输出: 3

## 示例2：
>输入: [2,2,1,1,1,2,2]  
输出: 2

## 代码 
```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}

```

