---
title: Lambda and Method References
category: Blo
tags: 
  - Java
---

## Lambda Express
- Lambda express is an anonymous method.
- Lambda express implements a functional interface.
- syntax of Lambda expressions: parameters -> body
- captured a local variable should be effectively `final`
- avoid side effect in lambda expressions
- `this` and `super` have the same meaning as in surrounding code, which is different from anonymous classes.
- dealing with `exception` can be inconvenient. match the definition of functioanl interface

## Method References
- Classname :: methodName  (static method)
- objectRef :: mehtodName  (instance method of a specific object)
- ClassName :: methodName  (instance method not of a specific object)
- ClassName :: new         (constructor)  
