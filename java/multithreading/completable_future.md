# CompletableFuture
CompletableFuture - an API for handling steps of asynchronous computations

## Submitting and processing a task
```java
CompletableFuture.supplyAsync(() -> getNameFromApiById(1)) // provide Supplier to submit a task
                .thenApply(name -> "Hi " + name + " :)")   // provide Function to process result
                .thenAccept(System.out::println)           // provide Consumer to do something with result
                .get();                                    // block thread to get result
```

## Combining sequential futures
Using `thenCompose()`:
```java
CompletableFuture.supplyAsync(() -> getNameFromApiById(1))
                .thenCompose(prev -> CompletableFuture.supplyAsync(() -> prev + " and " + getNameFromApiById(2)))
                .thenApply(name -> "Hi " + name + " :)")
                .thenAccept(System.out::println)
                .get();
```
Using `thenCombine()`:
```java
CompletableFuture.supplyAsync(() -> getNameFromApiById(1))
                .thenCombine(CompletableFuture.supplyAsync(
                        () -> getNameFromApiById(2)), (n1, n2) -> n1 + " and " + n2)
                .thenApply(name -> "Hi " + name + " :)")
                .thenAccept(System.out::println)
                .get();
```

## Running futures in parallel
Using `allOf()`:
```java
CompletableFuture<Void> futureAll = 
                CompletableFuture.allOf(future1, future2, future3); // waits for all 3 to complete
futureAll.get(); // since void, can't get individual results from this
```
Using `join()`:
```java
List<String> names = Stream.of(future1, future2, future3)
                .map(CompletableFuture::join) // here get would need exception handling
                .toList(); // can get results
```

## Exception handling
```java
CompletableFuture.supplyAsync(() -> getNameFromApiById(-1))
                .handle((str, thr) -> str == null ? "Stranger" : str)
                .thenApply(name -> "Hi " + name + " :)")
                .thenAccept(System.out::println)
                .get();
```
