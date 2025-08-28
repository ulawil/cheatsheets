# Producer-consumer pattern

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
