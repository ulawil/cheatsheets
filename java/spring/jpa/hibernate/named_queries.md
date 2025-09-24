# Named queries
A way to organize queries related to an entity in one place in the code (when not using JPA repositories)
```java
@Entity
@NamedQueries({
        @NamedQuery(name = "findAuthorById", query = "SELECT a FROM AuthorEntity a WHERE a.id = :authorId"),
        @NamedQuery(name = "findAuthorByName", query = "SELECT a FROM AuthorEntity a WHERE a.name = :authorName"),
        @NamedQuery(name = "findAuthorByMangaName", query = "SELECT a FROM AuthorEntity a JOIN a.manga m WHERE m.name = :mangaName")
})
@NamedNativeQueries({
        @NamedNativeQuery(name = "findAuthorByNameNative", query = "SELECT * FROM author WHERE author.name = :authorName")
})
public class AuthorEntity {
  ...
}
```
Usage:
```java
List<AuthorEntity> result = session.createNamedQuery("findAuthorByName", AuthorEntity.class)
    .setParameter("authorName", "Masashi Kishimoto")
    .getResultList();
```
```java
List<AuthorEntity> result = session.createNamedQuery("findAuthorByNameNative", AuthorEntity.class)
    .setParameter("authorName", "Tite Kubo")
    .getResultList();
```
