---
title: 两个数组的交集
date: 2021-05-14
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
输出：[2]  

输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]  
输出：[9,4]  
:::  

Tips:      
1. 输出结果中的每个元素一定是唯一的。  
2. 我们可以不考虑输出结果的顺序。  

## 算法设计
需要求解两个数组的交集，也就是说找出两个数组中的相同元素，然后输出。

首先想到的就是采用双指针，遍历循环两个数组，遇到相同的元素就添加到一个新的数组中。这是最暴力的方法，在不排序的前提下对两个数组求交集，要求最后的元素不重复，是不方便的，因为每一次当两个数组中出现同一个元素的时候，还要到返回数组中查找元素是否已经存在，并不有利于算法的设计。我们可以对其进行优化，就是先把原数组排序，排序后我们就在每一次要在返回数组增加元素时，只需判断待增加元素与返回数组最后一个元素是否相等，如果相等就不把元素加入到放回数组，这样能很方便的保证元素的唯一性。

所以先对原数组进行排序，然后再遍历数组，逐个找到相同的元素。

**qsort**函数的具体使用方法参见[qsort函数使用方法简介](https://shinuyeim.github.io/shinuye-site/views/PCCNotes/20210521Qsort.html)

## 代码
```c
int cmp(void* a, void* b) {
    int* pa = (int*)a;
    int* pb = (int*)b;
    int num1 = *pa;
    int num2 = *pb;
    return num1 - num2;
}

int* intersection(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize) {
    //先对两个数组进行排序，方便后续的查找
    qsort(nums1, nums1Size, sizeof(int), cmp);
    qsort(nums2, nums2Size, sizeof(int), cmp);

    *returnSize = 0;
    int i = 0, j = 0;
    int* intersection = malloc(sizeof(int) * (nums1Size + nums2Size));

    while (i < nums1Size && j < nums2Size) {   // 总结1
        int num1 = nums1[i], num2 = nums2[j];  // 总结2
        if (num1 == num2) {
            // 保证加入元素的唯一性
            if (!(*returnSize) || num1 != intersection[(*returnSize) - 1]) {
                intersection[(*returnSize)++] = num1;
            }
            i++;
            j++;
        } else if (num1 < num2) {
            i++;
        } else {
            j++;
        }
    }
    return intersection;
}
```

## 复杂度分析     
时间复杂度：O(nlogn)，其中 n 为 s 的长度。排序的时间复杂度为 O(nlogn)，比较两个字符串是否相等时间复杂度为 O(n)，因此总体时间复杂度为 O(n log n + n) = O(nlogn)。

## 总结
1. 这里用while而不用for的原因是因为两个数组的长度不一定一样长，排完序后的数组，只要其中一个遍历完成，那么两个数组中的公共元素一定找完了，节省了遍历时间，尤其当两个数组长度相差很大的时候体现的尤为明显。  
2. 这里也可以不需要变量num1和num2，但是为了便于后面的书写，增加上两个变量是值得的。