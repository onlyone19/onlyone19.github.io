---
title: Java Memory Model
category: Blog
tags:
  - java
---

## Internal Java Memory Model
![](https://jenkov.com/images/java-concurrency/java-memory-model-2.png)

## Hardware Memory Architecture
![](https://jenkov.com/images/java-concurrency/java-memory-model-4.png)

## Bridging The Gap Between The Java Memory Model And The Hardware Memory Architecture
![](https://jenkov.com/images/java-concurrency/java-memory-model-5.png)

## Happens Before Guarantee
The Java happens before guarantee is a set of rules that govern how the Java VM and CPU is allowed to reorder instructions 
for performance gains. The happens before guarantee makes it possible for threads to rely on when a variable value is 
synchronized to or from main memory, and which other variables have been synchronized at the same time. The Java happens 
before guarantee are centered around access to volatile variables and variables accessed from within synchronized blocks. 

[Happens-before Rules specified in Java Memory Model](https://medium.com/@gathilaharism/happens-before-rules-specified-in-java-memory-model-734ab400170f)

1. Program order rule: Each action in a thread happens-before every action in that thread that comes later in the program.
   This rule ensures that the execution order of actions within a single thread is preserved, maintaining a sequential consistency
  that is essential for the correct behaviour of multithreaded programs.
2. Monitor lock rule: An unlock on a monitor lock happens-before every sub-sequent lock on the same monitor lock. Results
   of all the actions that happened before releasing the lock are visible to the thread that acquired the lock.
3. Volatile variable rule: A write to a volatile field happens-before every subsequent read of that same field.
  This rule ensures that changes made by one thread to a volatile variable are visible to other threads that subsequently read the variable.
4. Thread start rule: A call to the Thread.start happens-before every action in the started thread.
  In practical terms, if you have some shared data that is going to be accessed or modified by the newly started thread, you can rely
  on the happens-before relationship to ensure that any changes made by the main thread before calling Thread.start are visible
  to the new thread. This helps in avoiding potential data inconsistency issues in multithreaded programs.
5. Thread termination rule: if one thread sees that another thread has terminated (using the thread.isAlive() method or the thread
   joining the main thread), then all the actions in the terminated thread happen-before the termination.
  This rule ensures that the effects of the actions performed by a thread are visible to other threads even after the thread
  has terminated, preventing any potential data inconsistencies due to premature thread termination.
6. Interruption Rule: The Interruption Rule in the Java Memory Model (JMM) specifies that when a thread calls interrupt on
   another thread, it happens-before the interrupted thread detects the interrupt. This ensures proper coordination
   between the interrupting and interrupted threads, preventing issues such as delayed or missed interruption.
  The Interruption Rule establishes a happens-before relationship to ensure the orderly coordination of thread interruption,
  preventing race conditions and ensuring that the interrupted thread promptly detects the interrupt signal. This also
  ensures that actions in the interrupting thread that occurred before the call to interrupt are visible to the interrupted thread.
7. Finalizer rule: The end of a constructor for an object happens-before the start of the finalizer for that object.
  The finalizer is a special method in Java that can be defined in a class and is executed by the garbage collector before
  reclaiming the memory occupied by an object. The start of the finalizer for an object happens-after the end of the
  constructor for that object.
8. Transitivity: If action A happens-before action B, and action B happens-before action C, then it follows that action A
   happens-before action C.

   
## Instruction Reordering

## `volatile` is Not Always Enough
Even if the volatile keyword guarantees that all reads of a volatile variable are read directly from main memory, and all writes to 
a volatile variable are written directly to main memory, there are still situations where it is not enough to declare a variable volatile. 

 In the situation explained earlier where only Thread 1 writes to the shared counter variable, declaring the counter variable volatile is 
 enough to make sure that Thread 2 always sees the latest written value.

In fact, multiple threads could even be writing to a shared volatile variable, and still have the correct value stored in main memory,
if the new value written to the variable does not depend on its previous value. In other words, if a thread writing a value to the 
shared volatile variable does not first need to read its value to figure out its next value. 

```
if two threads are both reading and writing to a shared variable, then using the volatile keyword for that is not enough.You need to
use a synchronized in that case to guarantee that the reading and writing of the variable is atomic. Reading or writing a volatile
variable does not block threads reading or writing. For this to happen you must use the synchronized keyword around critical sections.

 As an alternative to a synchronized block you could also use one of the many atomic data types found in the java.util.concurrent package.
For instance, the AtomicLong or AtomicReference or one of the others.

In case only one thread reads and writes the value of a volatile variable and other threads only read the variable, then the reading
threads are guaranteed to see the latest value written to the volatile variable. Without making the variable volatile, this would
not be guaranteed.

The volatile keyword is guaranteed to work on 32 bit and 64 variables. 
```


## False Sharing in Java
False sharing in Java occurs when two threads running on two different CPUs write to two different variables which happen to be 
stored within the same CPU cache line. When the first thread modifies one of the variables - the whole CPU cache line is 
invalidated in the CPU caches of the other CPU where the other thread is running. This means, that the other CPUs need to 
reload the content of the invalidated cache line - even if they don't really need the variable that was modified within that cache line. 
