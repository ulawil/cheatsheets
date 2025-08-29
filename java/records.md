# Records

Records - immutable data classes that are final and have only private final fields by default

Records automatically generate:
- all-args constructor
- getters
- `equals()` & `hashCode()`
- `toString()`

Records can:
- have compact constructors for validation
- have static fields and methods
- have instance methods
- implement interfaces

Records cannot:
- have instance fields that are not included in the header
- have setters (fields are `private final` by default)
- extend classes (already extend Record by default)
- be extended (are final by default)

Example:
```java
public record Person(String name, Integer weight, Integer height, LocalDate dateOfBirth) {

    // compact constructor for validation
    public Person {
        Objects.requireNonNull(name);
        if (dateOfBirth.isAfter(LocalDate.now())) {
            throw new IllegalStateException();
        }
    }

    // constructor with different arg list
    public Person(String name, LocalDate dateOfBirth) {
        this(name, null, null, dateOfBirth);
    }
}
```
```java
// all-args constructor example:
Person p1 = new Person("Ula", 63, 163, LocalDate.parse("1997-03-12"));
Person p2 = new Person("Shidou", 75, 185, LocalDate.parse("1997-07-07"));

// getter example:
System.out.println(p1.name());

// toString() example:
System.out.println(p1); // Person[name=Ula, weight=63, height=163, dateOfBirth=1997-03-12]

// equals & hashCode example:
System.out.println(p1.equals(p2));
```
