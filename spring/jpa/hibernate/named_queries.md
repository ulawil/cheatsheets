# Named queries
A way to organize queries related to an entity in one place in the code (when not using JPA repositories)
```java
@Entity
@org.hibernate.annotations.NamedQueries({
        @org.hibernate.annotations.NamedQuery(name = "findAuthorById", query = "SELECT a FROM AuthorEntity a WHERE a.id = :authorId"),
        @org.hibernate.annotations.NamedQuery(name = "findAuthorByName", query = "SELECT a FROM AuthorEntity a WHERE a.name = :authorName"),
        @org.hibernate.annotations.NamedQuery(name = "findAuthorByMangaName", query = "SELECT a FROM AuthorEntity a JOIN a.manga m WHERE m.name = :mangaName")
})
@org.hibernate.annotations.NamedNativeQueries({
        @org.hibernate.annotations.NamedNativeQuery(name = "findAuthorByNameNative", query = "SELECT * FROM author WHERE author.name = :authorName")
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
