---
title: GCD and LCM
categoy:
  - Blog
tags:
  - DSA
---

```java
public static int gcd(int a, int b) {
  return b == 0? a : gcd(b, a % b);
}

public static int lcm(int a, int b) {
  return (int) a / gcd(a, b) * b;
}
```
