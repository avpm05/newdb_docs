---
title: "patent_mo — проверка патента (Московская область)"
description: "Метод NEWDB patent_mo для проверки патента иностранного гражданина в Московской области по ИНН и дате рождения."
canonical_url: https://newdb.net/docs/foreign/08-foreign_patent_mo/
meta:
  - name: keywords
    content: "NEWDB API, patent_mo, патент Московская область, иностранные граждане, проверка патента"
  - property: og:title
    content: "Проверка патента в Московской области — метод patent_mo"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода patent_mo для проверки патента в Московской области."
---

# patent_mo — Патент (Московская область)

POST `https://api.newdb.net/v2`

Метод выполняет проверку патента для Московской области по ИНН физического лица и дате рождения.

## Заголовки
```http
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "patent_mo",
    "innfiz": "string",
    "dob": "YYYY-MM-DD",
    "country": "ru"
  },
  "requestId": "optional-string"
}
```

## Пояснения к полям
- `innfiz` — ИНН физического лица.
- `dob` — дата рождения в формате `YYYY-MM-DD`.
- `country` — страна запроса (`ru`).

## Пример запроса
```json
{
  "params": {
    "method": "patent_mo",
    "innfiz": "272116001938",
    "dob": "1987-01-08",
    "country": "ru"
  },
  "requestId": "b4c69a6b-45cc-440e-bbeb-a6528014bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "patent_mo",
    "innfiz": "272116001938",
    "dob": "1987-01-08",
    "country": "ru",
    "newdb_qid": "EP0iIP63yfbLMygA"
  },
  "requestId": "b4c69a6b-45cc-440e-bbeb-a6528014bca4",
  "datecreated": "2026-03-05 19:26:22",
  "state": "complete",
  "balance": 9809,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "patent_mo": {
      "taskId": "83845f02-3e3f-4bff-a541-f9eab2f88581",
      "dateupdated": "2026-03-05 19:26:31",
      "result": {
        "status": 200,
        "data": [
          {
            "message": "информация по патенту для текущего лица не найдена",
            "details": "проверьте правильность ИНН и ДАТЫ РОЖДЕНИЯ",
            "status": "not_found"
          }
        ]
      }
    }
  }
}
```

## Статус в ответе
- `status: "not_found"` — данные по патенту не найдены.

## x-ai (метаданные для AI)
```json
{
  "tools": [
    {
      "name": "patent_mo",
      "description": "Проверка патента иностранного гражданина в Московской области по ИНН и дате рождения.",
      "input_schema": {
        "method": "string (patent_mo)",
        "innfiz": "string",
        "dob": "string (YYYY-MM-DD)",
        "country": "string (ru)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "patent_mo": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "message": "string",
                  "details": "string",
                  "status": "string (not_found|valid|expired)"
                }
              ]
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь просит проверить патент в Московской области — используйте метод patent_mo и верните результат проверки."
}
```
