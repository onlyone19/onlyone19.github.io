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

## Bit Operations
### [231. Power of Two](https://leetcode.com/problems/power-of-two)
```java
public boolean isPowerOfTwo(int n) {
    // n-1: flips all the bits in n after the rightmost set bit (the least significant bit that is 1) and also flips that bit to 0.
    // n & (n-1): clears the rightmost set bit of n while keeping all other bits unchanged.
    return n > 0 && (n & (n-1)) == 0;
}

boolean isPowerOfTwo3(int n) {
    // extract right most 1
    return n > 0 && n == (n & -n);
}

boolean isPowerOfTwo2(int n) {
    int count = 0;
    while(n > 0) {
        if((n & 1) == 1) ++count;
        n = n >> 1;
    }

    return count == 1;
}
```

### [326. Power of Three](https://leetcode.com/problems/power-of-three)


### [201. Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range)
```java
public int rangeBitwiseAnd(int left, int right) {
    int rt = 0;
    for(int i = 0; i < 32; ++i) {
        if( left == right ) {
            rt = left << i;
            break;
        }
        left = left >>> 1;
        right = right >>> 1;
    }

    return rt;
}
```

### [190. Reverse Bits](https://leetcode.com/problems/reverse-bits)


### [461. Hamming Distance](https://leetcode.com/problems/hamming-distance)

### [477. Total Hamming Distance](https://leetcode.com/problems/total-hamming-distance)

### [3141. Maximum Hamming Distances](https://leetcode.com/problems/maximum-hamming-distances)



## 位运算实现加减乘除，过程中不能出现任何算术运算符

## 加法：利用每一步无进位相加的结果 + 进位的结果不停计算，直到进位消失
```java
public static int add(int a, int b) {
  int ans = a;
  while (b != 0) {
    // ans : a和b无进位相加的结果
    ans = a ^ b;
    // b : a和b相加时的进位信息
    b = (a & b) << 1;
    a = ans;
  }
  return ans;
}
```


### 减法：利用加法，和一个数字x相反数就是(~x)+1
```java
public static int minus(int a, int b) {
  return add(a, neg(b));
}

public static int neg(int n) {
  return add(~n, 1);
}
```


### 乘法：回想小学时候怎么学的乘法，除此之外没别的了
```java
public static int multiply(int a, int b) {
  int ans = 0;
  while (b != 0) {
    if ((b & 1) != 0) {
      // 考察b当前最右的状态！
      ans = add(ans, a);
    }
    a <<= 1;
    b >>>= 1;
  }
  return ans;
}
```

### 除法：为了防止溢出，让被除数右移，而不是除数左移。从高位尝试到低位
- [29. 两数相除](https://leetcode.com/problems/divide-two-integers/)
```java
public static int MIN = Integer.MIN_VALUE;

public static int divide(int a, int b) {
  if (a == MIN && b == MIN) {
    // a和b都是整数最小
    return 1;
  }
  if (a != MIN && b != MIN) {
    // a和b都不是整数最小，那么正常去除
    return div(a, b);
  }
  if (b == MIN) {
    // a不是整数最小，b是整数最小
    return 0;
  }
  // a是整数最小，b是-1，返回整数最大，因为题目里明确这么说了
  if (b == neg(1)) {
    return Integer.MAX_VALUE;
  }
  // a是整数最小，b不是整数最小，b也不是-1
  a = add(a, b > 0 ? b : neg(b));
  int ans = div(a, b);
  int offset = b > 0 ? neg(1) : 1;
  return add(ans, offset);
}

// 必须保证a和b都不是整数最小值，返回a除以b的结果
public static int div(int a, int b) {
  int x = a < 0 ? neg(a) : a;
  int y = b < 0 ? neg(b) : b;
  int ans = 0;
  for (int i = 30; i >= 0; i = minus(i, 1)) {
    if ((x >> i) >= y) {
      ans |= (1 << i);
      x = minus(x, y << i);
    }
  }
  return a < 0 ^ b < 0 ? neg(ans) : ans;
}
```
