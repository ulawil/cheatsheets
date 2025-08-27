# Entity states

## Transient
- entity is not associated with persistence context
- entity does not have a corresponding table row in db
- e.g. after `... = new CardEntity();`

## Persistent
- entity is associated with persistence context
- entity has a corresponding table row in db or will have when the session is flushed
- e.g. after calling `em.persist()` or `em.merge()`

## Detached
- entity is no longer associated with persistence context
- entity has a corresponding row in db
- e.g. after calling `em.detach()`

# Removed
- entity is associated with persistence context but is marked for removal
- entity has a corresponding table row which will be deleted after the session is flushed
- e.g. after calling `em.remove()`
