## Fetch types

### EAGER
```java
fetch = FetchType.EAGER
```
- parent entity's associations are fetched at the same time as the parent entity
- default fetch type for `@OneToOne` and `@ManyToOne` relationships

### LAZY
```java
fetch = FetchType.LAZY
```
- parent entity's associations are fetched on-demand when they're accessed, e.g. when using their getter
- default fetch type for `@OneToMany` and `@ManyToMany` relationships
