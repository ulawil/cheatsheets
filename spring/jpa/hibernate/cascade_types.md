# Cascade types

Setting cascade type:
```java
@OneToMany(cascade = ?)
private List<CardImage> cardImages;
```

Possible cascade types:
- `CascadeType.ALL`
- `CascadeType.PERSIST`
- `CascadeType.MERGE`
- `CascadeType.DETACH`
- `CascadeType.REMOVE`
- `CascadeType.REFRESH`
