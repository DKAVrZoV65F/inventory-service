# Сервис инвентаризации

Сервис инвентаризации — это микросервис на основе Spring Boot, который управляет доступностью товаров на складе.

## Возможности

- REST API для проверки наличия товаров.
- Использует MySQL в качестве базы данных.
- Документация OpenAPI через Swagger.
- Наблюдаемость с Micrometer.
- Логирование с использованием Loki.
- Поддержка Docker.

## Стек технологий

- Java 21
- Spring Boot 3
- Spring Data JPA
- Springdoc OpenAPI
- Micrometer Observability
- MySQL
- Docker
- Loki для логирования

## Начало работы

### Требования

- Java 21
- Docker и Docker Compose
- MySQL 8.3+

### Запуск приложения

1. **Запустить контейнер MySQL**:

   ```sh
   docker-compose up -d
   ```

2. **Запустить Spring Boot приложение**:

   ```sh
   mvn spring-boot:run
   ```

3. **Доступные API эндпоинты**:

    - Swagger UI: [http://localhost:8082/swagger-ui.html](http://localhost:8082/swagger-ui.html)
    - Проверка наличия товара: `GET /api/inventory?skuCode=XYZ&quantity=10`

## Конфигурация

### `application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3316/inventory_service
spring.datasource.username=root
spring.datasource.password=mysql
server.port=8082
springdoc.swagger-ui.path=/swagger-ui.html
```

### Конфигурация логирования

Настроено использование **Loki**:

- `logback-spring.xml` отправляет логи в Loki по адресу `http://localhost:3100/loki/api/v1/push`.

## Поддержка Docker

Проект включает поддержку Docker:

### `docker-compose.yml`

```yaml
version: '4'
services:
  mysql:
    image: mysql:8.3.0
    container_name: inventory-service-mysql
    environment:
      MYSQL_ROOT_PASSWORD: mysql
    ports:
      - "3316:3306"
    volumes:
      - ./mysql:/var/lib/mysql
      - ./docker/mysql/init.sql:/docker-entrypoint-initdb.d/init.sql
```

## Вклад в проект

Вы можете вносить свой вклад, отправляя pull request'ы или сообщая об ошибках.

## Лицензия

Этот проект лицензирован под Apache 2.0 License.

