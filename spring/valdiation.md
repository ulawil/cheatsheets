### Dependency:
```
implementation("org.springframework.boot:spring-boot-starter-validation")
```

### Annotations:
```
@Positive
@PositiveOrZero
@Negative
@NegativeOrZero
@Pattern(regexp = )
```

### Usage:
#### With path variables/request params:
```
@PathVariable("id") @Positive Long brandId
```

#### With request bodies:  
