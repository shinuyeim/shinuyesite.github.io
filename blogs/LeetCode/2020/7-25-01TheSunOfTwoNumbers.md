---
title: 两数之和
date: 2020-07-25
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 两数之和


给定一个整数数组 [^nums] 和一个目标值 [^target]，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
 

### 示例：
>给定 nums = [2, 7, 11, 15], target = 9  
因为 nums[0] + nums[1] = 2 + 7 = 9  
所以返回 [0, 1]  



### 代码
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int[] a = new int[2];
        for (int i = 0; i < numbers.length - 1; i++){

            for (int j = i + 1; j < numbers.length; j++ ){

                if (numbers[i] + numbers[j] == target){

                    a[0] = i ;
                    a[1] = j ;
                    break;
                }
            }
        }
        return a;
    }
}
```

