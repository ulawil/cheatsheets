# Fetch modes

## FetchMode.SELECT
```java
@OneToMany
@Fetch(FetchMode.SELECT)
private List<CardImage> cardImages;
```
- default mode for FetchType.LAZY 
- executes 1 SELECT for parents + n SELECTs for each parent's associations (n + 1 problem)

## FetchMode.JOIN
```java
@OneToMany
@Fetch(FetchMode.JOIN)
private List<CardImage> cardImages;
```
- default mode for FetchType.EAGER
- executes 1 JOIN query to fetch parent + associations

⚠️⚠️⚠️
- may fail for multi-entity loads - Hibernate falls back to SELECT mode to avoid cartesian product for a large number of entities and associations
- pagination technically works, but is memory consuming (join prevents usage of LIMIT + OFFSEt so Hibernate performs in-memory pagination)

## FetchMode.SUBSELECT
```java
@OneToMany
@Fetch(FetchMode.SUBSELECT)
private List<CardImage> cardImages;
```
- executes 2 queries - 1 SELECT for parents + 1 SELECT with subquery for associations by parent ids
- works with both FetchType.LAZY and FetchType.EAGER - overrides default mode

⚠️⚠️⚠️
- only works for collections - causes error when used with `@OneToOne` or `@ManyToOne`
- breaks pagination - only a page of entities gets loaded into the context, but the 2nd query tries fetching all other entities' associations by ids which triggers selects

---

‼️Hibernate-specific (not in JPA, will only be used if Hibernate is the implementation provider)
