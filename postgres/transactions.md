# Transactions

## Isolation levels

- `READ_UNCOMMITED`
  - dirty reads: ✅
  - non-repeatable reads: ✅
  - phantom reads: ✅

- `READ_COMMITED`
  - dirty reads: :x:
  - non-repeatable reads: ✅
  - phantom reads: ✅

- `REPEATABLE_READ`
  - dirty reads: :x:
  - non-repeatable reads: :x:
  - phantom reads: ✅
 
- `READ_SERIALIZABLE`
  - dirty reads: :x:
  - non-repeatable reads: :x:
  - phantom reads: :x:

**Dirty read** - situation in which a transaction reads a row that has been changed by another transaction before the changes have been committed (in case of rollback transaction ends up with invalid value)

**Non-repeatable read** - situation in which transaction A reads row, transaction B writes to the row, transaction A re-reads the row and gets 2 different values

**Phantom read** - a situation in which transaction A reads all rows that satisfy a WHERE clause, transaction B inserts a row that also satisfies it, transaction A re-reads all rows that satisfy it including the inserted "pahntom row"  


## Setting isolation level
In DB:
```sql
BEGIN;
SET TRANSACTION ISOLATION LEVEL ...;
...
COMMIT;
```
In Spring:
```java
@Transactional(isolation = ...)
public Cards saveAll() {
  ...
}
```
