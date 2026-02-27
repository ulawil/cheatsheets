# Reactive Streams (Project Reactor, RxJava)

## Creating a Reactive Stream

Creating a Flux:
- `Flux.just`
- `Flux.fromArray`
- `Flux.fromIterable`
- `Flux.fromStream`
- `Flux.from(publisher) // can be Mono or FLux`

Creating a Mono:
- `Mono.just`
- `Mono.justOrEmpty`
- `Mono.from(publisher) // can be Mono or Flux but if Flux will be created from 1st element?`
- `Mono.fromCallable`
- `Mono.fromRunnable`
- `Mono.fromFuture(completableFuture)`

## Basic intermediate and terminal operations
**Intermediate operations** - operations that do not trigger stream execution (basically anything that isn't `subscribe()` or doesn't call it internally)
- `map` >! like in streams
- `filter` - like in streams
- `transform` - allows for combining multiple operations on Mono/Flux into 1 method (e.g. filter + map)
- `flatMap` - use instead of map if the result of element transformation is another flux/mono; eagerly subscribes to all inner fluxes so elements may overlap
- `flatMapMany` - use instead of flatMap if transforming element inside Mono into a Flux
- `concatMap` - similar to flatMap but preserves element order by waiting for one inner flux to complete before subscribing to another one
- `concat`, `concatWith` - combines multiple monos/fluxes into one flux; does not cause element overlap by waiting for one publisher to complete before subscribing to the next one 
- `merge`, `MergeWith` - combines multiple monos/fluxes into one flux; may cause element overlap by subscribing to all publishers eagerly
- `mergeSequential` - combines multiple monos/fluxes into one flux; subscribes to all publishers eagerly but does not cause element overlap by caching (?)
- `zip`, `zipWith` - combines multiple monos/fluxes into a flux of tuples; waits for all sources to emit 1 element, puts elements into a tuple, then waits for another element
- `defaultIfEmpty` - provides a default value if a mono/flux is completed without any data
- `switchIfEmpty` - switches to an alternate publisher if a mono/flux is completed without any data
- `repeat` - repeatedly and indefinitely subscribes to the source when previous subscription completed
- `repeat(n)` - repeatedly subscribes to the source fixed number of times

**Terminal operations** - operations trigger execution of the stream (`subscribe()` and anything that calls it internally)
- `subscribe` - subscribes to the streamm triggering the data flow
- `block // for Mono` - blocks the thread waiting for the stream to complete and returns value; terminal because it subscribes internally
- `blockFirst // for FLux`
- `blockLast // for Flux`

## Exception handling

Exception handling by recovering from exception (catch exception and take action):
- `onErrorReturn` - catches the exception and provides a default fallback value
- `onErrorResume` - catches the exception and subscribes to a fallback publisher
- `onErrorContinue` - catches the exception, drops the element that caused it and continues the stream

Exception handling by taking action and rethrowing:
- `onErrorMap` - catches the exception, maps it into another type and throws
- `doOnError` - catches the exception, performs an action that does not modify the stream and re-throws it

Retrying the stream:
- `retry` - in case of error, re-subscribes to the stream indefinitely
- `retry(n)` - in case of error, re-subscribes to the stream fixed number of times
- `retryWhen(retrySpec)` - conditionally retries in case of specific errors

## Best Practices

## Understanding the difference between Java Stream API and Reactive Streaming

**Java Stream API** - used for processing collections of data, replaces large for loops with nested ifs with functional-style processing

**Reactive Streaming** - used for creating non-blocking, asynchronous APIs instead of traditional thread-per-request APIs

## Understanding operations: zip, defer, combineLatest, etc.

- `combineLatest` - creates a flux whose elements are the latest published elements from each source combined
- `defer(supplier)` - lazily provides a publisher every time a the subscription happens (when we want to do something that provides the publisher, e.g. call external service every time the subscription is made?)

## Project Reactor: Understanding the difference between Flux and Mono and converting them to each other

**Mono** - an implementation of Publisher that emits 0-1 elements

**FLux** - an implementation of Publisher that emits 0-n elements

Converting Mono to Flux:
- `Flux.from(mono)`
- `mono.flux()`

Converting FLux to Mono:
- `Mono.from(flux)` - creates Mono with 1st element of fLux
- `flux.next()` - creates Mono with 1st element of fLux
- `flux.last()` - creates Mono with last element of fLux
- `flux.collectList()`
- `flux.reduce()`

## RxJava: Understanding the difference between Observable, Flowable, Maybe, Single, and converting them to each other




