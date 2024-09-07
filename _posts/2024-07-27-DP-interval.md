---
title: Dynamic Programming - Interval
category: Blog
tags:
  - DSA
  - DP
---


## 区间动态规划：
```
线性 DP 的一种，简称为「区间 DP」。以「区间长度」划分阶段，以两个坐标（区间的左、右端点）作为状态的维度。一个状态通常由被它包含且比它更小的区间状态转移而来。
```

区间 DP 的主要思想就是：先在小区间内得到最优解，再利用小区间的最优解合并，从而得到大区间的最优解，最终得到整个区间的最优解。

根据小区间向大区间转移情况的不同，常见的区间 DP 问题可以分为两种：

1. 单个区间从中间向两侧更大区间转移的区间 DP 问题。比如从区间 [i+1,j−1][i+1,j−1] 转移到更大区间 [i,j][i,j]。
2. 多个（大于等于 22 个）小区间转移到大区间的区间 DP 问题。比如从区间 [i,k][i,k] 和区间 [k,j][k,j] 转移到区间 [i,j][i,j]。

## 区间 DP 问题的基本思路
### 1.2.1 第 1 种区间 DP 问题基本思路

从中间向两侧转移的区间 DP 问题的状态转移方程一般为：
`dp[i][j]=max{dp[i+1][j−1],dp[i+1][j],dp[i][j−1]}+cost[i][j],i≤jdp[i][j]=max{dp[i+1][j−1],dp[i+1][j],dp[i][j−1]}+cost[i][j],i≤j`。

1. 其中 dp[i][j]dp[i][j] 表示为：区间 [i,j][i,j]（即下标位置 ii 到下标位置 jj 上所有元素）上的最大价值。
2. costcost 表示为：从小区间转移到区间 [i,j][i,j] 的代价。
3. 这里的 max/minmax/min 取决于题目是求最大值还是求最小值。

从中间向两侧转移的区间 DP 问题的基本解题思路如下：

  1. 枚举区间的起点；
  2. 枚举区间的终点；
  3. 根据状态转移方程计算从小区间转移到更大区间后的最优值。

### 1.2.3 第 2 种区间 DP 问题基本思路
多个（大于等于 22 个）小区间转移到大区间的区间 DP 问题的状态转移方程一般为：
`dp[i][j]=max/min{dp[i][k]+dp[k+1][j]+cost[i][j]},i<k≤jdp[i][j]=max/min{dp[i][k]+dp[k+1][j]+cost[i][j]},i<k≤j`。

1. 其中状态 dp[i][j]dp[i][j] 表示为：区间 [i,j][i,j] （即下标位置 ii 到下标位置 jj 上所有元素）上的最大价值。
2. cost[i][j]cost[i][j] 表示为：将两个区间 [i,k][i,k] 与 [k+1,j][k+1,j] 中的元素合并为区间 [i,j][i,j] 中的元素的代价。
3. 这里的 max/minmax/min 取决于题目是求最大值还是求最小值。

多个小区间转移到大区间的区间 DP 问题的基本解题思路如下：

1. 枚举区间长度；
2. 枚举区间的起点，根据区间起点和区间长度得出区间终点；
3. 枚举区间的分割点，根据状态转移方程计算合并区间后的最优值。

对应代码如下：


区间dp：大范围的问题拆分成若干小范围的问题来求解

---------------------------------------------------------------------------------------------
可能性展开的常见方式：
1）基于两侧端点讨论的可能性展开
2）基于范围上划分点的可能性展开

- [5. (M) Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)
- [516. (M) Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/description/)
- [1216. (H) Valid Palindrome III](https://leetcode.com/problems/valid-palindrome-iii/description/)

-----------------------------------------------------------------------------------------

- [1312. (H) Minimum Insertion Steps to Make a String Palindrome](https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome)
- [486. (M) Predict the Winner](https://leetcode.com/problems/predict-the-winner/description/)
- [1039. (M) Minimum Score Triangulation of Polygon](https://leetcode.com/problems/minimum-score-triangulation-of-polygon/description/)
- [1547. (H) Minimum Cost to Cut a Stick](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/description/)
- [312. (H) Burst Balloons](https://leetcode.com/problems/burst-balloons/description/)
- [(M) boolean evaluation](https://leetcode.cn/problems/boolean-evaluation-lcci/description/)
  Given a boolean expression consisting of the symbols 0 (false), 1 (true), & (AND), | (OR), and ^ (XOR), and a desired boolean result value result, implement a function to count the number of ways of parenthesizing the expression such that it evaluates to result.
  ```
  Example 1:
  Input: s = "1^0|0|1", result = 0
  Output: 2
  Explanation: Two possible parenthesizing ways are:
  1^(0|(0|1))
  1^((0|0)|1)

  Example 2:
  Input: s = "0&0&0&1^1|0", result = 1
  Output: 10
  ```
- [括号区间匹配](https://www.nowcoder.com/practice/e391767d80d942d29e6095a935a5b96b)
  ```
  给定一个由 '[' ，']'，'('，‘)’ 组成的字符串，请问最少插入多少个括号就能使这个字符串的所有括号左右配对。
  例如当前串是 "([[])"，那么插入一个']'即可满足。
  
  数据范围：字符串长度满足 
  1  ≤  n  ≤  100
  ```

--------------------------------------------------------------------------------------------

- [664. (H) Strange Printer](https://leetcode.com/problems/strange-printer/description/)
- [P3205 [HNOI2010] 合唱队](https://www.luogu.com.cn/problem/P3205)
- [546. (H) Remove Boxes](https://leetcode.com/problems/remove-boxes/description/)
- [1000. (H)  Minimum Cost to Merge Stones](https://leetcode.com/problems/minimum-cost-to-merge-stones/description/)
- [730. Count Different Palindromic Subsequences](https://leetcode.com/problems/count-different-palindromic-subsequences/)
  key word is "different". thre are maybe multiple subsequence "aaa" for example


----------------------------------------------------------------------------------------------

- [1278. (H) Palindrome Partitioning III](https://leetcode.com/problems/palindrome-partitioning-iii/description/)
- [813. (M) Largest Sum of Averages](https://leetcode.com/problems/largest-sum-of-averages/description/)
- [410. (H) Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/description/)
- [1335. (H) Minimum Difficulty of a Job Schedule](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/)
  
