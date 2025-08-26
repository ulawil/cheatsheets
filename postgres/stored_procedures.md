# Stored procedures

## Creating a stored procedure
```sql
CREATE OR REPLACE PROCEDURE add_card_to_faves(
    IN p_user_id BIGINT,
    IN p_card_id BIGINT
)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO user_fave_card(user_id, card_id) VALUES(p_user_id, p_card_id);
    UPDATE card SET faves = faves + 1 WHERE id=p_card_id;
END;
$$;
```
- for REPLACE to work args have to be the same

## Calling a stored procedure
```sql
CALL add_card_to_faves(1, 68396121);
```

## Deleting a stored procedure
```sql
DROP PROCEDURE add_card_to_faves(BIGINT, BIGINT);
```
