## Обзор

API для генерации JWT-токенов

---
## Базовый URL

`http://localhost:8080/api/v1/`

---
## Конечные точки

### 1. Получение токенов

**Endpoint:** `/tokens`

**Метод:** `GET`

**Параметры запроса:**
- `GUID` - идентификатор пользователя

**Описание:** выдает пару access и refresh токенов на основе GUID пользователя.

**Пример запроса**: 
```
/tokens&GUID=760528b4-cfa0-4fe6-86b2-d7cdb8839f3a
```
**Успешный ответ:**
```JSON
{
	"access_token":"string",
}
```

### 2. Обновление токенов

**Endpoint:** `/tokens/refresh`

**Метод:** `POST`

**Описание:** обновляет пару access и refresh токенов пользователя.

**Пример запроса**: 
```JSON
{
	"access_token":"string",
	"refresh_token":"string",  
}
```
**Успешный ответ:**
```JSON
{
	"access_token":"string",
}
```


---
## Запуск проекта

### Переменные окружения

Для запуска проекта необходимо установить переменную JWT_KEY

Для удобства она указана в файле .env

Эту переменную окружения нужно передавать в `docker-compose`

### Шаги для запуска проекта

1. Клонировать репозиторий с github.com

```git
git clone https://github.com/m3owmurrr/token_issuance_service.git
```

2. Запустить контейнеры с помощью docker-compose

```
docker-compose up
```
### Используемые порты

Контейнеры используют следующие порты:

```yaml
ports:
  - "5432:5432"  # PostgreSQL
  - "1969:1969"  # Приложение
```

---
## Используемые технологии

- **Go** - язык программирования.
- **PostgreSQL** - реляционная база данных.
- **Docker** - для контейнеризации приложения.
- **Docker Compose** - для оркестрации многоконтейнерных Docker приложений.

---
## Необходимо сделать

1. Добавить миграцию базы данных через goose
2. Покрыть код тестами
3. Добавить документацию API OpenApi/Swagger
4. Конкретизировать ошибки выдаваемые сервисом
5. Перенести часть данных из файла конфигурации в переменные окружения

---
## Комментарии

Размещение файла .env в открытом доступе является плохой практикой, но в данном случае это сделано для удобства тестирования и проверки