---
title: "foreign_rnr — проверка разрешения на работу"
description: "Метод NEWDB foreign_rnr для проверки разрешения на работу (РНР) иностранного гражданина по данным документа."
canonical_url: https://newdb.net/docs/foreign/05-foreign_rnr/
meta:
  - name: keywords
    content: "NEWDB API, foreign_rnr, РНР, разрешение на работу, иностранные граждане"
  - property: og:title
    content: "Проверка разрешения на работу — метод foreign_rnr"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода foreign_rnr для проверки разрешения на работу."
---

# foreign_rnr — Разрешение на работу (РНР)

POST `https://api.newdb.net/v2`

Метод выполняет проверку разрешения на работу иностранного гражданина по данным документа.

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "foreign_rnr",
    "doctype": "rnr",
    "doc_seria": "string",
    "doc_number": "string",
    "id_doc_seria": "string",
    "id_doc_number": "string",
    "blank_seria": "string",
    "blank_number": "string",
    "country": "ru"
  },
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
    "method": "foreign_rnr",
    "doctype": "rnr",
    "doc_seria": "82",
    "doc_number": "2205693712",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "blank_seria": "РР",
    "blank_number": "8118448",
    "country": "ru"
  },
  "requestId": "b4c61a6b-34cc-430e-bbeb-a6528014bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "foreign_rnr",
    "doctype": "rnr",
    "doc_seria": "82",
    "doc_number": "2205693712",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "blank_seria": "РР",
    "blank_number": "8118448",
    "country": "ru",
    "newdb_qid": "EJoZIP3R7Yy9MygC"
  },
  "requestId": "b4c61a6b-34cc-430e-bbeb-a6528014bca4",
  "datecreated": "2026-01-18 17:56:20",
  "state": "complete",
  "balance": 9867,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "foreign_rnr": {
      "taskId": "26d6d020-1202-47b5-9bbf-36f8611c36c1",
      "dateupdated": "2026-01-18 17:56:51",
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
      "name": "foreign_rnr",
      "description": "Проверка разрешения на работу (РНР) иностранного гражданина по данным документа.",
      "input_schema": {
        "method": "string (foreign_rnr)",
        "doctype": "string (rnr)",
        "doc_seria": "string",
        "doc_number": "string",
        "id_doc_seria": "string",
        "id_doc_number": "string",
        "blank_seria": "string",
        "blank_number": "string",
        "country": "string (ru)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "foreign_rnr": {
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
            "method": "foreign_rnr",
            "doctype": "rnr",
            "doc_seria": "82",
            "doc_number": "2205693712",
            "id_doc_seria": "FA",
            "id_doc_number": "4678821",
            "blank_seria": "РР",
            "blank_number": "8118448",
            "country": "ru"
          },
          "requestId": "b4c61a6b-34cc-430e-bbeb-a6528014bca4"
        },
        "response": {
          "requestId": "b4c61a6b-34cc-430e-bbeb-a6528014bca4",
          "state": "complete",
          "results": {
            "foreign_rnr": {
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
  "policy": "Если пользователь просит проверить разрешение на работу (РНР) — используйте метод foreign_rnr и верните статус по документу."
}
```
