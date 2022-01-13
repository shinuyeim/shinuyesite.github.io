---
title: 实现 strStr()
date: 2020-08-15
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 实现 strStr()

实现 [^strStr()] 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。


## 示例1：
>输入: haystack = "hello", needle = "ll"  
输出: 2

## 示例2：
>输入: haystack = "aaaaa", needle = "bba"  
输出: -1

## 说明：
当 [^needle] 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 [^needle] 是空字符串时我们应当返回 0 。这与C语言的 [^strstr()] 以及 Java的 [^indexOf()] 定义相符。


## 代码 
```java
class Solution {
    public int strStr(String haystack, String needle) {
    if (needle.length() == 0) {
        return 0;
    }
    int j = 0;
    for (int i = 0; i < haystack.length(); i++) {
        if (haystack.charAt(i) == needle.charAt(j)) {
            j++;
            if (j == needle.length()) {
                return i - j + 1;
            }
        } else {
            i = i - j;
            j = 0;
        }
    }
    return -1;
    }
}
```

