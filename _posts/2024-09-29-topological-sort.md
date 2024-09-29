---
title: Topological Sort
category: Blog
tags:
  - DSA
  - Graph
  - Topological Sort
---

## 建图的三种方式
1. 邻接矩阵（适合点的数量不多的图）
2. 邻接表（最常用的方式）
3. 链式前向星（空间要求严苛情况下使用。比赛必用，大厂笔试、面试不常用）


## Topological Sort
要求：有向图、没有环

拓扑排序的顺序可能不只一种。拓扑排序也可以用来判断有没有环。
1. 在图中找到所有入度为0的点
2. 把所有入度为0的点在图中删掉，重点是删掉影响！继续找到入度为0的点并删掉影响
3. 直到所有点都被删掉，依次删除的顺序就是正确的拓扑排序结果
4. 如果无法把所有的点都删掉，说明有向图里有环

### [210. (M) Course Schedule II](https://leetcode.com/problems/course-schedule-ii/description/)
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an 
array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

    For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. 
If it is impossible to finish all courses, return an empty array.

### [字典序最小的拓扑排序](https://www.luogu.com.cn/problem/U107394)


### [269. Alien Dictionary](https://leetcode.com/problems/alien-dictionary/description/)
There is a new alien language which uses the latin alphabet. However, the order among letters are 
unknown to you. You receive a list of words from the dictionary, where words are sorted 
lexicographically by the rules of this new language. Derive the order of letters in this language.


### [936. (H) Stamping The Sequence](https://leetcode.com/problems/stamping-the-sequence/description/)
You are given two strings stamp and target. Initially, there is a string s of length target.length with all s[i] == '?'.

In one turn, you can place stamp over s and replace every letter in the s with the corresponding letter from stamp.

    For example, if stamp = "abc" and target = "abcba", then s is "?????" initially. In one turn you can:
        place stamp at index 0 of s to obtain "abc??",
        place stamp at index 1 of s to obtain "?abc?", or
        place stamp at index 2 of s to obtain "??abc".
    Note that stamp must be fully contained in the boundaries of s in order to stamp (i.e., you cannot place stamp at index 3 of s).

We want to convert s to target using at most 10 * target.length turns.

Return an array of the index of the left-most letter being stamped at each turn. If we cannot obtain target from s 
within 10 * target.length turns, return an empty array.

## 拓扑排序的扩展技巧
重要技巧：利用拓扑排序的过程，上游节点逐渐推送消息给下游节点的技巧. 这个技巧已经是树型dp的内容了

### [P4017 最大食物链计数](https://www.luogu.com.cn/problem/P4017)
给你一个食物网，你要求出这个食物网中最大食物链的数量。

（这里的“最大食物链”，指的是生物学意义上的食物链，即最左端是不会捕食其他生物的生产者，最右端是不会被其他生物捕食的消费者。）

Delia 非常急，所以你只有 11 秒的时间。

由于这个结果可能过大，你只需要输出总数模上 8011200280112002 的结果。


### [851. (M) Loud and Rich](https://leetcode.com/problems/loud-and-rich/description/)
There is a group of n people labeled from 0 to n - 1 where each person has a different amount of money and a 
different level of quietness.

You are given an array richer where richer[i] = [ai, bi] indicates that ai has more money than bi and an 
integer array quiet where quiet[i] is the quietness of the ith person. All the given data in richer are 
logically correct (i.e., the data will not lead you to a situation where x is richer than y and y is 
richer than x at the same time).

Return an integer array answer where answer[x] = y if y is the least quiet person (that is, the person y 
with the smallest value of quiet[y]) among all people who definitely have equal to or more money than the person x.



### [2050. (H) Parallel Courses III](https://leetcode.com/problems/parallel-courses-iii/description/)
You are given an integer n, which indicates that there are n courses labeled from 1 to n. You are also given a 
2D integer array relations where relations[j] = [prevCoursej, nextCoursej] denotes that course prevCoursej has 
to be completed before course nextCoursej (prerequisite relationship). Furthermore, you are given a 0-indexed 
integer array time where time[i] denotes how many months it takes to complete the (i+1)th course.

You must find the minimum number of months needed to complete all the courses following these rules:

    You may start taking a course at any time if the prerequisites are met.
    Any number of courses can be taken at the same time.

Return the minimum number of months needed to complete all the courses.

Note: The test cases are generated such that it is possible to complete every course (i.e., the graph is a directed acyclic graph).


### [2127. (H) Maximum Employees to Be Invited to a Meeting](https://leetcode.com/problems/maximum-employees-to-be-invited-to-a-meeting)
A company is organizing a meeting and has a list of n employees, waiting to be invited. They have arranged for a large 
circular table, capable of seating any number of employees.

The employees are numbered from 0 to n - 1. Each employee has a favorite person and they will attend the meeting only 
if they can sit next to their favorite person at the table. The favorite person of an employee is not themself.

Given a 0-indexed integer array favorite, where favorite[i] denotes the favorite person of the ith employee, return 
the maximum number of employees that can be invited to the meeting.


### ???[1494. (H) Parallel Courses II](https://leetcode.com/problems/parallel-courses-ii/description/)
You are given an integer n, which indicates that there are n courses labeled from 1 to n. You are also given an array 
relations where relations[i] = [prevCoursei, nextCoursei], representing a prerequisite relationship between course 
prevCoursei and course nextCoursei: course prevCoursei has to be taken before course nextCoursei. Also, you are given the integer k.

In one semester, you can take at most k courses as long as you have taken all the prerequisites in the previous semesters
for the courses you are taking.

Return the minimum number of semesters needed to take all courses. The testcases will be generated such that it is 
possible to take every course.

