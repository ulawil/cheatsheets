# Bulk operations

```yml
spring:
  jpa:
    properties:
      hibernate:
        order_inserts=true
        order_updates=true
        default_batch_fetch_size=?
        jdbc:
          batch_size=?
```

- `jdbc.batch_size` - sets max batch size for bulk inserts/updates/deletes
- `order_inserts`, `order_updates` - a batch can only contain 1 type of entity; to insert/update multiple entity types properly, they need to be ordered by type
- `default_batch_fetch_size` - sets max batch size for fetching entity associations

</br>

- ⚠️ Bulk insert doesn't work with IDENTITY id generation strategy (because Hibernate can't generate ids in batches); use SEQUENCE or TABLE strategy

