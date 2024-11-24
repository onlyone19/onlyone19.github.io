---
title: Binary and Bitwise Operations
category: Blog
tags:
  - leetcode
  - DSA
---

## Signed Binary
### Negative Number -> Binary
- `abs(negative number) - 1`, then reverse. For example, -7 - > 7 -1 -> 0111 - 1 = 0110 -> then reverse = 1001
  
### Binary -> Negative Number
- reverse + 1, then add sign

### Print Binary
```java
@Test
public void binaryprint() {
    int value = -7;

    // uses two's complement
    assertEquals("11111111111111111111111111111001", Integer.toBinaryString(value));
    // with sign
    assertEquals("-111", Integer.toString(value, 2));
}
```


### 常见的位运算（|、&、^、~、<<、>>、>>>）

### 相反数 ( `-A = ~A + 1` )
```java
@Test
public void additiveInverse() {
    int v = -7;
    int r = ~v + 1;
    // 相反数 = reverse + 1
    assertEquals(7, r);

    v = Integer.MIN_VALUE;
    r = ~v + 1;
    // MIN_VALUE的相反数 = MIN_VALUE
    assertEquals(v, r);

    r = Math.abs(v);
    // 取绝对值还是自己
    assertEquals(v, r);
}
```


## XOR

### 异或运算性质
1. 异或运算就是无进位相加
2. 异或运算满足交换律、结合律，也就是同一批数字，不管异或顺序是什么，最终的结果都是一个
3. `0^n=n`，`n^n=0`
4. 整体异或和如果是x，整体中某个部分的异或和如果是y，那么剩下部分的异或和是x^y

### 袋子里一共a个白球，b个黑球，每次从袋子里拿2个球，每个球每次被拿出机会均等
如果拿出的是2个白球、或者2个黑球，那么就往袋子里重新放入1个白球
如果拿出的是1个白球和1个黑球，那么就往袋子里重新放入1个黑球
那么最终袋子里一定会只剩1个球，请问最终的球是黑的概率是多少？用a和b来表达这个概率。

### 题目1 交换两个数
```java
@Test
public void swapTwoNumbers() {
    int a = 10;
    int b = -123;

    a = a ^ b;
    b = a ^ b;
    a = a ^ b;

    assertEquals(10, b);
    assertEquals(-123, a);
}
```

### 题目2 不用任何判断语句和比较操作，返回两个数的最大值
```java
@Test
public void maxOfTowNumbers() {
    int a = 20;
    int b = 10;
    assertEquals(a, max(a, b));

    a = 10;
    b = 20;
    assertEquals(b, max(a, b));

    a = 10;
    b = -20;
    assertEquals(a, max(a, b));

    a = -10;
    b = 20;
    assertEquals(b, max(a, b));

    a = Integer.MIN_VALUE;
    b = -10;
    assertEquals(b, max(a, b));

    a = Integer.MAX_VALUE;
    b = Integer.MIN_VALUE;
    assertEquals(a, max(a, b));
}

public static int max(int a, int b) {
    int c = a - b;
    int signC = sign(c);

    int signA = sign(a);
    int signB = sign(b);

    int diffSign = signA ^ signB;
    int sameSign = flip(diffSign);

    // return a if a and b has same sign and a - b >=0 || diff sign and a >= 0
    int returnA = diffSign * signA + sameSign * signC;
    int returnB = flip(returnA);

    return a * returnA + b * returnB;
}

// return 1 if v == 0; return 0 if v == 1
public static int flip(int v) {
    return v ^ 1;
}

// return 0 if v < 0; return 1 if v >= 0;
public static int sign(int v) {
    return flip(v >>> 31);
}
```


### [leetcode 268 Missing Number](https://leetcode.com/problems/missing-number)
```java
public int missingNumber(int[] nums) {
    int all = 0;
    int has = 0;
    for(int i = 0; i < nums.length; ++i) {
        all ^= i;
        has ^= nums[i];
    }
    all ^= nums.length;

    return all ^ has;
}
```


### [236: Single Number](https://leetcode.com/problems/single-number)

### [137. Single Number II](https://leetcode.com/problems/single-number-ii)
- Given an integer array `nums` where every element appears `three times` except for one, which appears `exactly once`. 
Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.
- **数组中只有1种数出现次数少于m次，其他数都出现了m次，返回出现次数小于m次的那种数**

### [260. Single Number III](https://leetcode.com/problems/single-number-iii) 
数组中有2种数出现了奇数次，其他的数都出现了偶数次，返回这2种出现了奇数次的数
- **Brian Kernighan算法 - 提取出二进制状态中最右侧的1** => `n & -n` => `n & (~n + 1)`
```java
public int[] singleNumber(int[] nums) {
    int all = 0;
    for(int num : nums) {
        all ^= num;
    }
    // all = a ^ b
    // a and b has different value at bit mostRightOne
    // this bit can split the arrays into 2 groups
    // the group has only a OR b
    int mostRightOne = all & (-all);
    int num1 = 0;
    for(int num : nums) {
        if((num & mostRightOne) == 0) {
            num1 ^= num;
        }
    } 
    System.out.println(mostRightOne);

    return new int[] {num1, all ^ num1};
}
```




