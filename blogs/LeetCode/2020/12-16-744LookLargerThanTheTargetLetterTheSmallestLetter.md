---
title: 寻找比目标字母大的最小字母  
date: 2020-12-16
tags:
 - 简单
 - 力扣
 - 二分搜索
categories:
 - 算法笔记
---


## 题目描述
给你一个排序后的字符列表 letters ，列表中只包含小写英文字母。另给出一个目标字母 target，请你寻找在这一有序列表里比目标字母大的最小字母。

在比较时，字母是依序循环出现的。举个例子：

如果目标字母 target = 'z' 并且字符列表为 letters = ['a', 'b']，则答案返回 'a'


## 示例
::: tip  
输入:  
letters = ["c", "f", "j"]  
target = "a"  
输出: "c  

输入:  
letters = ["c", "f", "j"]  
target = "c"  
输出: "f"  

输入:  
letters = ["c", "f", "j"]  
target = "g"  
输出: "j"  

输入:  
letters = ["c", "f", "j"]  
target = "j"  
输出: "c"  

输入:  
letters = ["c", "f", "j"]  
target = "k"  
输出: "c"  
:::  


## 算法设计
这是一个有序数组，并且数组中也没有重复的元素，我们运用二分法查找时。二分查找分几轮进行，在每一轮中我们保持循环始终在区间 [lo，hi]。让 mi = (lo + hi) / 2。若 letters[mi] <= target，则我们修改查找区间为 [mi + 1, hi]，否则，我们修改为 [lo, mi]。  
最后，如果插入位置是最后一个位置 letters.length，则返回 letters[0]。这就是模运算的运用。

## 代码
```c
char nextGreatestLetter(char* letters, int lettersSize, char target){
    int lo = 0, hi = lettersSize;
    while (lo < hi) {
        int mi = lo + (hi - lo) / 2;
        if (letters[mi] <= target) lo = mi + 1;
        else hi = mi;
    }
    return letters[lo % lettersSize];
}
```

## 复杂度分析  
时间复杂度：O(\log N)O(logN)。NN 指的是 letters 的长度，我们只查看数组中的 \log nlogn 个元素。  
空间复杂度：O(1)O(1)。只使用了指针。  