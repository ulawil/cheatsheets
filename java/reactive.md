# Reactive Streams (Project Reactor, RxJava)

## Creating a Reactive Stream.

## Basic intermediate and terminal operation.
Intermediate operations - transform the stream (modify, filter, combine) and do not trigger execution of the stream
- `map`
- `filter`
- `flatMap` - transforms elements asynchronously into publishers and flattens them into 1 flux (bc it's asynchronous, order may not be preserved)
- `concatMap` - similar to flatMap but preserves order
- `flatMapMany` - transforms item in Mono into publisher and returns a Flux with it
- `transform` - allows for combining multiple transforming operations (e.g.g map + filter)

Terminal operations - operations that trigger execution of the stream
- subscribe
