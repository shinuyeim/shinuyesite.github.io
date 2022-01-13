---
title: 两个数组的交集||
date: 2021-05-21
tags:
 - 简单
 - 力扣
 - 排序
categories:
 - 算法笔记
---

## 题目描述
给定两个数组，编写一个函数来计算它们的交集。

## 示例
::: tip  
输入：nums1 = [1,2,2,1], nums2 = [2,2]   
输出：[2,2]   

输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]  
输出：[9,4]  
:::  

Tips:      
1. 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。    
2. 我们可以不考虑输出结果的顺序。  

## 算法设计
这个题也是一个合并数组元素的题目，和上个题不一样的是这个题可以保留重复元素，所以还比上一个题更加简单。首先我们也先进性排序，然后用两个指针遍历数组。当其中一个指针超出数组范围的时候，遍历结束。

## 代码
```c
int cmp(void* a, void* b) {
    int* pa = (int*)a;
    int* pb = (int*)b;
    int num1 = *pa;
    int num2 = *pb;
    return num1 - num2;
}

int* intersect(int* nums1, int nums1Size, int* nums2, int nums2Size,int* returnSize) {
    qsort(nums1, nums1Size, sizeof(int), cmp);
    qsort(nums2, nums2Size, sizeof(int), cmp);
    *returnSize = 0;
    int* intersection = malloc(sizeof(int) * (nums1Size + nums2Size));

    int i = 0, j = 0;
    while (i < nums1Size && j < nums2Size) {
        int num1 = nums1[i], num2 = nums2[j];
        if (num1 == num2) {
                intersection[(*returnSize)++] = nums1[i];
                i++;
                j++; 
        }else if (num1 < num2) {
            i++;
        }else {
            j++;  
        }
    }
    return intersection;
}
```

## 复杂度分析     
时间复杂度：对两个数组进行排序的时间复杂度是O(nlogn)，这是快速排序算法的平均复杂度，n为数组的长度，遍历两个数组的时间复杂度是O(m+n)，m和n是两个数组的长度，所以总的时间复杂度为O(mlogm + nlogn)。

空间复杂度：返回数组中数组占用的长度为额外的空间，在此题中，返回数组的最长长度不会超出原来两个数组中最短的数组长度，所以空间复杂度为两个数组长度小的那个数组长度，O(min(m,n))。