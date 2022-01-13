---
title: 整数反转
date: 2020-07-31
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 整数反转 

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。


## 示例1：
>输入: 123  
输出: 321

## 示例2：
>输入: -123  
输出: -321

## 示例3：
>输入: 120  
输出: 21

## 注意：
假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

## 代码
```java
class Solution {
    public int reverse(int x) {
        long y = x;
        long res = 0;
        do{
            res = 10*res + y % 10;
        }while((y = y / 10) != 0);
        if(res < Integer.MIN_VALUE || res > Integer.MAX_VALUE){
            return 0;
        }
        return (int) res;
    }
}
```