---
title: 统计有序矩阵中的负数
date: 2020-11-08
tags:
 - 简单
 - 力扣
 - 二分搜索
categories:
 - 算法笔记
---


## 题目描述
给你一个 m * n 的矩阵 grid，矩阵中的元素无论是按行还是按列，都以非递增顺序排列。   

请你统计并返回 grid 中 负数 的数目。

## 示例
::: tip      
输入：grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]  
输出：8  
解释：矩阵中共有 8 个负数。  
 
输入：grid = [[3,2],[1,0]]  
输出：0  

输入：grid = [[1,-1],[-1,-1]]  
输出：3  

输入：grid = [[-1]]  
输出：1  
:::


## 算法设计
注意到题目中给了一个性质，即矩阵中的元素无论是按行还是按列，都以非递增顺序排列，可以考虑把这个性质利用起来优化暴力。已知这个性质告诉了我们每一行的数都是有序的，所以我们通过二分查找可以找到每一行中从前往后的第一个负数，那么这个位置之后到这一行的末尾里所有的数必然是负数了，可以直接统计。

1.遍历矩阵的每一行。

2.二分查找到该行从前往后的第一个负数，考虑第i行，我们记这个位置为posi，那么第i行 [ posi , m-1]中的所有数都是负数，所以这一行对答案的贡献就是 m-1-posi+1 = m-posi。

### 代码(二分查找)
最后的结果为：
```c
int countNegatives(int** grid, int gridSize, int* gridColSize){
    int x = 0;
    int num = 0;
    for(int i=0;i<gridSize;i++){
        int j = 0;
        int count = 0;
        while(j<*gridColSize && grid[i][j]>=0){
            count++;
            j++;
        }
        num+=(*gridColSize-count);
    }
    return num;
}
```

### 复杂性分析(暴力法)
时间复杂度： O(log2n) 。为二分查找的时间复杂度。
空间复杂度： O(1) 。没有使用额外的空间。

### 代码(我的想法)
```c
int countNegatives(int** grid, int gridSize, int* gridColSize){
    int left = 0;
    int right = *gridColSize;
    int num = 0;
    for(int i = gridSize; i >= 0; i--){
        for(int j = *gridColSize;j >= 0; j++){
            while(j < 0 && grid[i][j] < 0){
                num = *gridColSize - j;
            }
        }
        num = num + num;
    }
    return num;
}
```

### 解释
元素都是非递增排序的，所以从每一行的后面判断，找到第一个大于等于0的数，用这一行的总长度减去这个数的位置就是这一行中负数的个数，然后一行一行的循环判断。但是给的参数限制，这个方法暂时没有成功。不过稍微改进，应该还是可以成功通过的。