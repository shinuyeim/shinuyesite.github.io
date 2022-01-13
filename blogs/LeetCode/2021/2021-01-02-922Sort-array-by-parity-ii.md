---
title: 奇偶排序数组 II  
date: 2021-01-02
tags:
 - 简单
 - 力扣
 - 排序
categories:
 - 算法笔记
---


## 题目描述
给定一个非负整数数组 A， A 中一半整数是奇数，一半整数是偶数。  

对数组进行排序，以便当 A[i] 为奇数时，i 也是奇数；当 A[i] 为偶数时， i 也是偶数。  

你可以返回任何满足上述条件的数组作为答案。   


## 示例
::: tip  
输入：[4,2,5,7]   
输出：[4,5,2,7]   
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。       
:::  

Tips:    
1. 2 <= A.length <= 20000  
2. A.length % 2 == 0  
3. 0 <= A[i] <= 1000  


## 算法设计
题目的意思就是给定一个数组，数组长度一定是偶数位，（提示里面的第二点说明）。按照数组下标的奇偶，把数组里面的元素排序。   

一种简单的方法就是循环遍历数组，把所有的偶数放进ans[0],ans[2],ans[4],以此类推。  
在遍历一遍，把所有的奇数放进ans[1],ans[3],ans[5],以此类推。  

还有一种解法就是整个数组只要遍历一次，设置两个指针，一个指针只指向奇数，一个只指向偶数。随后，在每一步中，如果 A[i] 为奇数，则不断地向前移动 j（每次移动两个单位），直到遇见下一个偶数。此时，可以直接将 A[i] 与 A[j] 交换。我们不断进行这样的过程，最终能够将所有的整数放在正确的位置上。

## 代码
两次遍历：
```c
int* sortArrayByParityII(int* A, int ASize, int* returnSize) {
    int* ans = malloc(sizeof(int) * ASize);
    int add = 0;//做偶数指针
    for (int i = 0; i < ASize; i++) {
        if (A[i] % 2 == 0) {
            ans[add] = A[i];
            add += 2;
        }
    }
    add = 1;//做奇数指针
    for (int i = 0; i < ASize; i++) {
        if (A[i] % 2 == 1) {
            ans[add] = A[i];
            add += 2;
        }
    }
    *returnSize = ASize;
    return ans;
}
```

双指针:
```c
int* sortArrayByParityII(int* A, int ASize, int* returnSize) {
    int j = 1;
    for (int i = 0; i < ASize; i += 2) {
        if (A[i] % 2 == 1) {
            while (A[j] % 2 == 1) {
                j += 2;
            }
            int temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
    }
    *returnSize = ASize;
    return A;
}
```

## 复杂度分析  
两次遍历：   
时间复杂度：O(N)，其中 N 是数组 A 的长度。   
空间复杂度：O(1)。注意在这里我们不考虑输出数组的空间占用。   

双指针：  
时间复杂度：O(N)，其中 NN 是数组 A 的长度。    
空间复杂度：O(1)。 