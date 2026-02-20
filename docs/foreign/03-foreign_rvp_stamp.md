---
title: "foreign_rvp_stamp — проверка РВП (штамп в паспорте)"
description: "Метод NEWDB foreign_rvp_stamp для проверки разрешения на временное проживание (штамп в паспорте) иностранного гражданина."
canonical_url: https://newdb.net/docs/foreign/03-foreign_rvp_stamp/
meta:
  - name: keywords
    content: "NEWDB API, foreign_rvp_stamp, РВП, штамп, иностранные граждане"
  - property: og:title
    content: "Проверка РВП (штамп в паспорте) — метод foreign_rvp_stamp"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода foreign_rvp_stamp для проверки РВП."
---

# foreign_rvp_stamp — РВП (штамп в паспорте)

POST `https://api.newdb.net/v2`

Метод выполняет проверку разрешения на временное проживание (штамп) иностранного гражданина по данным паспорта и дате выдачи.

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "foreign_rvp_stamp",
    "doctype": "rvp_stamp",
    "firstname": "string",
    "lastname": "string",
    "issue_date": "YYYY-MM-DD",
    "id_doc_seria": "string",
    "id_doc_number": "string",
    "country": "ru"
  },
  "requestId": "optional-string"
}
```


## Пояснения к полям
- `doc_seria` и `doc_number` — реквизиты документа, который проверяем.
- `blank_seria` и `blank_number` — серия и номер бланка.
- `id_doc_seria` и `id_doc_number` — серия и номер документа, удостоверяющего личность.

## Пример запроса
```http
POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
  "params": {
    "method": "foreign_rvp_stamp",
    "doctype": "rvp_stamp",
    "firstname": "Хаджиакбар",
    "lastname": "Юлдошев",
    "issue_date": "2025-01-01",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "country": "ru"
  },
  "requestId": "b4c61a6b-39cc-432e-bbeb-a6518014bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "foreign_rvp_stamp",
    "doctype": "rvp_stamp",
    "firstname": "Хаджиакбар",
    "lastname": "Юлдошев",
    "issue_date": "2025-01-01",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "country": "ru",
    "newdb_qid": "EJUYIK3M3om9MygA"
  },
  "requestId": "b4c61a6b-39cc-432e-bbeb-a6518014bca4",
  "datecreated": "2026-01-18 16:07:22",
  "state": "complete",
  "balance": 9870,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "foreign_rvp_stamp": {
      "taskId": "250607d8-e2c0-4118-9954-568ae2d41353",
      "dateupdated": "2026-01-18 16:07:55",
      "result": {
        "status": 200,
        "data": [
          {
            "doc_status": "Данные не найдены"
          }
        ]
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
      "name": "foreign_rvp_stamp",
      "description": "Проверка разрешения на временное проживание (РВП, штамп в паспорте) иностранного гражданина по данным паспорта и дате выдачи.",
      "input_schema": {
        "method": "string (foreign_rvp_stamp)",
        "doctype": "string (rvp_stamp)",
        "firstname": "string",
        "lastname": "string",
        "issue_date": "string (YYYY-MM-DD)",
        "id_doc_seria": "string",
        "id_doc_number": "string",
        "country": "string (ru)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "foreign_rvp_stamp": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "doc_status": "string"
                }
              ]
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "method": "foreign_rvp_stamp",
            "doctype": "rvp_stamp",
            "firstname": "Хаджиакбар",
            "lastname": "Юлдошев",
            "issue_date": "2025-01-01",
            "id_doc_seria": "FA",
            "id_doc_number": "4678821",
            "country": "ru"
          },
          "requestId": "b4c61a6b-39cc-432e-bbeb-a6518014bca4"
        },
        "response": {
          "requestId": "b4c61a6b-39cc-432e-bbeb-a6518014bca4",
          "state": "complete",
          "results": {
            "foreign_rvp_stamp": {
              "result": {
                "status": 200,
                "data": [
                  {
                    "doc_status": "Данные не найдены"
                  }
                ]
              }
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь просит проверить РВП (штамп в паспорте) — используйте метод foreign_rvp_stamp и верните статус по документу."
}
```
