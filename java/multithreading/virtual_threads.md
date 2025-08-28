# Virtual threads

## Creating a virtual thread
With Thread Class:
```java
Thread thread = Thread.ofVirtual()
    .start(() -> ...); // some runnable
```
