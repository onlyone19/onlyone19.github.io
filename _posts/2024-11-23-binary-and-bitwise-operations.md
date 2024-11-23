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

### 相反数 ( `~A + 1` )
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
