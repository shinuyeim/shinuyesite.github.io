---
title: 回文数
date: 2020-07-26
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---


## 回文数

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。


### 示例1：
>输入：121  
输出：true

### 示例2：
>输入：-121  
输出：false  
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

### 示例3：
>输入：10  
输出：false  
解释: 从右向左读, 为 01 。因此它不是一个回文数。


### 代码
```java
class Solution {
    public boolean isPalindrome(int x) {

        if(x<0){    //TODO:最后一位数字是零也可以排除
            return false;
        }

        String s = x+"";
        int mid =s.length()/2 , i = 1;

        if(length()%2 ==1){
            while(mid-i>-1&& s.charAt(mid-i) == s.charAt(mid+i))
                i++;
        }

        if(length()%2 ==0){
            while(mid-i>-1&&s.charAt(mid+i-1) == s.charAt(mid-i))
                i++;
        }
        if(mid-i == -1) return true;
         return false;

    }
}
```

