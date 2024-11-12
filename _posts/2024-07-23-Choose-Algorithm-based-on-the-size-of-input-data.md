---
title: Master公式 and Choose Algorithm Based On The Size of Input Data
category: Blog
tags:
  - DSA
  - Math
---

## Master 
5. master公式
    a. 所有子问题规模相同的递归才能用master公式，T(n) = a * T(n/b) + O(n^c)，a、b、c都是常数
    b. 如果log(b,a)  < c，复杂度为：O(n^c)
    c. 如果log(b,a)  > c，复杂度为：O(n^log(b,a))
    d. 如果log(b,a) == c，复杂度为：O(n^c * logn)
6. 一个补充
    T(n) = 2*T(n/2) + O(n*logn)，时间复杂度是O(n * ((logn)的平方))，证明过程比较复杂，记住即可

## Choose Algorithm Based On The Size of Input Data
- n <= 11 => O(n!)
- n <= 25 => O(2^n)
- n <= 5,000 => O(n^2)
- n <= 10^6 => O(nlogn)
- n <= 10^7 => O(n)
- n >= 10^8 => O(logN)



- [906. Super Palindromes](https://leetcode.com/problems/super-palindromes/description/)
- [消灭怪物](https://www.nowcoder.com/practice/d88ef50f8dab4850be8cd4b95514bbbd)
