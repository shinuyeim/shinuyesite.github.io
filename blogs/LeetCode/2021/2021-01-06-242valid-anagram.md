---
title: 有效的字母异位词
date: 2021-01-06
tags:
 - 简单
 - 力扣
 - 哈希表
categories:
 - 算法笔记
---


## 题目描述
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。   

## 示例
::: tip  
输入: s = "anagram", t = "nagaram"  
输出: true  

输入: s = "rat", t = "car"  
输出: false  
:::  

Tips:      
1. 假设字符串只包含小写字母。  


## 算法设计
题目的意思就是给定两个字符串，然后判断两个字符串里面的字母以及他们出现的次数是否相等，很简单的一个办法就是将数组排序，然后比较内容是否一样。如果两个字符串的长度都不等的话，直接返回false。

此题也可以用O(n)的时间复杂度完成，我们遍历一遍数组，然后统计每一个数组出现的频次，然后比较也可以等处答案。  
由于字符串只包含 26 个小写字母，因此我们可以维护一个长度为 26 的频次数组 table，先遍历记录字符串 s 中字符出现的频次，然后遍历字符串 t，减去 table 中对应的频次，如果出现 table[i]<0，则说明 t 包含一个不在 s 中的额外字符，返回 false 即可。


## 代码
排序
```c
int cmp(const void* _a, const void* _b) {
    char a = *(char*)_a, b = *(char*)_b;
    return a - b;
}

bool isAnagram(char* s, char* t) {
    int len_s = strlen(s), len_t = strlen(t);
    if (len_s != len_t) {
        return false;
    }
    qsort(s, len_s, sizeof(char), cmp);
    qsort(t, len_t, sizeof(char), cmp);
    return strcmp(s, t) == 0;
}
```

strcmp函数是string compare(字符串比较)的缩写，用于比较两个字符串并根据比较结果返回整数。基本形式为strcmp(str1,str2)，若str1=str2，则返回零；若str1 < str2，则返回负数；若str1>str2，则返回正数。

哈希表
```c
bool isAnagram(char* s, char* t) {
    int len_s = strlen(s), len_t = strlen(t);
    if (len_s != len_t) {
        return false;
    }
    int table[26];
    memset(table, 0, sizeof(table));
    for (int i = 0; i < len_s; ++i) {
        table[s[i] - 'a']++;
    }
    for (int i = 0; i < len_t; ++i) {
        table[t[i] - 'a']--;
        if (table[t[i] - 'a'] < 0) {
            return false;
        }
    }
    return true;
}

```

## 复杂度分析     
排序：
时间复杂度：O(nlogn)，其中 n 为 s 的长度。排序的时间复杂度为 O(nlogn)，比较两个字符串是否相等时间复杂度为 O(n)，因此总体时间复杂度为 O(n log n + n) = O(nlogn)。

哈希表：
时间复杂度：O(n)，其中 n 为 s 的长度。

