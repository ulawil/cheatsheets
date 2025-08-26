# Window functions

## Aggregate example
```sql
SELECT name, attribute, atk, AVG(atk) OVER(PARTITION BY attribute) FROM card;
```
- unlike GROUP BY, does not collapse rows - can display both individual and aggregated value
