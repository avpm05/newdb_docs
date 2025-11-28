# Обзор API

Все методы принимают и возвращают JSON. Для асинхронных задач поддерживается `webhook`.

### Общие требования
- `Content-Type: application/json`
- `X-API-KEY: <your_token>`

### Структура ответа асинхронных методов
- `requestId` — идентификатор запроса
- `state` —  `in progress` | `complete` | `error`
- `results.<method>.result` — полезные данные

### Базовый URL

```
https://api.newdb.net/v2
```
