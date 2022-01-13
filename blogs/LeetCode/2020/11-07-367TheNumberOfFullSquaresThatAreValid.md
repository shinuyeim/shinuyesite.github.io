---
title: 完全有效的平方数
date: 2020-11-07
tags:
 - 简单
 - 力扣
 - 二分搜索
categories:
 - 算法笔记
---

## 题目描述
给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。  
说明：不要使用任何内置的库函数，如  sqrt。

## 示例
::: tip      
输入：16  
输出：True  

输入：14  
输出：False  
:::

## 算法设计
> + 1.若 num < 2，返回 true。  
> + 2.设置左边界为 2，右边界为 num/2。  
> + 3.当 left <= right：  
  > +   令 x = (left + right) / 2 作为一个猜测，计算 guess_squared = x * x 与 num 做比较：  
    > + 如果 guess_squared == num，则 num 是一个完全平方数，返回 true。  
    > + 如果 guess_squared > num ，设置右边界 right = x-1。  
    > + 否则设置左边界为 left = x+1。  
> + 如果在循环体内没有找到，则说明 num 不是完全平方数，返回 false。  


### 代码
最后的结果为：
```c
bool isPerfectSquare(int num){
    if (num < 2) {
      return true;
    }

    long left = 2, right = num / 2, x, guessSquared;
    while (left <= right) {
      x = left + (right - left) / 2;
      guessSquared = x * x;
      if (guessSquared == num) {
        return true;
      }
      if (guessSquared > num) {
        right = x - 1;
      } else {
        left = x + 1;
      }
    }
    return false;
}
```

### 复杂性分析
时间复杂度：O(logN)。
空间复杂度：O(1)。
