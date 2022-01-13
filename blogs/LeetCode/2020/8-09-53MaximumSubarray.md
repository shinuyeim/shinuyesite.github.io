---
title: 最大子序和
date: 2020-08-09
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---


## 最大子序和

给定一个整数数组 [^nums] ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

## 示例1：
>输入: [-2,1,-3,4,-1,2,1,-5,4]  
输出: 6  
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。  

## 代码
```java
class Solution {
   public int maxSubArray(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    int max = nums[0];
    dp[0] = nums[0];
    for (int i = 1; i < n; i++) {
        if (dp[i - 1] < 0) {
            dp[i] = nums[i];
        } else {
            dp[i] = dp[i - 1] + nums[i];
        }
        max = Math.max(max, dp[i]);
    }
    return max;
    }
}
```

### 说明
当输入数组只有一个元素的时候,上述解法不成立,需要加入判断条件,if(nums.length==1) return nums[0];

