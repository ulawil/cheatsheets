# Correlated subqueries

# Uncorrelated subquery
Find cards with atk higher than average:
```sql
SELECT name, atk FROM card WHERE atk > (SELECT AVG(atk) FROM card);

EXPLAIN ANALYZE...
Seq Scan on card  (... loops=1)
    ->  Seq Scan on card card_1  (... loops=1)
```
- inner query and qouter query are independent
- inner query is executed once

# Correlated subquery
Find cards with atk higher than average card with this card's attribute (inner query requires card from outer query)
```sql
SELECT name, atk FROM card c_outer WHERE atk > (SELECT AVG(atk) FROM card WHERE card.attribute = c_outer.attribute);

EXPLAIN ANALYZE...
Seq Scan on card c_outer  (... loops=1)
    ->  Seq Scan on card  (... loops=13868)
```
- inner query depends on fields from outer query
- inner query is executed once for each row from outer query
