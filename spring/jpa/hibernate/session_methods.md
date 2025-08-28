# Session methods

## persist
```java
session.persist(anime);
// persists a transient entity
// doesn't guarantee immediate id assignment
// JPA specification-compliant
```

## save
```java
Long savedId = (Long) session.save(anime);
// also persists a transient entity
// guarantees immediate id assignment and returns id
// deprecated in favor of persist()
```

## merge
```java
AnimeEntity animeUpdated = session.merge(anime);
// copies the state of given detached instance into a persistent instance with the same id
// JPA specification-compliant
```

## update
```java
session.update(anime);
// updates the state of persistent instance with the id of given detached instance
// deprecated in favor of merge()
```

## saveOrUpdate
```java
session.saveOrUpdate(anime)
// saves or updates instance, depending if it exists in db or not
// deprecated
```

## flush
```java
session.flush();
// synchronizes state of db with the state of persistence context
// JPA specification-compliant
```

## detach
```java
session.detach(anime);
// removes instance from persistence context
// JPA specification-compliant
```

## evict
```java
session.detach(anime);
// removes instance from persistence context
// synonym for detach()
```

## clear
```java
session.refresh(anime);
// clears persistent context by
// - detaching all entities
// - cancelling all pending operations (saves, updates, deletes...)
// JPA specification-compliant
```

## remove
```java
session.remove(anime);
// marks given persistent instance for removal
// JPA specification-compliant
```

## delete
```java
session.delete(anime);
// removes persistent instance from the db
// deprecated in favor of `remove()`
```

## find
```java
AnimeEntity anime = session.find(AnimeEntity.class, 1L);
// finds instance by id
// JPA specification-compliant
```

## refresh
```java
session.refresh(anime);
// synchronizes state of given instance with the state of its correesponding table row in db
// JPA specification-compliant
```
