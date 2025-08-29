# Executor

## Executor interface
An interface that represents an object that executes provided tasks; used for decoupling task submission from mechanisms of how task will be ran (e.g. in the same thread? in new thread?)  
  
Example - current thread
```java
Executor currentThreadExecutor = new Executor() {
    @Override
    public void execute(Runnable command) {
        command.run();
    }
};
currentThreadExecutor.execute(() -> System.out.println(Thread.currentThread())); // Thread[main,5,main]

```
Example - new thread
```java
Executor newThreadExecutor = new Executor() {
    @Override
    public void execute(Runnable command) {
        new Thread(command).start();
    }
};
newThreadExecutor.execute(() -> System.out.println(Thread.currentThread())); // Thread[Thread-0,5,main]
```

## ExecutorService
An extension of Executor interface that provides methods to manage task termination as well as methods that return Future for tracking progress of asynchronous tasks; used with `Executors` class that provides factory methods for creating executors

### SingleThreadExecutor + Runnable example
```java
ExecutorService executorService = Executors.newSingleThreadExecutor();
Future<?> future = executorService.submit(() -> System.out.println(Thread.currentThread()));
System.out.println(future.get()); // since submitted Runnable, will be null
executorService.shutdown();



```

### SingleThreadExecutor + Callable example
```java
ExecutorService executorService = Executors.newSingleThreadExecutor();
Future<?> future = executorService.submit(Thread::currentThread);
System.out.println(future.get()); // since submitted Callable, will return String representation
                                  // of thread that executed task
executorService.shutdown();



```

### SingleThreadScheduledExecutor example
```java
ScheduledExecutorService executorService = Executors.newSingleThreadScheduledExecutor();
executorService.scheduleAtFixedRate(() -> System.out.println("Fixed rate task"), 0, 3, TimeUnit.SECONDS);



```

### FixedThreadPool example
```java
ExecutorService executorService = Executors.newFixedThreadPool(3);
for (int i = 1; i <= 3; i++) {
    Future<?> future = executorService.submit(Thread::currentThread);
    System.out.println(future.get()); // since using a thread pool with 3 threads, each iteration
                                      // will print different thread name
}
executorService.shutdown();



```

### Cached thread pool example

### Scheduled thread pool example
