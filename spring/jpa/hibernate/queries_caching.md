# Queries caching

## Enabling query caching
```yml
spring:
  jpa:
    properties:
      hibernate:
        cache:
          use_second_level_cache: true
          use_query_cache: true
```

## Making query cachable
```java
List<PlayerEntity> result = session.createQuery(..., PlayerEntity.class)
    .setCacheable(true)
    .getResultList();
```
Query results are cached in form of lists of primary keys, so for any real performance gain, entities need to be in 2nd level cache:
```java
@Entity
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class PlayerEntity {
    ...
}
```

## Restrictions
- Don't cache queries for frequently changing entities
- Don't cache queries with many parameters (each combinations of params = 1 more cache entry)

## Best practices
- Use with 2nd level cache
