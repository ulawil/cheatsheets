# Atomic variables

## Atomic operation
An operation that cannot be divided into smaller steps and does not have intermediate steps that can be observed by other threads; example:
```java
int a = 1; // atomic; just write to a

a++; // not atomic; can be broken down into
     // 1) read a
     // 2) add 1 to value
     // 3) write back to a
```

## Atomic variables in java
- Make use of instruction like compare-and-swap (CAS) to allow for atomic updates
- Are a non-blocking alternative to using regular types inside synchronized blocks
- Also provide the visibility like `volatile` keyword

Examples:
- `AtomicInteger`
- `AtomicLong`
- `AtomicBoolean`
- `AtomicReference`

## `AtomicInteger`
```java
AtomicInteger ai = new AtomicInteger(0);
ai.incrementAndGet(); // atomic increment, return value after
ai.getAndIncrement(); // atomic increment, return value before
ai.set(4); // write value directly to main memory (equivalent to writing to volatile variable)
ai.get();  // read value directly from main memory (equivalent to reading a volatile variable)
```
