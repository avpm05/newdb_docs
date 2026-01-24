---
title: "foreign_patent — проверка патента"
description: "Метод NEWDB foreign_patent для проверки патента иностранного гражданина по данным документа и ФИО."
canonical_url: https://newdb.net/docs/foreign/02-foreign_patent/
meta:
  - name: keywords
    content: "NEWDB API, foreign_patent, патент, иностранные граждане, проверка документов"
  - property: og:title
    content: "Проверка патента иностранного гражданина — метод foreign_patent"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода foreign_patent для проверки патента."
---

# foreign_patent — Патент

POST `https://api.newdb.net/v2`

Метод выполняет проверку патента иностранного гражданина по данным документа и ФИО.

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "foreign_patent",
    "doctype": "patent",
    "firstname": "string",
    "lastname": "string",
    "secondname": "string",
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
    "method": "foreign_patent",
    "doctype": "patent",
    "firstname": "Хаджиакбар",
    "lastname": "Юлдошев",
    "secondname": "Джумабой Угли",
    "doc_seria": "82",
    "doc_number": "2205693712",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "blank_seria": "РР",
    "blank_number": "8118448",
    "dob": "1985-12-01",
    "country": "ru"
  },
  "requestId": "b4c61a6b-34cc-440e-bbeb-a6528024bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "foreign_patent",
    "doctype": "patent",
    "firstname": "Хаджиакбар",
    "lastname": "Юлдошев",
    "secondname": "Джумабой Угли",
    "doc_seria": "82",
    "doc_number": "2205693712",
    "id_doc_seria": "FA",
    "id_doc_number": "4678821",
    "blank_seria": "РР",
    "blank_number": "8118448",
    "dob": "1985-12-01",
    "country": "ru",
    "newdb_qid": "EJcZIIORoom9MygC"
  },
  "requestId": "b4c61a6b-34cc-440e-bbeb-a6528024bca4",
  "datecreated": "2026-01-18 15:50:50",
  "state": "complete",
  "balance": 9874,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "foreign_patent": {
      "taskId": "59fa0c7d-ed1a-40c9-b43d-6e7144ff8956",
      "dateupdated": "2026-01-18 15:51:20",
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
      "name": "foreign_patent",
      "description": "Проверка патента иностранного гражданина по данным документа и ФИО.",
      "input_schema": {
        "method": "string (foreign_patent)",
        "doctype": "string (patent)",
        "firstname": "string",
        "lastname": "string",
        "secondname": "string",
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
          "foreign_patent": {
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
            "method": "foreign_patent",
            "doctype": "patent",
            "firstname": "Хаджиакбар",
            "lastname": "Юлдошев",
            "secondname": "Джумабой Угли",
            "doc_seria": "82",
            "doc_number": "2205693712",
            "id_doc_seria": "FA",
            "id_doc_number": "4678821",
            "blank_seria": "РР",
            "blank_number": "8118448",
            "dob": "1985-12-01",
            "country": "ru"
          },
          "requestId": "b4c61a6b-34cc-440e-bbeb-a6528024bca4"
        },
        "response": {
          "requestId": "b4c61a6b-34cc-440e-bbeb-a6528024bca4",
          "state": "complete",
          "results": {
            "foreign_patent": {
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
  "policy": "Если пользователь просит проверить патент иностранного гражданина — используйте метод foreign_patent и верните статус по документу."
}
```
