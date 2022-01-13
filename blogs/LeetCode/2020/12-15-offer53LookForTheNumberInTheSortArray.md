---
title: 在排序数组中查找数字 1
date: 2020-12-15
tags:
 - 简单
 - 力扣
 - 二分搜索
categories:
 - 算法笔记
---

## 题目描述
统计一个数字在排序数组中出现的次数。

## 示例
::: tip  
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2  

输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
:::  


## 算法设计
首先，数组已经是排好序的，所以在对排好序的数组进行查询时，最好的方法就是采用二分查找法（以我目前的知识）。我们要的结果是数字出现的次数，也就是求出这个排序数组中某一个数字的个数有几个。我们可以想到，当查找到这个数字时，left（左指针）和right（右指针）的差值加一就是我们要的结果。所以我们有以下代码。

## 代码
```c
int search(int* nums, int numsSize, int target){
    // 搜索右边界 right
        int i = 0, j = numsSize - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] <= target) i = m + 1;
            else j = m - 1;
        }
        int right = i;
        // 若数组中无 target ，则提前返回
        if(j >= 0 && nums[j] != target) return 0;
        // 搜索左边界 right
        i = 0; j = numsSize - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] < target) i = m + 1;
            else j = m - 1;
        }
        int left = j;
        return right - left - 1;
}
```

## 复杂度分析  
时间复杂度 O(log N)O(logN) ： 二分法为对数级别复杂度。  
空间复杂度 O(1)O(1) ： 几个变量使用常数大小的额外空间。  