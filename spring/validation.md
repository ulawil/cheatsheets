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

    @NotBlank
    private String name;

    @NotEmpty
    @Valid
    private List<PigmentShortInfoDto> pigments;

    @NotNull
    @Valid
    private BrandShortInfoDto brand;

    ...
```
```java
public class PigmentShortInfoDto {

    @NotNull
    private Long id;

    ...
}
```
```java
public class BrandShortInfoDto {

    @NotNull
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
