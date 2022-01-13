---
title: 搜索插入位置
date: 2020-08-04
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---


## 搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。


## 示例1：
>输入: [1,3,5,6], 5  
输出: 2

## 示例2：
>输入: [1,3,5,6], 2  
输出: 1

## 示例3：
>输入: [1,3,5,6], 7  
输出: 4

## 示例4：
>输入: [1,3,5,6], 0  
输出: 0

## 代码
```java
public class Solution {

    public int searchInsert(int[] nums, int target) {
        int len = nums.length;
        if (len == 0) {
            return 0;
        }
        if (nums[len - 1] < target) {
            return len;
        }
        int left = 0;
        int right = len - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
}

```
