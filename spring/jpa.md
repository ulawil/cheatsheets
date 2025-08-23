### Relationship mapping
<details>
  <summary>One-to-many</summary>

```java
@Entity
@Table(name = "brand")
public class BrandEntity {

    // mappedBy - goes to the non-owning side (one without the foreign key)   
    @OneToMany(mappedBy = "brand", fetch = ?, cascade = ?, orphanRemoval = ?)
    private List<PaintEntity> paints;

    ...
}
```
```java
@Entity
@Table(name = "paint")
public class PaintEntity {

    @ManyToOne(fetch = ?, cascade = ?, optional = ?)
    @JoinColumn(name = "brand_id") // goes to the owning side of the relationship (one that contains the foreign key)  
    private BrandEntity brand;

    ...
```

</details>

<details>
  <summary>Many-to-many</summary>

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

</details>

<details>
  <summary>One-to-one</summary>

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
}
```

</details>

<details>
  <summary>Fetch types</summary>
</br>
  
`fetch` - specifies at what point the referenced entity/collection of entities is fetched:
* `FetchType.EAGER` - when the referencing entity is fetched; default for `@OneToOne`, `@ManyToOne` realtionships
* `FetchType.LAZY` - when the referenced entity is accessed; default for `@OneToMany`, `@ManyToMany` realtionships


</details>

<details>
  <summary>Cascade types</summary>
</br>
  
`cascade` - specifies which operations will cascade to the referenced entity/collection of entities:
* `CascadeType.ALL`
* `CascadeType.PERSIST`
* `CascadeType.MERGE`
* `CascadeType.DETACH`
* `CascadeType.REMOVE`
* `CascadeType.REFRESH`

</details>

### Type mapping

<details>
  <summary>Enum</summary>

```java
@Enumerated(EnumType.STRING)
private Transparency transparency;
```

</details>

<details>
  <summary>Array</summary>

```java
@JdbcTypeCode(SqlTypes.ARRAY)
@Column(columnDefinition = "TEXT[]")
private List<String> linkmarkers;
```

</details>

<details>
  <summary>Json</summary>

```java
@JdbcTypeCode(SqlTypes.JSON)
@Column(name = "misc_info", columnDefinition = "JSONB")
private MiscInfo miscInfo;
```

</details>
