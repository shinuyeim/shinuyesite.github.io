---
title: 合并两个有序数组
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 合并两个有序数组

给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。


## 说明：
>+ 初始化 nums1 和 nums2 的元素数量分别为 m 和 n.   
>+ 你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。

## 示例1：
>输入:
nums1 = [1,2,3,0,0,0], m = 3  
nums2 = [2,5,6],       n = 3  

>输出: [1,2,2,3,5,6]

## 代码
```java
class Solution {
  public void merge(int[] nums1, int m, int[] nums2, int n) {
    int [] nums1_copy = new int[m];
    System.arraycopy(nums1, 0, nums1_copy, 0, m);

    int p1 = 0;
    int p2 = 0;

    int p = 0;

    while ((p1 < m) && (p2 < n))
      nums1[p++] = (nums1_copy[p1] < nums2[p2]) ? nums1_copy[p1++] : nums2[p2++];

    if (p1 < m)
      System.arraycopy(nums1_copy, p1, nums1, p1 + p2, m + n - p1 - p2);
    if (p2 < n)
      System.arraycopy(nums2, p2, nums1, p1 + p2, m + n - p1 - p2);
  }
}

```

## 说明：
System.arraycopy()

>public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)

### 参量
>src-这是源数组。
>
>srcPos-这是源数组中的起始位置。
>
>dest-这是目标数组。
>
>destPos-这是目标数据中的起始位置。
>
>length-这是要复制的数组元素的数量。
