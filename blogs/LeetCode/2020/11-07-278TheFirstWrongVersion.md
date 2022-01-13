---
title: 第一个错误的版本
date: 2020-11-07
tags:
 - 简单
 - 力扣
 - 二分搜索
categories:
 - 算法笔记
---


## 题目描述
你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

## 示例
::: tip  
给定 n = 5，并且 version = 4 是第一个错误的版本   

调用 isBadVersion(3) -> false  
调用 isBadVersion(5) -> true  
调用 isBadVersion(4) -> true  

所以，4 是第一个错误的版本。     

:::

## 算法设计
分析可知此题可用二分搜索算法求解，我们需要找出出错的版本，借助bool isBadVersion(version)接口判断是否出错，分析可知有两种情况：
> + 1. 假如isBadVersion(middle)返回false，则证明出错的版本在middle之后，则我们令left = middle + 1。
> + 2. 假如isBadVersion(middle)返回true，则证明出错的版本在middle之前（也包括可能第一个出错的版本就是middle），此时我们下次的查找范围就是[left , middle]。


### 代码
最后的结果为：
```c
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

int firstBadVersion(int n) {
    int left = 1;
    int right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (isBadVersion(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

### 复杂性分析
时间复杂度：O(logn)。搜索空间每次减少一半，因此时间复杂度为O(logn)。
空间复杂度：O(1)。


### 思考
> + 1.假如就是middle是第一出错的，有什么改进可以快速找到错误版本的方式吗？
提示：middle出错的话，前一个版本就是正确的。
