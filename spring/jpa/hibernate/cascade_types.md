# Cascade types

```java
@OneToMany(cascade = ?)
private List<CardImage> cardImages;
```
- `CascadeType.ALL    ` - all operations on entity are propagated to the associations

- `CascadeType.PERSIST` - only persist operation (`entityManager.persist()`, JPA repository `save()` is propagated

- `CascadeType.MERGE  ` - only merge operation (`entityManager.merge()`, JPA repository `save()` is propagated

- `CascadeType.DETACH ` - only detach operation (`entityManager.detach()`) is propagated

- `CascadeType.REMOVE ` - only remove operation (`entityManager.remove()`, JPA repository `delete()` is propagated

- `CascadeType.REFRESH` - only refresh operation (`entityManager.refresh()`) is propagated


