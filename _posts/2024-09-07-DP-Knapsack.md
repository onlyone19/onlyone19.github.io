---
title: Dynamic Programming - Knapsack
category: Blog
tags:
  - DSA
  - DP
---

将原本题意的解空间(代表各种物品是否使用的高维向量),替换成了代价的解空间(是一个有上限C的标量)。压缩了复杂度。

## 0-1 Knapsack
- [01背包(模版)](https://www.luogu.com.cn/problem/P1048)
- [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/description/)
- [
- [494. Target Sum](https://leetcode.com/problems/target-sum/description/)
- [1049. Last Stone Weight II](https://leetcode.com/problems/last-stone-weight-ii/description/)
- [有依赖的背包(模版)](https://www.luogu.com.cn/problem/P1064)
  ```
  物品分为两大类：主件和附件
  主件购买没有限制，钱够就可以；附件购买有限制，该附件所归属的主件先购买，才能购买这个附件
  例如，若想买打印机或扫描仪这样的附件，必须先购买电脑这个主件。以下是一些主件及其附件的展示：
  电脑：打印机，扫描仪 | 书柜：图书 | 书桌：台灯，文具 | 工作椅：无附件
  每个主件最多有2个附件，并且附件不会再有附件，主件购买后，怎么去选择归属附件完全随意，钱够就可以
  所有的物品编号都在1~m之间，每个物品有三个信息：价格v、重要度p、归属q
  价格就是花费，价格 * 重要度 就是收益，归属就是该商品是依附于哪个编号的主件
  比如一件商品信息为[300,2,6]，花费300，收益600，该商品是6号主件商品的附件
  再比如一件商品信息[100,4,0]，花费100，收益400，该商品自身是主件(q==0)
  给定m件商品的信息，给定总钱数n，返回在不违反购买规则的情况下最大的收益
  测试链接 : https://www.luogu.com.cn/problem/P1064
  测试链接 : https://www.nowcoder.com/practice/f9c6f980eeec43ef85be20755ddbeaf4
  ```
- [474. Ones and Zeroes](https://leetcode.com/problems/ones-and-zeroes/description/)
- [879. Profitable Schemes](https://leetcode.com/problems/profitable-schemes/description/)
- [956. Tallest Billboard](https://leetcode.com/problems/tallest-billboard/description/)


## 分组背包、完全背包
- [分组背包(模版)](https://www.luogu.com.cn/problem/P1757)
- [2218. Maximum Value of K Coins From Piles](https://leetcode.com/problems/maximum-value-of-k-coins-from-piles/description/)
- [完全背包(模版)](https://www.luogu.com.cn/problem/P1616)
- [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/description/)
- [44. Wildcard Matching](https://leetcode.com/problems/wildcard-matching/description/)
- [购买足量干草的最小花费](https://www.luogu.com.cn/problem/P2918)

## 多重背包、混合背包
- [宝物筛选](https://www.luogu.com.cn/problem/P1776)
  ```
  一共有n种货物, 背包容量为t
  每种货物的价值(v[i])、重量(w[i])、数量(c[i])都给出
  请返回选择货物不超过背包容量的情况下，能得到的最大的价值
  测试链接 : https://www.luogu.com.cn/problem/P1776
  ```
  
- [观赏樱花](https://www.luogu.com.cn/problem/P1833)
  ```
  给定一个背包的容量t，一共有n种货物，并且给定每种货物的信息
  花费(cost)、价值(val)、数量(cnt)
  如果cnt == 0，代表这种货物可以无限选择
  如果cnt > 0，那么cnt代表这种货物的数量
  挑选货物的总容量在不超过t的情况下，返回能得到的最大价值
  背包容量不超过1000，每一种货物的花费都>0
  测试链接 : https://www.luogu.com.cn/problem/P1833
  ```
- [混合背包 + 多重背包普通窗口优化](http://poj.org/problem?id=1742)
  ```
  [能成功找零的钱数种类](http://poj.org/problem?id=1742)
  每一种货币都给定面值val[i]，和拥有的数量cnt[i]
  想知道目前拥有的货币，在钱数为1、2、3…m时
  能找零成功的钱数有多少
  也就是说当钱数的范围是1~m
  返回这个范围上有多少可以找零成功的钱数
  比如只有3元的货币，数量是5张
  m = 10
  那么在1~10范围上，只有钱数是3、6、9时，可以成功找零
  所以返回3表示有3种钱数可以找零成功
  测试链接 : http://poj.org/problem?id=1742
  ```


