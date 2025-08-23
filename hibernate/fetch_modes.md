## Fetch modes

### SELECT
```java
@Fetch(FetchMode.SELECT)
```
- default mode for FetchType.LAZY 
- executes 1 SELECT for parents + n SELECTs for each parent's associations (n + 1 problem)
- can be optimized with `@BatchSize(size = ...)`

### JOIN
```java
@Fetch(FetchMode.JOIN)
```
- default mode for FetchType.EAGER
- executes 1 JOIN query to fetch parent + associations


### SUBSELECT
```java
@Fetch(FetchMode.SUBSELECT)
```
- executes 2 queries - 1 SELECT for parents + 1 SUBSELECT for associations by parent ids
- works with both FetchType.LAZY and FetchType.EAGER - overrides default mode
- only works for collections - causes error when used with `@OneToOne` or `@ManyToOne`

---

‼️May not work when using JPA cause who knows what that uses under the hood (just use JPQL instead)
