# Testcontainers

## Dependency
```java
testImplementation(platform("org.testcontainers:testcontainers-bom:1.20.4"))  // bom, example version

testImplementation("org.testcontainers:testcontainers")                       // core
testImplementation("org.testcontainers:junit-jupiter")                        // junit5 integration
testImplementation("org.testcontainers:postgresql")                           // db module, e.g. postgres

testImplementation("org.springframework.boot:spring-boot-testcontainers")     // spring boot integration
```

## Example

```java
@SpringBootTest
@Testcontainers
public class SomeIntegrationTest {

    @Container
    @ServiceConnection
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:17-alpine"); // example image

    // that's it, now write tests
```
