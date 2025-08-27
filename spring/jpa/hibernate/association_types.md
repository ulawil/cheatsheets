# Association types

## One-to-many
```java
@Entity
@Table(name = "brand")
public class BrandEntity {

    @OneToMany(mappedBy = "brand", fetch = ?, cascade = ?, orphanRemoval = ?)
    private List<PaintEntity> paints;

    ...
```
```java
@Entity
@Table(name = "paint")
public class PaintEntity {

    @ManyToOne(fetch = ?, cascade = ?, optional = ?)
    @JoinColumn(name = "brand_id")
    private BrandEntity brand;

    ...
```

## Many-to-many
```java
@Entity
@Table(name = "paint")
public class PaintEntity {

    @ManyToMany(fetch = ?, cascade = ?)
    @JoinTable(
            name = "paint_pigment",
            joinColumns = @JoinColumn(name = "paint_id"),
            inverseJoinColumns = @JoinColumn(name = "pigment_id")
    )
    private List<PigmentEntity> pigments;

    ...
```
```java
@Entity
@Table(name = "pigment")
public class PigmentEntity {

    @ManyToMany(mappedBy = "pigments")
    private List<PaintEntity> paints;

    ...
```

## One-to-one
```java
@Entity
@Table(name = "card")
public class Card {

    @OneToOne(fetch = ?, cascade = ?, orphanRemoval = ?, optional = ?)
    @JoinColumn(name = "banlist_info_id")
    private BanlistInfo banlistInfo;

    ...
```
```java
@Entity
@Table(name = "banlist_info")
public class BanlistInfo {

    @OneToOne(mappedBy = "banlistInfo")
    private Card card;

    ...
```

---
- `@JoinColumn` - used to specify the foreign key; goes to the owning side of the relationship (one that contains the foreign key)
- `mappedBy` - used to specify entity that maps the relationship; goes to the non-owning side (one without the foreign key)   
