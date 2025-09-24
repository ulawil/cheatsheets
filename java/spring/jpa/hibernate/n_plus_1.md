# N + 1 problem

## Solution #1: JPQL + JOIN FETCH
```java
@Query("SELECT c from Card c JOIN FETCH c.cardImages ce")
List<Card> findAllWithImages();
```
- Number of queries: 1
- Pagination: technically works, but is memory consuming (join prevents usage of LIMIT + OFFSET so Hibernate performs in-memory pagination)

## Solution #2: Batch size
```java
@OneToMany
@BatchSize(size = 100)
private List<CardImage> cardImages;
```
Or set default value for all associations:
```yml
spring:
  jpa:
    properties:
      hibernate:
        default_batch_fetch_size: 100
```
- Number of queries: 1 + n/batch_size  
- Pagination: works

## Solution #3: FetchMode.SUBSELECT
```java
@OneToMany
@Fetch(FetchMode.SUBSELECT)
private List<CardImage> cardImages;
```
- Number of queries: 2
- Pagination: breaks (only a page of root entities loaded into context, SUBSELECT tries to fetch all others which causes n selects)
