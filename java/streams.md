# Streams

## Parallel streams
Parallel streams utilize ForkJoinPool under the hood to achieve parallel processing  

This is not always safe, example:
``` java
List<Integer> ints = List.of(1, 2, 3, 4);

int sumSeq = ints.stream().mapToInt(i -> i)
                .peek(str -> System.out.println(Thread.currentThread())) // Thread[main,5,main]
                .reduce(5, Integer::sum); // 15 - 5 gets added once

int sumPar = ints.parallelStream().mapToInt(i -> i)
                .peek(str -> System.out.println(Thread.currentThread())) // Thread[main,5,main] or Thread[ForkJoinPool.commonPool-worker-x,5,main]
                .reduce(5, Integer::sum); // 30 - every worker thread adds 5
```
