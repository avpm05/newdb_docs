---
title: "patent_msk — проверка патента (Москва)"
description: "Метод NEWDB patent_msk для проверки патента иностранного гражданина в Москве по данным документа."
canonical_url: https://newdb.net/docs/foreign/07-foreign_patent_msk/
meta:
  - name: keywords
    content: "NEWDB API, patent_msk, патент Москва, иностранные граждане, проверка документов"
  - property: og:title
    content: "Проверка патента в Москве — метод patent_msk"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода patent_msk для проверки патента в Москве."
---

# patent_msk — Патент (Москва)

POST `https://api.newdb.net/v2`

Метод выполняет проверку патента для Москвы по данным документа, удостоверяющего личность.

## Заголовки
```http
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "patent_msk",
    "id_doc_seria": "string",
    "id_doc_number": "string",
    "citizenship": "string (optional)",
    "country": "ru"
  },
  "requestId": "optional-string"
}
```

## Пояснения к полям
- `id_doc_seria` и `id_doc_number` — серия и номер документа, удостоверяющего личность.
- `citizenship` — опциональный параметр.
- Если `citizenship` не передан, проверка выполняется по 3 странам: `Узбекистан`, `Таджикистан`, `Кыргызстан`.

## Пример запроса
```http
POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
  "params": {
    "method": "patent_msk",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "citizenship": "Узбекистан",
    "country": "ru"
  },
  "requestId": "b4c65a6b-45cc-440e-bbeb-a6528014bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "patent_msk",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "citizenship": "Узбекистан",
    "country": "ru",
    "newdb_qid": "ENUjIKqUmdTLMygC"
  },
  "requestId": "b4c65a6b-45cc-440e-bbeb-a6528014bca4",
  "datecreated": "2026-03-04 23:24:48",
  "state": "complete",
  "balance": 9810,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "patent_msk": {
      "taskId": "b9e7d26d-4d0a-4e9e-a037-2fc47abcba33",
      "dateupdated": "2026-03-04 23:25:05",
      "result": {
        "status": 200,
        "data": [
          {
            "citizenship": "Узбекистан",
            "message": "Срок действия Вашего патента истек 26.08.2025 Для работы в Москве необходимо оформить новый патент.",
            "status": "expired"
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
      "name": "patent_msk",
      "description": "Проверка патента иностранного гражданина в Москве по данным документа, удостоверяющего личность.",
      "input_schema": {
        "method": "string (patent_msk)",
        "id_doc_seria": "string",
        "id_doc_number": "string",
        "citizenship": "string (optional)",
        "country": "string (ru)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "patent_msk": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "citizenship": "string",
                  "message": "string",
                  "status": "string"
                }
              ]
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь просит проверить патент в Москве — используйте метод patent_msk и верните результат проверки."
}
```
