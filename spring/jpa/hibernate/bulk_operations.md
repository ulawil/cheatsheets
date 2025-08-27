# Bulk operations

## Batch insert/update/delete
```yml
spring:
  jpa:
    properties:
      hibernate:
        jdbc:
          batch_size: ?
```
⚠️ Bulk insert doesn't work with IDENTITY id generation strategy (because Hibernate can't generate ids in batches); use SEQUENCE or TABLE strategy

### Ordering inserts/updates
A batch can only contain 1 type of entity; to batch insert/update multiple entity types properly they need to be ordered; configured by setting:
```yml
spring:
  jpa:
    properties:
      hibernate:
        order_inserts: true
        order_updates: true
```

## Batch fetch
Configure batch fetching entities associations with:
```yml
spring:
  jpa:
    properties:
      hibernate:
        default_batch_fetch_size: ?
```
Or at collection level:
```java
@OneToMany
@BatchSize(size = 100)
private List<CardImage> cardImages;
```
