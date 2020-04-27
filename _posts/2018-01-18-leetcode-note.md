---
layout: post
title:  "leetcode-note"
date:   2018-01-18 18:30:00
categories: 前端
tags: JavaScript 算法
---

* content
{:toc}

在这里归纳总结做过的一些算法题以及有趣的js题目




### 找出变位映射

给定两个A和B的列表，B是A的一个字母组。B是A的一个字母组，意味着B是通过随机化A中元素的顺序而制成的。
我们希望找到一个从A到B的索引映射P.映射P [i] = j意味着A中的第i个元素出现在索引为j的B中。
这些列表A和B可能包含重复项。如果有多个答案，则输出它们中的任何一个。
ex: 
```
A = [12, 28, 46, 32, 50]
B = [50, 12, 32, 46, 28]
```
We should return
```
[1, 4, 3, 2, 0]
```
解:
```javascript
/**
 * @param {number[]} A
 * @param {number[]} B
 * @return {number[]}
 */
var anagramMappings = function (A, B) {
    let res = [ ];
    res.length = A.length;
    let m = {};
    for (let i = 0; i < B.length; i++) {
        m[B[i]] = i;
    }
    for (let i in A) {
        res[i] = m[A[i]];
    }
    return res;
};
```
更优解: 
```javascript
var anagramMappings = function(A, B) {
    var r = [];
    A.forEach(item => r.push(B.indexOf(item)));
    return r;
};
```
**思路：最后利用对象存储数值和下标，匹配A中的数字来解决。查看solution发现使用forEach可以快速解决问题。**

### 使(a == 1 && a == 2 && a == 3)为true

解:
```javascript
const a = {
    i: 1,
    valueOf: function () {
        return a.i ++;
    }
}
if (a == 1 && a == 2 && a == 3) {
    console.log('yes');
}
```
**思路： 因为判断中使用的是“==”，当两个参数类型不同时会先进行类型转换。在上面的代码中，左边为对象右边为数字，在比较==两边的数据时，会先调用左边对象的valueOf方法将a进行转换，这里重写了对象a的valueOf方法实现每次调用都返回上一次加一的值。但实际开发基本不会使用==，且ts的应用也时隐式转换的出现场景变的更少了。**

### 打印从1到最大的n位数

输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

示例：
```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```
说明：
* 用返回一个整数列表来代替打印
* n 为正整数

解:
```javascript
/**
 * @param {number} n
 * @return {number[]}
 */
var printNumbers = function(n) {
    let res = [];
    let max = 10 ** n - 1;
    for (let i = 1; i <= max; i ++ ) {
        res.push(i);
    }
    return res;
};
```
更优解:
```javascript
/**
 * @param {number} n
 * @return {number[]}
 */
var printNumbers = function(n) {
    let max = 1;
    let x = 10;
    while (n) {
        if (n & 1) {
            max = max * x;
        }
        x = x * x;
        n = n >> 1;
    }

    const res = [];
    for (let i = 1; i < max; ++i) {
        res.push(i);
    }
    return res;
};
```
**思路：考察的是乘幂的优化，只需要对 10 的 n 次方进行快速计算即可。可以直接调用内置函数Math.pow或者使用\*\*运算,从时间复杂上更优的方式是采用位运算。**