# Spring + PostgreSQL db setup

## docker-compose.yml
```yaml
version: "3.8"

services:
  db:
    image: postgres:17.0
    container_name: postgres
    ports:
      - "5432:5432"
    volumes:
      - mydata:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: <your user>
      POSTGRES_PASSWORD: <your password>
      POSTGRES_DB: <your db>

volumes:
  mydata:
```

## application.yml

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/<db name>
    username: <username>
    password: <password>
  jpa:
    show-sql: true
```
