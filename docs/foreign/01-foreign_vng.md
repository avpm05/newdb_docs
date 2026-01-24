---
title: "foreign_vng — проверка ВНЖ (вид на жительство)"
description: "Метод NEWDB foreign_vng для проверки вида на жительство (ВНЖ) иностранного гражданина по документам и ФИО."
canonical_url: https://newdb.net/docs/foreign/01-foreign_vng/
meta:
  - name: keywords
    content: "NEWDB API, foreign_vng, ВНЖ, иностранные граждане, проверка документов"
  - property: og:title
    content: "Проверка ВНЖ иностранного гражданина — метод foreign_vng"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода foreign_vng для проверки вида на жительство."
---

# foreign_vng — Вид на жительство (ВНЖ)

POST `https://api.newdb.net/v2`

Метод выполняет проверку вида на жительство иностранного гражданина по данным документа и ФИО.

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "foreign_vng",
    "doctype": "vng",
    "firstname": "string",
    "lastname": "string",
    "doc_seria": "string",
    "doc_number": "string",
    "id_doc_seria": "string",
    "id_doc_number": "string",
    "blank_seria": "string",
    "blank_number": "string",
    "dob": "YYYY-MM-DD",
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
    "method": "foreign_vng",
    "doctype": "vng",
    "firstname": "Хаджиакбар",
    "lastname": "Юлдошев",
    "doc_seria": "82",
    "doc_number": "2205693712",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "blank_seria": "РР",
    "blank_number": "8118448",
    "dob": "1985-12-01",
    "country": "ru"
  },
  "requestId": "b4c63a7b-45cc-031e-bbeb-a6518014bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "foreign_vng",
    "doctype": "vng",
    "firstname": "Хаджиакбар",
    "lastname": "Юлдошев",
    "doc_seria": "82",
    "doc_number": "2205693712",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "blank_seria": "РР",
    "blank_number": "8118448",
    "dob": "1985-12-01",
    "country": "ru",
    "newdb_qid": "EJQYIJ7pnYm9MygA"
  },
  "requestId": "b4c63a7b-45cc-031e-bbeb-a6518014bca4",
  "datecreated": "2026-01-18 15:49:41",
  "state": "complete",
  "balance": 9875,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "foreign_vng": {
      "taskId": "c0fb4556-152b-4590-99d8-8779cb887a74",
      "dateupdated": "2026-01-18 15:50:13",
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
      "name": "foreign_vng",
      "description": "Проверка вида на жительство (ВНЖ) иностранного гражданина по данным документа и ФИО.",
      "input_schema": {
        "method": "string (foreign_vng)",
        "doctype": "string (vng)",
        "firstname": "string",
        "lastname": "string",
        "doc_seria": "string",
        "doc_number": "string",
        "id_doc_seria": "string",
        "id_doc_number": "string",
        "blank_seria": "string",
        "blank_number": "string",
        "dob": "string (YYYY-MM-DD)",
        "country": "string (ru)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "foreign_vng": {
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
            "method": "foreign_vng",
            "doctype": "vng",
            "firstname": "Хаджиакбар",
            "lastname": "Юлдошев",
            "doc_seria": "82",
            "doc_number": "2205693712",
            "id_doc_seria": "FA",
            "id_doc_number": "4678821",
            "blank_seria": "РР",
            "blank_number": "8118448",
            "dob": "1985-12-01",
            "country": "ru"
          },
          "requestId": "b4c63a7b-45cc-031e-bbeb-a6518014bca4"
        },
        "response": {
          "requestId": "b4c63a7b-45cc-031e-bbeb-a6518014bca4",
          "state": "complete",
          "results": {
            "foreign_vng": {
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
  "policy": "Если пользователь просит проверить ВНЖ иностранного гражданина — используйте метод foreign_vng и верните статус по документу."
}
```
