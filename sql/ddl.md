# DDL - Data Definintion Language

## Creating a table

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
    col_name col_type [AUTO_INCREMENT]                          PRIMARY KEY, -- MySQL
    col_name col_type [GENERATED ALWAYS|BY DEFAULT AS IDENTITY] PRIMARY KEY, -- PostgreSQL
    col_name col_type REFERENCES another_table(col_name) [ON DELETE action ON UPDATE action],
    col_name col_type NOT NULL,
    col_name col_type UNIQUE,
    col_name col_type DEFAULT x,
    col_name col_type CHECK(condition),
    ...
    CONSTRAINT constraint_name PRIMARY KEY(col_name_1 [, col_name_2, ...]),
    CONSTRAINT constraint_name FOREIGN KEY(col_name) REFERENCES another_table(col_name) [ON DELETE action ON UPDATE action],
    CONSTRAINT constraint_name UNIQUE(col_name_1 [, col_name_2, ...]),
    CONSTRAINT constraint_name CHECK(condition),
    ...
);
```

## Modifying a table
```sql
ALTER TABLE table_name RENAME TO new_table_name;
                       ADD    COLUMN col_name col_type [constraints];
                       DROP   COLUMN col_name;
                       RENAME COLUMN col_name TO new_col_name;
                       ADD  CONSTRAINT constraint_name constraint_def;
                       DROP CONSTRAINT constraint_name; -- doesn't work for pkeys and fkeys in MySQL
               (MySQL) DROP PRIMARY KEY;
                            FOREIGN KEY fkey_name;
          (PostgreSQL) ALTER  COLUMN col_name DROP|SET NOT NULL;
                                              DROP|SET DEFAULT x;
                                              TYPE new_type;
               (MySQL) MODIFY COLUMN col_name new_type [NOT NULL|DEFAULT x];
                       CHANGE COLUMN col_name new_name new_type [constraints];
```

## Deleting a table
```sql
DROP TABLE [IF EXISTS] table_name;
```

## Clearing a table
```sql
TRUNCATE table_name;
```
