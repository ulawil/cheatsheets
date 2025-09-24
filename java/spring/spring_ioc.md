# Spring IoC

## Dependency injection
Done with `@Autowired` annotation (or if using Spring 4.3+ and constructor injection, can be ommitted)  

Constructor injection:
```java
@Autowired
public CardController(CardService cardService) {
    this.cardService = cardService;
}
```
or in Spring 4.3+ with Lombok:
```java
@RequiredArgsConstructor
public class CardController {

    private final CardService cardService;

    ...
```
- allows for injecting final fields
- decreases risk of NPE because all beans have to be injected before bean can be used

Setter injection:
```java
@Autowired
public void setCardService(CardService cardService) {
    this.cardService = cardService;
}
```
- okay for injecting optional dependencies
- can cause NPE

Field injection:
```java
@Autowired
private CardService cardService;
```
- slow because it uses Reflection
- can cause NPE
