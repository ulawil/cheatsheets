# Mockito

## Dependency
```java
testImplementation("org.springframework.boot:spring-boot-starter-test")
```

## Mockito annotations
- `@Mock` - used to create a mock object instead of Mockito.mock method
- `@InjectMocks` - injects created mocks into the class that is being tested instead of injecting them manually through constructor
- `@ExtendWith(MockitoExtension.class)` - enables Mockito in Junit5 (`@Mock` objects are created, `InjectMocks` is processed)
- `@MockBean` - replaces a spring bean with a mock in `@SpringBootTest` tests
- `@Spy` - used to create a partial mock (real object which can have specific behavior overriden) instead of Mockito.spy
- `@Captor` - captures method arguments

Mocking with Spring example:
```java
@ExtendWith(MockitoExtension.class)
class UserServiceUnitTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    void userService_issueGreeting_success() {
        // given
        Long userId = 1L;
        User user = User.builder().id(userId).name("Uleczka").build();
        when(userRepository.findById(userId)).thenReturn(Optional.of(user));

        // when
        String result = userService.issueGreeting(userId);

        // then
        assertThat(result).isEqualTo("Hello, Uleczka");
        verify(userRepository).findById(userId);
    }
```

Mocking without Spring example:
```java
    @Test
    void userService_issueGreeting_success() {
        // given
        UserRepository userRepository = mock(UserRepository.class);
        UserService userService = new UserService(userRepository);
        Long userId = 1L;
        User user = User.builder().id(userId).name("Uleczka").build();
        when(userRepository.findById(userId))
                .thenReturn(Optional.of(user));
        // when
        String result = userService.issueGreeting(userId);

        // then
        assertThat(result).isEqualTo("Hello, Uleczka");

        verify(userRepository).findById(idCaptor.capture());
        Long id = idCaptor.getValue();
        assertThat(id).isEqualTo(1L);
    }
```

## Argument matchers
- can be used in place of exact method arguments, e.g. `1L -> anyLong()
- cannot be mixed, raw values need to be wrapped, e.g  `eq(1L)`
- use `argThat()` for advanced matching

## Argument captors
- use with `verify()` to capture what was *actually* passed into a mock and inspect it
```
@Captor
ArgumentCaptor<Long> idCaptor;
...
verify(userRepository).findById(idCaptor.capture());
Long id = idCaptor.getValue();
assertThat(id).isEqualTo(1L);

```

## Verification mode
- used to check how many times method was invoked

## Mocking static methods
Needs `mockito-inline` dependency which is already included in spring boot starter;
done by using `MockedStatic` object created with `mockStatic` method inside try-with-resources block:
```java
try (MockedStatic<UserUtils> utilsMock = mockStatic(UserUtils.class)) {
    utilsMock.when(() -> UserUtils.validateId(userId)).thenThrow(new RuntimeException());
    // rest of the test in this block!!
        
```

## Mocking final classes
Needs `mockito-inline` dependency which is already included in spring boot starter;
then works like regular mocking
```java
JwtUtils mockJwtUtils = mock(JwtUtils.class);
when(mockJwtUtils.generateJwt()).thenReturn("lololo")
// rest of the test
```

## Creating objects at runtime
Needs `mockito-inline` dependency which is already included in spring boot starter;
done by using `MockedConstruction` object created with `mockConstruction` method inside try-with-resouces block:
```java
try (MockedConstruction<User> mockedUser = mockConstruction(User.class,
    (mock, context) -> when(mock.getName()).thenReturn("Uleczka"))) {

    User result = userService.getUser(1L);

    assertThat(result.getName()).isEqualTo("Uleczka");
}
```





