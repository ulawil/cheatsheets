# Threads basics

## Thread states
`NEW` - thread has not started yet  

`RUNNABLE` - thread is executing in JVM (includes waiting for OS resources)

`BLOCKED` - thread is waiting to acquire a monitor lock so it can enter a synchronized block

`WAITING` - thread is waiting for another thread to perform some action:

- calling `notify()` or `notifyAll` if it called `wait()` with no timeout
- terminate if it called `join` with no timeout

`TIMED_WAITING` - like `WAITING` but if the methods were called with timeout
- also includes `Thread.sleep()`

`TERMINATED` - the thread has finished execution

## Thread.start()
Causes the thread to begin execution - under the hood JVM calls run() method in a new thread  
:warning: throws `IllegalThreadStateException` when called more than once on the same thread

## Thread.run()
The method to override when creating a thread; contains the code the thread needs to execute; is called by the JVM once the thread is started  
:warning: Should not be called to start the thread - will only cause the execution of the Runnable **in the same thread**

## Thread.join()
Makes the calling thread wait until the referenced thread dies:
```java
public static void main(String[] args) {
    Thread thread = new Thread(() -> ..., "thread_1");
    thread.start();
    thread.join(); // calling thread (main) will now wait for the referenced thread (thread_1)
                   // to finish execution and die
    ...
```
With timeout:
```java
public static void main(String[] args) {
    Thread thread = new Thread(() -> ..., "thread_1");
    thread.start();
    thread.join(1000); // main thread will wait for thread_1 for 1 second before resuming
    ...
```

## Thread.sleep()
Makes the thread go idle for a specified period of time (no CPU used)

## Thread properties to set
- `name`
- `priority` - can influence scheduling
- `daemon` - makes the thread a daemon (a thread JVM does not wait for before finishing execution)

## Object.wait()
Makes the current thread that holds the object's monitor release the monitor and wait until it's awakened by:
- another object calling notify() on that object
- another object calling notifyAll() on that object
- thread being interrupted

As opposed to busy waiting (when a thread continuously checks for some condition inside a loop), `wait()` does not waste CPU cycles
## Object.notify()
Wakes up one of the threads waiting for the object's monitor (thread is chosen arbitrarily); the awakened thread still needs the calling thread to release the monitor

## Object.notifyAll()
Wakes up all threads waiting for the object's monitor

## Wait & notify example - producer-consumer pattern
Producer:
```java
while(data_to_produce) {
    synchronized(lock) {
        while(data_not_consumed) { // while instead of if protects against spurious wake up
            lock.wait();
        }
        produce_data();
        lock.notify();
    }
}
```

Consumer:
```java
while(data_to_consume) {
    synchronized(lock) {
        while(data_not_produced) { // while instead of if protects against spurious wake up
            lock.wait();
        }
        consume_data();
        lock.notify();
    }
}
```

## synchronized keyword
Makes it so only 1 thread at a time can execute marked code; can be used on:
- instance methods
- static methods
- code blocks
```java
public synchronized void synchronizedInstanceMethodExample() {
    // instance the method was called on (e.g. new SynchronizeExample()) serves as the monitor object
}
```
```java
public static synchronized void synchronizedStaticMethodExample() {
    // class object (e.g. SynchronizeExample.class) serves as the monitor object
}
```
```java
public void synchronizedInstanceCodeBlockExample() {
    synchronized (this) { // this = instance of SynchronizeExample
      ...
    }
}
```
```java
final Object lock = new Object(); // final bc we want all threads to synchronize on the same object
...
public void synchronizedLockCodeBlockExample() {
    synchronized (lock) {
      ...
    }
}
```
```java
public static void synchronizedStaticCodeBlockExample() {
    synchronized (SynchronizeExample.class) {
      ...
    }
}
```

## volatile keyword
In order to ensure any updates to variable are visible to all threads at any given time, makes the JVM bypass some optimization mechanisms when reading/writing to the variable:
- avoid reordering instructions related to volatile variable
- avoid reading/writing to thread cache, instead reading/writing to main memory directly  

:warning: Only use by itself for simple flag/state checks - for atomic operations use synchronized or atomic types  
- No need to combine with `synchronized` (it already provides visibility) unless implementing double-checked locking for lazy singletons
