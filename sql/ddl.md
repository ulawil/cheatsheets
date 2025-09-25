# DDL - Data Definintion Language

## Creating a table

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
    col_name col_type [AUTO_INCREMENT] PRIMARY KEY, -- MySQL
    col_name col_type [GENERATED ALWAYS/BY DEFAULT AS IDENTITY] PRIMARY KEY , -- PostgreSQL
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

## Altering a table
```sql
ALTER TABLE table_name ADD COLUMN col_name TYPE <contraints/options.
```

## Dropping a table

### Truncating a table
`TRUNCATE` - will delete all table rows