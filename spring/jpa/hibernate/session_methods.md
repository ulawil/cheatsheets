# Session methods

## persist / save
```java
session.persist(anime);
// persists a transient entity
// doesn't guarantee immediate id assignment
// JPA specification-compliant
```
```java
Long savedId = (Long) session.save(anime);
// also persists a transient entity
// guarantees immediate id assignment and returns id
// deprecated in favor of persist()
```

## merge / update
```java
AnimeEntity animeUpdated = session.merge(anime);
// copies the state of given detached instance into a persistent instance with the same id
// JPA specification-compliant
```
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

## detach / evict
```java
session.detach(anime);
// removes instance from persistence context
// JPA specification-compliant
```
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

## remove / delete
```java
session.remove(anime);
// marks given persistent instance for removal
// JPA specification-compliant
```
```java
session.delete(anime);
// removes persistent instance from the db
// deprecated in favor of `remove()`
```

## find / get
```java
AnimeEntity anime = session.find(AnimeEntity.class, 1L);
// loads instance by id
// JPA specification-compliant
```
```java
AnimeEntity anime = session.find(AnimeEntity.class, 1L);
// loads instance by id
// similar to find()
```

## getReference / load
```java
AnimeEntity anime = session.getReference(AnimeEntity.class, 1L);
// loads instance by id who's state may be lazily fetched
// JPA specification-compliant
```
```java
AnimeEntity anime = session.getReference(AnimeEntity.class, 1L);
// loads instance by id who's state may be lazily fetched
// deprecated in favor of getReference()
```

## refresh
```java
session.refresh(anime);
// synchronizes state of given instance with the state of its correesponding table row in db
// JPA specification-compliant
```

## close
```java
session.close();
// ends session by releasin JDBC connection and cleaning up
// JPA specification-compliant
```
