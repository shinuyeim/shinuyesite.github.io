---
title: 按照频率将数组升序排序
date: 2021-01-08
tags:
 - 简单
 - 力扣
 - 哈希表
categories:
 - 算法笔记
---



## 题目描述
给你一个整数数组 nums ，请你将数组按照每个值的频率升序排序。如果有多个值的频率相同，请你按照数值本身将它们降序排序。 

请你返回排序后的数组。

## 示例
::: tip  
输入：nums = [1,1,2,2,2,3]  
输出：[3,1,1,2,2,2]  
解释：'3' 频率为 1，'1' 频率为 2，'2' 频率为 3 。  

输入：nums = [2,3,1,3,2]  
输出：[1,3,3,2,2]  
解释：'2' 和 '3' 频率都为 2 ，所以它们之间按照数值本身降序排序。  

输入：nums = [-1,1,-6,4,5,-6,1,4,1]  
输出：[5,-1,4,4,-6,-6,1,1,1]  
:::  

Tips:      
1. 1 <= nums.length <= 100。  
2. -100 <= nums[i] <= 100。

## 算法设计
这一题的难度比其他简单难度的难一点，读完题目时感觉这题很简单，但是编起来就不是那么容易了。

## 代码
哈希
```c
#define NUM_MAX 201
int g_hash[NUM_MAX];

int cmp(const void *a, const void *b)
{
    int tmpa = *(int *)a + 100;
    int tmpb = *(int *)b + 100;
    // 如果频率相等，数字降序排序
    if (g_hash[tmpb] == g_hash[tmpa]) {
        return tmpb - tmpa;
    }
    // 如果频率不等，频率升序排序
    return g_hash[tmpa] - g_hash[tmpb];
}

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int *frequencySort(int *nums, int numsSize, int *returnSize)
{

    memset(g_hash, 0, sizeof(int) * NUM_MAX);
    for (int i = 0; i < numsSize; i++) {
        g_hash[nums[i] + 100]++;
    }
    qsort(nums, numsSize, sizeof(int), cmp);

    *returnSize = numsSize;
    return nums;
}

## 复杂度分析     
时间复杂度：O(nlogn)，其中 n 为 s 的长度。排序的时间复杂度为 O(nlogn)，比较两个字符串是否相等时间复杂度为 O(n)，因此总体时间复杂度为 O(n log n + n) = O(nlogn)。



