---
title: "terrorist — проверка на причастность к терроризму и распространению ОМУ"
description: "Метод NEWDB terrorist проверяет совпадения по перечням причастных к экстремистской деятельности, терроризму и распространению оружия массового уничтожения."
canonical_url: https://newdb.net/docs/fiz/12-terrorist/
meta:
  - name: keywords
    content: "NEWDB API, terrorist, терроризм, ОМУ, экстремизм, проверка физлица"
  - property: og:title
    content: "Проверка на причастность к терроризму и ОМУ — метод terrorist"
  - property: og:description
    content: "Проверка физического лица по ФИО и дате рождения на совпадения с перечнями терроризма, экстремизма и распространения ОМУ."
---

# terrorist — Проверка на причастность к терроризму и распространению ОМУ

POST `https://api.newdb.net/v2`

Метод выполняет поиск совпадений по ФИО и дате рождения в перечнях лиц, причастных к экстремистской деятельности, терроризму и распространению оружия массового уничтожения.

## Заголовки

```text
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)

```json
{
  "params": {
    "lastname": "string",
    "firstname": "string",
    "secondname": "string",
    "dob": "YYYY-MM-DD",
    "country": "string (ru)",
    "method": "terrorist"
  },
  "webhook": "https://your.host/whook",
  "requestId": "optional-string"
}
```

## Пример запроса

```http
POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
  "params": {
    "method": "terrorist",
    "lastname": "АЛИМОВ",
    "firstname": "РЕФАТ",
    "secondname": "МАМЕТОВИЧ",
    "dob": "1991-10-28",
    "country": "ru"
  },
  "requestId": "b4c68a6b-44cc-430e-bbeb-a5518014bca4"
}
```

## Пример ответа

```json
{
  "params": {
    "method": "terrorist",
    "lastname": "АЛИМОВ",
    "firstname": "РЕФАТ",
    "secondname": "МАМЕТОВИЧ",
    "dob": "1991-10-28",
    "country": "ru"
  },
  "requestId": "b4c68a6b-44cc-430e-bbeb-a5518014bca4",
  "datecreated": "2026-03-20 09:00:00",
  "state": "complete",
  "balance": 9696,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "terrorist": {
      "taskId": "0a95a93c-57f0-45f3-90ca-548729e08c68",
      "dateupdated": "2026-03-20 09:00:04",
      "result": {
        "status": 200,
        "data": [
          {
            "query": "АЛИМОВ РЕФАТ МАМЕТОВИЧ 28.10.1991 г.р.",
            "suggestions": [
              "1269. АЛИМОВ РЕФАТ МАМЕТОВИЧ*, 28.10.1991 г.р. , Г. ДУШАНБЕ ТАДЖИКСКОЙ ССР;"
            ]
          }
        ]
      }
    }
  }
}
```

## Поля результата `results.terrorist.result.data[]`

| Поле | Описание |
|------|----------|
| `query` | Поисковая строка, сформированная из ФИО и даты рождения |
| `suggestions` | Список найденных совпадений или похожих записей в перечне |

## Пример ответа без совпадений

```json
{
  "state": "complete",
  "results": {
    "terrorist": {
      "result": {
        "status": 200,
        "data": []
      }
    }
  }
}
```

## x-ai (метаданные для AI)

```json
{
  "tools": [
    {
      "name": "terrorist",
      "description": "Проверка физического лица по ФИО и дате рождения на совпадения с перечнями причастных к экстремистской деятельности, терроризму и распространению оружия массового уничтожения.",
      "input_schema": {
        "lastname": "string — фамилия",
        "firstname": "string — имя",
        "secondname": "string — отчество",
        "dob": "string (YYYY-MM-DD) — дата рождения",
        "country": "string (ru)",
        "method": "string (terrorist)",
        "webhook": "string (URL, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "terrorist": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "query": "string — поисковая строка",
                  "suggestions": "array — найденные совпадения"
                }
              ]
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь хочет проверить физлицо на причастность к терроризму, экстремизму или распространению ОМУ по ФИО и дате рождения, используй метод terrorist."
}
```
