# Reactive Streams (Project Reactor, RxJava)

## Creating a Reactive Stream.

## Basic intermediate and terminal operations
Intermediate operations - transform the stream (modify, filter, combine) and do not trigger execution of the stream
- `map` - like in streams
- `filter` - like in streams
- `transform` - allows for combining multiple operations on Mono/Flux into 1 method (e.g. filter + map)
---
- `flatMap` - use instead of map if the result of element transformation is another flux/mono; eagerly subscribes to all inner fluxes so element order may not be preserved
- `flatMapMany` - use instead of flatMap if transforming element inside Mono into a Flux
- `concatMap` - similar to flatMap but preserves element order by waiting for one inner flux to complete before subscribing to another one
---
- `concat` - static method for combining multiple monos/fluxes into one flux with order preserved by waiting for one publisher to complete emitting before subscribing to the next one 
- `concatWith` - non-static equivalent of concat
- `merge` - similar to concat but does not preserve order due to all publishers being subscribed to eagerily
- `MergeWith` non-static equivalent of merge
- `mergeSequential` - combines concat and merge; all publishers are subscribed to eagerily but order is preserved (more memory usage tho due to caching?)
- `zip` - static method for combining multiple monos/fluxes into a flux of tuples by waiting for all sources to emit 1 element, putting them into a tuple, then subscribing to another
- `zipWith` - non-static equivalent of zip
---
- `defaultIfEmpty` - provides a default value if a mono/flux is completed without any data
- `switchIfEmpty` - switches to an alternate publisher if a mono/flux is completed without any data (flux -> mono v, mono -> flux x)

Terminal operations - operations that trigger execution of the stream
- `subscribe`

Callbacks - 

## Exception handling

### Exception handling by recovering from exception (catch exception and take action)
- `onErrorReturn` - catches the exception and provides a default fallback value
```java
.onErrorReturn("fallback value")
```
- `onErrorResume` - catches the exception and subscribes to a fallback publisher
```java
.onErrorResume(e -> {
    log.error("exception: ", e);
    return Flux.just("recovery flux e1", "recovery flux e2");
})
```
- `onErrorContinue` - catches the exception, drops the element that caused it and continues the stream
```java
.onErrorContinue((e, obj) -> log.error("exception for obj {}: {})", obj, e.getMessage()))
```

### Exception handling by taking action and rethrowing
- `onErrorMap` - catches the exception, maps it into another type and throws
```java
.onErrorMap(e -> new IllegalStateException(e.getMessage()))
```

- `doOnError` - catches the exception, performs an action that does not modify the stream and throws
```java
.doOnError(e -> log.error("exception: ", e))
```

## Best Practices

## Understanding the difference between Java Stream API and Reactive Streaming

Java Stream API:
- uses threads

Reactive Streaming:
- uses events

## Understanding operations: zip, defer, combineLatest, etc.

## Project Reactor: Understanding the difference between Flux and Mono and converting them to each other

## RxJava: Understanding the difference between Observable, Flowable, Maybe, Single, and converting them to each other




