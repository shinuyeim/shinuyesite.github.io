---
title: 有效的括号
date: 2020-08-01
tags:
 - 简单
 - 力扣
categories:
 - 算法笔记
---

## 有效的括号

给定一个只包括 [^'('],[^')'],[^'{'],[^'}'],[^'['],[^']'] 的字符串，判断字符串是否有效。

有效字符串需满足：

>1.左括号必须用相同类型的右括号闭合。  
2.左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。


## 示例1：
>输入: "()"  
输出: true

## 示例2：
>输入: "()[]{}"  
输出: true

## 示例3：
>输入: "(]"  
输出: false

## 示例4：
>输入: "([)]"  
输出: false

## 示例5：
>输入: "{[]}"  
输出: true

## 代码
```java
class Solution {
    public boolean isValid(String s) {
        if (s.length() == 0 || s == null) return true;
        if (s.length() % 2 != 0 ) return false;
        Map<Character,Character> map = new HashMap<>();
        map.put(')','(');
        map.put(']','[');
        map.put('}','{');
        Deque<Character> brackets = new ArrayDeque<>();
        for(char c: s.toCharArray()){
            if(c=='(' || c=='[' || c=='{'){
               brackets.push(c); 
            }else{
                if(brackets.size()==0 ||map.get(c)!= brackets.pop())
                return false;
            }
        }
        return brackets.size()==0;
    }
}
```

## 说明

### HashMap的基本用法

#### 创建HashMap对象

>Map<Character,Character> map = new HashMap<>();

#### 添加键值对

添加元素时，如果key已经存在，则返回旧value，并将新的value存到该key中；如果key不存在，则返回null

>1.hashMap.put("aa",1);  
>2.hashMap.put("bb",2);  
>3.hashMap.put("cc",3);  


