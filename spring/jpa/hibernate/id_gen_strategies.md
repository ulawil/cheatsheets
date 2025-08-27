# Id generation strategies

## GenerationType.AUTO
```java
@Id
@GeneratedValue(strategy = GenerationType.AUTO)
private Long id;
```
- allows persistence provider to choose the strategy based on the PK type

## GenerationType.IDENTITY
```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
- for auto-incremented ids (e.g. `AUTO_INCREMENT` in MySQL)
- does not allow for batch inserts or `TABLE_PER_CLASS` inheritance mapping


## GenerationType.SEQUENCE
```java
@Id
@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "cardImageSeqGen")
@SequenceGenerator(
    name = "cardImageSeqGen",
    sequenceName = "card_image_id_seq",
    allocationSize = 1
)
private Long id;
```
- for ids that use values from a sequence (e.g. `SERIAL`/`BIGSERIAl` in PostgreSQL)

## GenerationType.TABLE
```java
@Id
@GeneratedValue(strategy = GenerationType.TABLE, generator = "paintingTableGen")
@TableGenerator(
    name = "paintingTableGen",
    table = "id_generator",
    pkColumnName = "gen_key",
    valueColumnName = "gen_value",
    allocationSize = 1
)
private Long id;
```
- for ids that use values from a table

## GenerationType.UUID
