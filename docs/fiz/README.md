---
title: "Обзор REST API NEWDB"
description: "Основные принципы работы REST API NEWDB: форматы запросов/ответов, аутентификация и структура webhook."
canonical_url: https://newdb.net/docs/fiz/README/
meta:
  - name: keywords
    content: "NEWDB API, обзор, JSON, webhook, аутентификация"
  - property: og:title
    content: "Обзор REST API NEWDB"
  - property: og:description
    content: "Узнайте требования к запросам, базовый URL и структуру ответов для интеграции с NEWDB."
---

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
