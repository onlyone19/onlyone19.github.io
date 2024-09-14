---
title: Dynamic Programming on Trees
category: Blog
tags:
  - DSA
  - DP
---

## DP on Trees
树型dp在树上做动态规划，依赖关系比一般动态规划简单. 因为绝大部分多数都是父依赖子. 只是依赖关系简单，不代表题目简单

树型dp套路
1. 分析父树得到答案需要子树的哪些信息
2. 把子树信息的全集定义成递归返回值
3. 通过递归让子树返回全集信息
4. 整合子树的全集信息得到父树的全集信息并返回

## [333. (M) Largest BST Substree](https://leetcode.com/problems/largest-bst-subtree/description/)
给定一个二叉树，找到其中最大的二叉搜索树（BST）子树，并返回该子树的大小. 其中，最大指的是子树节点数最多的二叉搜索树（BST）中的所有节点都具备以下属性：1. 左子树的值小于其父（根）节点的值 2. 右子树的值大于其父（根）节点的值
注意：子树必须包含其所有后代

## [1373. (H) Maximum Sum BST in Binary Tree](https://leetcode.com/problems/maximum-sum-bst-in-binary-tree/description/)
Given a binary tree root, return the maximum sum of all keys of any sub-tree which is also a Binary Search Tree (BST).

## [543. (E) Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/)
Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.
The length of a path between two nodes is represented by the number of edges between them.

## [979. (M) Distribute Coins in Binary Tree](https://leetcode.com/problems/distribute-coins-in-binary-tree/description/)
You are given the `root` of a binary tree with `n` nodes where each `node` in the tree has `node.val` coins. 
There are `n` coins in total throughout the whole tree.

In one move, we may choose two adjacent nodes and move one coin from one node to another. A move may be from parent to child, 
or from child to parent.

Return the **minimum** number of moves required to make every node have **exactly** one coin.

## [337. House Robber III](https://leetcode.com/problems/house-robber-iii/description/)
same as [P1352 没有上司的舞会](https://www.luogu.com.cn/problem/P1352)

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses 
in this place form a binary tree. It will automatically contact the police if **two directly-linked houses were broken into on the same night**.

Given the `root` of the binary tree, return the maximum amount of money the thief can rob **without alerting the police**.


## [968. (H) Binary Tree Cameras](https://leetcode.com/problems/binary-tree-cameras/description/)
You are given the root of a binary tree. We install cameras on the tree nodes where each camera at a node can monitor its parent, 
itself, and its immediate children.

Return the minimum number of cameras needed to monitor all nodes of the tree.

## [437. (M) Path Sum III](https://leetcode.com/problems/path-sum-iii/description/)
Given the root of a binary tree and an integer targetSum, return the number of paths where the sum of the values 
along the path equals targetSum.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).


## [2477. (M) Minimum Fuel Cost to Report to the Capital](https://leetcode.com/problems/minimum-fuel-cost-to-report-to-the-capital/description/)
There is a tree (i.e., a connected, undirected graph with no cycles) structure country network consisting of n cities 
numbered from 0 to n - 1 and exactly n - 1 roads. The capital city is city 0. You are given a 2D integer array roads 
where roads[i] = [ai, bi] denotes that there exists a bidirectional road connecting cities ai and bi.

There is a meeting for the representatives of each city. The meeting is in the capital city.

There is a car in each city. You are given an integer seats that indicates the number of seats in each car.

A representative can use the car in their city to travel or change the car and ride with another representative. The cost of traveling between two cities is one liter of fuel.

Return the minimum number of liters of fuel to reach the capital city.


## [2246. (H) Longest Path With Different Adjacent Characters](https://leetcode.com/problems/longest-path-with-different-adjacent-characters)
You are given a tree (i.e. a connected, undirected graph that has no cycles) rooted at node 0 consisting of n nodes numbered from 0 to n - 1. 
The tree is represented by a 0-indexed array parent of size n, where parent[i] is the parent of node i. Since node 0 is the root, parent[0] == -1.

You are also given a string s of length n, where s[i] is the character assigned to node i.

Return the length of the longest path in the tree such that no pair of adjacent nodes on the path have the same character assigned to them.


## dfn序
用深度优先遍历的方式遍历整棵树, 给每个节点依次标记序号. 编号从小到大的顺序就是dfn序

dfn序 + 每颗子树的大小，可以起到定位子树节点的作用. 如果某个节点的dfn序号是x，以这个节点为头的子树大小为y. 
那么可知，dfn序号从x ~ x+y-1所代表的节点，都属于这个节点的子树
利用这个性质，**节点间的关系判断**，**跨子树的讨论** 就会变得方便

## [2458. (H) Height of Binary Tree After Subtree Removal Queries]()
You are given the root of a binary tree with n nodes. Each node is assigned a unique value from 1 to n. 
You are also given an array queries of size m.
You have to perform m independent queries on the tree where in the ith query you do the following:
Remove the subtree rooted at the node with the value queries[i] from the tree. It is guaranteed that queries[i] will not be equal to 
the value of the root.
Return an array answer of size m where answer[i] is the height of the tree after performing the ith query.

Note:
    The queries are independent, so the tree returns to its initial state after each query.
    The height of a tree is the number of edges in the longest simple path from the root to some node in the tree.

## [2322. (H) Minimum Score After Removals on a Tree](https://leetcode.com/problems/minimum-score-after-removals-on-a-tree/description/)
There is an undirected connected tree with n nodes labeled from 0 to n - 1 and n - 1 edges.

You are given a 0-indexed integer array nums of length n where nums[i] represents the value of the ith node. You are also given 
a 2D integer array edges of length n - 1 where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the tree.

Remove two distinct edges of the tree to form three connected components. For a pair of removed edges, the following steps are defined:

    Get the XOR of all the values of the nodes for each of the three components respectively.
    The difference between the largest XOR value and the smallest XOR value is the score of the pair.

    For example, say the three components have the node values: [4,5,7], [1,9], and [3,3,3]. The three XOR values are 4 ^ 5 ^ 7 = 6, 1 ^ 9 = 8, and 3 ^ 3 ^ 3 = 3. The largest XOR value is 8 and the smallest XOR value is 3. The score is then 8 - 3 = 5.

Return the minimum score of any possible pair of edge removals on the given tree.

 





