---
title: Union Find
category: Blog
tags:
  - DSA
  - Union Find
---

## Union Find



### [765. (H) couples holding hands](https://leetcode.com/problems/couples-holding-hands/description/)
```
There are n couples sitting in 2n seats arranged in a row and want to hold hands.

The people and seats are represented by an integer array row where row[i] is the ID of the person sitting in the ith seat. The couples are numbered in order, the first couple being (0, 1), the second couple being (2, 3), and so on with the last couple being (2n - 2, 2n - 1).

Return the minimum number of swaps so that every couple is sitting side by side. A swap consists of choosing any two people, then they stand up and switch seats.
```


### [839. (H) similar string groups](https://leetcode.com/problems/similar-string-groups/description/)
```
Two strings, X and Y, are considered similar if either they are identical or we can make them equivalent by swapping at most two letters (in distinct positions) within the string X.

For example, "tars" and "rats" are similar (swapping at positions 0 and 2), and "rats" and "arts" are similar, but "star" is not similar to "tars", "rats", or "arts".

Together, these form two connected groups by similarity: {"tars", "rats", "arts"} and {"star"}.  Notice that "tars" and "arts" are in the same group even though they are not similar.  Formally, each group is such that a word is in the group if and only if it is similar to at least one other word in the group.

We are given a list strs of strings where every string in strs is an anagram of every other string in strs. How many groups are there?
```



### [200. (M) number of Islands]()

### [947. (M) most stones removed with same row or column]()

### [2092. (H) find all people with secret]()


### [2421. (H) number of good paths]()


### [1697. (H) checking existance of edge length limited paths](https://leetcode.com/problems/checking-existence-of-edge-length-limited-paths/)
```
An undirected graph of n nodes is defined by edgeList, where edgeList[i] = [ui, vi, disi] denotes an edge between nodes ui and vi with distance disi. Note that there may be multiple edges between two nodes.

Given an array queries, where queries[j] = [pj, qj, limitj], your task is to determine for each queries[j] whether there is a path between pj and qj such that each edge on the path has a distance strictly less than limitj .

Return a boolean array answer, where answer.length == queries.length and the jth value of answer is true if there is a path for queries[j] is true, and false otherwise.

```
  
### [721. (M) Accounts Merge](https://leetcode.com/problems/accounts-merge/description/)
```
Given a list of accounts where each element accounts[i] is a list of strings, where the first element accounts[i][0] is a name, and the rest of the elements are emails representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails in sorted order. The accounts themselves can be returned in any order.
```
