# Spring beans
Bean - an object created and managed by the ApplicationContext

## Creating a bean
Inside a configuration class:
```java
@Configuration
public class Config {

    @Bean
    public CardService cardService() {
        ...
    }

    ...
```
At component level:
```java
@Component
public class CardService {
    ...
```

## Bean scopes
**Singleton** - default bean scope; only one instance of the bean exists per ApplicationContext
```java
@Bean
@Scope(SCOPE_SINGLETON)
```

**Prototype** - each time the bean is requested from the ApplicationContext, a new instance is created and returned
```java
@Bean
@Scope(SCOPE_PROTOTYPE)
```

**Request** - one instance of the bean per HttpRequest
```java
@Bean
@Scope(SCOPE_REQUEST)
```

**Session** - one instance of the bean per HttpSession
```java
@Bean
@Scope(SCOPE_SESSION)
```

**Application** - one instance of the bean per ServletContext
```java
@Bean
@Scope(SCOPE_APPLICATION)
```

## Lazy beans
Beans that are not created at the application startup, instead their creaton is delayed until they are requested from the ApplicationContext
- default behavior of prototype-scoped beans
- for other scopes, annotate bean with `@Lazy`:
```java
@Bean
@Lazy
public CardService cardService() {
    ...
}
```
```java
@Autowired
@Lazy
private CardService cardService;
```

## Bean lifecycle

### Cration phases
1. Instantiation
2. Dependency injection
3. `BeanNameAware.setBeanName()`, `BeanFactoryAware.setBeanFactory()`, `ApplicationContextAware.setApplicationContext()` called if implemented
4. `BeanPostProcessor.postProcessBeforeInitialization()` called if implemented
5. `InitializingBean.afterPropertiesSet()`, `@Bean(initMethod = ...)` method, `@PostConstruct` annotated method called if implemented
6. `BeanPostProcessor.postProcessAfterInitialization()` called if implemented

### Destruction phases
1. `DisposableBean.destroy()`, `@Bean(destroyMethod = ...)` method, `@PreDestroy` annotated methods called if implemented
