## N + 1 problem

### Solution #1 - JPQL + `JOIN FETCH`

### Solution #2 - batch size

--- 

- ‼️Eager fetching is not a solution, cause sometimes instead of using FetchMode.JOIN it falls back to FetchMode.SELECT to avoid cartesian product and we're still left with n + 1 selects  
  
- ‼️FetchMode.SUBSELECT is unpredictable so don't use it either  
