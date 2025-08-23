### Dependency:
```
implementation("org.springframework.boot:spring-boot-starter-validation")
```

### Annotations:
#### General:
* `@NotNull`
 
#### Numbers:
* `@Positive`, `@PositiveOrZero`
* `@Negative`, `@NegativeOrZero`
* `@Min`, `@DecimalMin`
* `@Max`, `@DecimalMax`
* `@Digits(integer = , fraction = )`

#### Strings:
* `@NotBlank`
* `@Pattern(regexp = )`
* `@Email`

#### Arrays, collections, maps, strings:
* `@NotEmpty`
* `@Size`

#### Dates:
* `@Past`, `@PastOrPresent`
* `@Future`, `@FutureOrPresent`

### Usage:
#### With path variables/request params:
```java
@PathVariable("id") @Positive Long brandId
```

#### With request bodies:  
```java
@RequestBody @Valid PaintFullInfoDto paintFullInfoDto
```
```java
public class PaintFullInfoDto {

    ...

    // simple field + custom message
    @NotBlank(message = "Paint name must not be blank")
    private String name;

    // simple collection
    @NotEmpty
    private List<@NotNull @Positive Long> pigmentIds;

    // nested dto
    @NotNull
    @Valid
    private BrandShortInfoDto brand;

    // collection of nested dtos
    @NotEmpty
    @Valid
    private List<PigmentShortInfoDto> pigments;

    ...
```
```java
public class BrandShortInfoDto {

    @NotNull
    @Positive
    private Long id;

    ...
}
```
```java
public class PigmentShortInfoDto {

    @NotNull
    @Positive
    private Long id;

    ...
}
```

##### Error handling example:
```java
@ExceptionHandler(MethodArgumentNotValidException.class)
public ResponseEntity<ApiErrorDto> handleValidationException(MethodArgumentNotValidException e) {

    Map<String, String> metadata = e.getFieldErrors().stream()
        .collect(Collectors.toMap(FieldError::getField, FieldError::getDefaultMessage));

    ...
```
