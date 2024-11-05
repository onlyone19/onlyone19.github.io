---
title: Java Streams
category: Blog
tags:
  - java
---

## 1. Obtain Streams
- list.stream()
- Arrays.stream(myarray)
- Stream.of("a", "b", "c")
- Stream.ofNullable()
- Steam.empty()
- new Random().ints(1, 7)
- file.lines()
- Stream.generate(Supplier)
- Stream.iterate(BigInteger.ONE, n -> n.multiply(BigInteger.TWO));
- Stream.iterate('A', letter -> letter <= 'Z', letter ->(char)(letter + 1));

## 2. Filtering and Transforming
- filter
- distinct
- map
- flatMap

## 3. Searching
- find a particular element: `filter` + `findFirst`, `findAny`
- check if elements exist: `anyMatch`, `allMatch`, `noMatch`

## 4. Reducing and Collecting
- forEach
- collect(Collectors.toList())
- collect(Collectors.join(", ")


## Reducing Streams in Detail
- `Optional<T> 	reduce​(BinaryOperator<T> accumulator)`
- `T 	reduce​(T identity, BinaryOperator<T> accumulator)`
- `<U> U 	reduce​(U identity, BiFunction<U,​? super T,​U> accumulator, BinaryOperator<U> combiner)`

  in this version, the return type is different from the element type.

  Many reductions using this form can be represented more simply by an explicit combination of map and reduce operations.
  The accumulator function acts as a fused mapper and accumulator, which can sometimes be more efficient than separate
  mapping and reduction, such as when knowing the previously reduced value allows you to avoid some computation.

## Collecting Streams in Detail
- Collection is `Mutable` reduction. A collection opration reduces a stream into a mutable result container.
- `<R> R collect​(Supplier<R> supplier, BiConsumer<R,​? super T> accumulator, BiConsumer<R,​R> combiner)`
  - Supplier -> creates a new mutable result container
  - Accumlator -> an associative, non-interfering, stateless function that must fold an element into a result container.
  - Combinator -> an associative, non-interfering, stateless function that accepts two partial result containers and merges
    them, which must be compatible with the accumulator function. The combiner function must fold the elements from the
    second result container into the first result container.


## Collectors
- toList
- toSet
- toMap
```java
Map<Category, BigDecimal> totalPerCategory = products.stream()
   .collect(Collectors.toMap(
            Product::getCategory, // keyMappingFunction,
            Product::getPrice,    // valueMappingFunction,
            BigDecimal::add       // MergeFunctionforSamekey
  ));
```

## Grouping
1. Map<Category, List<Product>> productsByCategory = products.stream().collect(
         Collectors.groupingBy(Product::getCategory));
2. Map<Category, List<String>> productNameByCategory = products.stream().collect(
         Collectors.groupingBy(Product::getCategory, Collectors.mapping(Product::getName, Collectors.toList())
   );
   // key -> a Collector implementing the downstream reduction


## Partitioning


## Examples???


    
