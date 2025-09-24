# Inheritance mapping

## MappedSuperclass

```java
@MappedSuperclass
public class Card {
    ...
}
```
Superclass annotated with  `@MappedSuperclass` is not an entity and does not have a table associated with it in the db; instead, all tables for its subclasses will contain rows corresponding to its fields

## SINGLE_TABLE strategy
```java
@Inheritance(strategy = SINGLE_TABLE) // default strategy, can be omitted
@DiscriminatorColumn(name = "card_type", discriminatorType = DiscriminatorType.STRING)
@Entity
public class Card {
    ...
}
```
```java
@DiscriminatorValue("monster") // additional column in the table, no need to define a field for it
@Entity
public class MonsterCard extends Card {
    ...
}
```
```java
@DiscriminatorValue("spell")
@Entity
public class SpellCard extends Card {
    ...
}
```
```java
@DiscriminatorValue("trap")
@Entity
public class TrapCard extends SpellCard {
    ...
}
```
Pros:
- Best performance for polymorphic queries (no joins & union all)

Cons:
- Many nullable collumns (waste of space)

## JOINED strategy
```java
@Inheritance(strategy = JOINED)
@Entity
public class Card {
    ...
}
```
```java
@PrimaryKeyJoinColumn(name = "monster_id") // additional column in the table, primary key & foreign key to parent table
@Entity
public class MonsterCard extends Card {
    ...
}
```
```java
@PrimaryKeyJoinColumn(name = "spell_id")
@Entity
public class SpellCard extends Card {
    ...
}
```
```java
@PrimaryKeyJoinColumn(name = "trap_id")
@Entity
public class TrapCard extends SpellCard {
    ...
}
```
Pros:
- Less nullable columns
- Normalized schema

Cons:
- Worse query performance (requires joins)
- Worse performance for polymorphic queries (joins for each type + joins for all types)

## TABLE_PER_CLASS strategy
```java
@Inheritance(strategy = TABLE_PER_CLASS)
@Entity
public class Card {
    ...
}
```
```java
@Entity
public class MonsterCard extends Card {
    ...
}
```
```java
@Entity
public class SpellCard extends Card {
    ...
}
```
```java
@Entity
public class TrapCard extends SpellCard {
    ...
}
```
Pros:
- Less nullable columns

Cons:
- Worse performance for polymorphic queries (union all)
- Does not work with IDENTITY id generation strategy (each table generates its own id -> duplicate ids); use SEQUENCE or TABLE
