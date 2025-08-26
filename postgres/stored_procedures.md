# Stored procedures

## Creating a stored procedure
```sql
CREATE OR REPLACE PROCEDURE add_card_to_faves(
    IN arg_user_id BIGINT,
    IN arg_card_id BIGINT
)
LANGUAGE plpgsql
AS $$
BEGIN
    INSERT INTO user_fave_card(user_id, card_id) VALUES(arg_user_id, arg_card_id);
    UPDATE card SET faves = faves + 1 WHERE id=arg_card_id;
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
