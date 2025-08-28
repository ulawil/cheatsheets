# Session vs EntityManager

## Session
- Hibernate interface representing persistence context
- Implementation provided by Hibernate

## EntityManager
- JPA interface representing persistence context
- Implementation needs to be provided by a persistence provider, e.g. Hibernate
- If implementation provided by Hibernate, can obtain session by calling `em.unwrap(Session.class)`
