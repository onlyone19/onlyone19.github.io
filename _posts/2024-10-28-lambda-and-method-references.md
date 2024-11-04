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

## Functional Interface
### 1. @FunctionalInterface

### 2. Common Standard Functional Interface
[java.util.function](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html)
  
```java
interface Function<T, R> {
    R apply(T value);
}

interface Consumer<T> {
    void accept(T value);
}

interface Supplier<T> {
    T get();
}

interface Predicate<T> {
    boolean test(T value);
}

interface UnaryOperator<T> {
    T apply(T value);
}
```

```java
interface BiFuntion<T, U, R> {
    R apply(T v1, U v2);
}

interface BiConsumer<T, U> {
    void accept(T v1, U v2);
}

interface BiPredicate<T, U> {
    boolean test(T v1, U v2);
}

interface BinaryOperator<T> {
    T apply(T v1, T v2);
}
```

### 3. Composition
```
default <V> Function<T,V>   andThen(Function<? super R,? extends V> after)
                            Returns a composed function that first applies this function to its input, and then applies
                            the after function to the result.
default <V> Function<V,R>   compose(Function<? super V,? extends T> before)
                            Returns a composed function that first applies the before function to its input, and then
                            applies this function to the result.
static <T> Function<T,T> 	  identity()
                            Returns a function that always returns its input argument.
```

```
default Predicate<T> 	    and(Predicate<? super T> other)
                          Returns a composed predicate that represents a short-circuiting logical AND of this predicate and another.
static <T> Predicate<T> 	isEqual(Object targetRef)
                          Returns a predicate that tests if two arguments are equal according to Objects.equals(Object, Object).
default Predicate<T> 	    negate()
                          Returns a predicate that represents the logical negation of this predicate.
default Predicate<T> 	    or(Predicate<? super T> other)
                          Returns a composed predicate that represents a short-circuiting logical OR of this predicate and another.
```
