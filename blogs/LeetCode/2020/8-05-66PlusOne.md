---
title: 加一
date: 2020-08-05
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 加一 

给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。


## 示例1：
>输入: [1,2,3]  
输出: [1,2,4]  
解释: 输入数组表示数字 123。

## 示例2：
>输入: [4,3,2,1]  
输出: [4,3,2,2]  
解释: 输入数组表示数字 4321。

## 代码
```java
class Solution {
   public int[] plusOne(int[] digits) {
    for (int i = digits.length - 1; i >= 0; i--) {
        if (digits[i] < 9) {
            digits[i] += 1;
            break;
        } 
        digits[i] = 0; 
    }

    if (digits[0] == 0) {
        int[] ans = new int[digits.length + 1];
        ans[0] = 1; 
        digits = ans;
    }
    return digits;
    }
}
```
