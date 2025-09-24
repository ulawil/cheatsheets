# Cache levels

## 1st level
- Session-scoped (entities loaded into persistence context)
- implementation provided by HIbernate
- enabled by default and cannot be disabled

## 2nd level
- SessionFactory-scoped
- implementation not provided by hibernate, requires external provider, e.g. EHCache
- enabled/disabled through application.yml

```yml
spring:
  jpa:
    properties:
      hibernate:
        cache:
          use_second_level_cache=true
```
```java
@Entity
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class TeamEntity {
    ...

    @OneToMany
    @JoinColumn(name = "team_id")
    @Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
    private List<PlayerEntity> players;
}
```
```java
@Entity
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class PlayerEntity {
    ...
}
```
