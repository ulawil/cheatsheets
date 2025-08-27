# Types mapping

## Enum
```java
@Enumerated(EnumType.STRING)
private Transparency transparency;
```

## Array
```java
@JdbcTypeCode(SqlTypes.ARRAY)
@Column(columnDefinition = "TEXT[]")
private List<String> linkmarkers;
```

## Json
```java
@JdbcTypeCode(SqlTypes.JSON)
@Column(name = "misc_info", columnDefinition = "JSONB")
private MiscInfo miscInfo;
```
