# Mockito

## Mockito annotations

### `@Mock`
Can be used instead of `Mockito.mock` method to create a mock object:
```java
// static method
UserRepository userRepository = mock(UserRepository.class);

// annotation
@Mock
private UserRepository userRepository;
```

### `@Spy`
Can be used instead of `Mockito.spy` method to create a partial mock (real object which can have specific behavior overriden):
```java
// static method
List<UserDto> usersSpy = spy(users);

// annotation
@Spy
private List<UserDto> users;
```
!! always use `doReturn` instead of `when` with spies because the latter actually invokes the method before mocking

### `@InjectMocks`
Creates instance of class under test and injects mocks and spies into it
```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;
```

### `@Captor`
Can be used instead of `ArgumentCaptor.forClass` method to create an argument captor:
```java
// static method
ArgumentCaptor<UserEntity> userCaptor = ArgumentCaptor.forClass(UserEntity.class);

// annotation
@Captor
private ArgumentCaptor<UserEntity> userCaptor;
```

### `@MockitoBean`
Replaces a spring bean with a mock in `@SpringBootTest` tests
```java
@SpringBootTest
class UserServiceTest {

    @MockitoBean
    private UserRepository userRepository;

    @Autowired
    private UserService userService;
```

## Argument matchers
- can be used in place of exact method arguments, e.g. `1L -> anyLong()
- cannot be mixed, raw values need to be wrapped, e.g  `eq(1L)`
- use `argThat()` for advanced matching

## Argument captors
Used with `verify()` to capture what was *actually* passed into a mock and inspect it:
```java
@Captor
private ArgumentCaptor<UserEntity> userCaptor;
...
when(userRepository.findById(anyLong())).thenReturn(Optional.of(UserEntity.builder().name("Uleczka").build()));
...
verify(userMapper).toDto(userCaptor.capture());
UserEntity captured = userCaptor.getValue();
assertThat(captured.getName()).isEqualTo("Uleczka");
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





