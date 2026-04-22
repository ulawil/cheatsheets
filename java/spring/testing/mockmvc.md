# MockMVC

## Dependency

```java
testImplementation("org.springframework.boot:spring-boot-starter-test")
```

## Example

```java
@SpringBootTest
@AutoConfigureMockMvc
public class SomeIntegrationTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    void someTest() throws Exception {
        ...
        mockMvc.perform(post("/someEndpoint")
                        .content("some json content as string")
                        .contentType("application/json")
                .andExpect(status().isCreated())
                // if response root is a single element:
                .andExpect(jsonPath("$.field").value("value"));
                // if response root is an array:
                .andExpect(jsonPath("$.length()").value(...))
                .andExpect(jsonPath("$[0].field").value("value1"))
                .andExpect(jsonPath("$[1].field").value("value2"));
                ...
                // hamcrest matcher example:
                .andExpect(jsonPath("$[0].field", notNullValue()))
        ...
    }

```
