---
title: "bankrot_legal — банкротство юрлица через ЕФРСБ"
description: "Метод NEWDB bankrot_legal ищет сведения о банкротстве юридического лица в Едином федеральном реестре сведений о банкротстве."
canonical_url: https://newdb.net/docs/legal/03-bankrot_legal/
meta:
  - name: keywords
    content: "NEWDB API, bankrot_legal, ЕФРСБ, банкротство, юрлица"
  - property: og:title
    content: "Проверка банкротства юрлица — метод bankrot_legal"
  - property: og:description
    content: "Получите статусы дел и публикации ЕФРСБ по ИНН юридического лица через API NEWDB."
---

# bankrot_legal — Проверка на банкротство юрлица (Федресурс)

POST `https://api.newdb.net/v2`

Метод выполняет проверку юридического лица на наличие сведений о банкротстве в ЕФРСБ. Поиск осуществляется по ИНН компании.

## Заголовки

```text
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)

```json
{
  "params": {
    "inn": "string (ИНН юрлица)",
    "country": "string (ru)",
    "method": "bankrot_legal"
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
    "inn": "7707332613",
    "country": "ru",
    "method": "bankrot_legal"
  },
  "requestId": "a5962f98-2916-4779-b52d-43c123faa812"
}
```

## Пример ответа

```json
{
  "params": {
    "inn": "7707332613",
    "country": "ru",
    "method": "bankrot_legal"
  },
  "requestId": "a5962f98-2916-4779-b52d-43c123faa812",
  "datecreated": "2026-03-20 07:09:05",
  "state": "complete",
  "balance": 9708,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "bankrot_legal": {
      "result": {
        "status": 200,
        "data": [
          {
            "bankruptcy": [],
            "commmon": {
              "type": "company",
              "name_or_fio": "ООО \"АПЕКС КОНСАЛТ\"",
              "inn": "7707332613",
              "reg_number_type": "ОГРН",
              "reg_number": "1157746102535",
              "activity": "Разработка компьютерного программного обеспечения",
              "address": "127473, Г.МОСКВА, ПЕР. 1-Й САМОТЁЧНЫЙ, Д. 2, СТР. 2, ПОМЕЩ. 4 ОФ 3",
              "status": "Действующее",
              "details_url": "https://fedresurs.ru/companies/97a3146e-dc92-4b7a-ae9e-026fd6999091"
            },
            "encumbrances": [],
            "publications": []
          }
        ]
      },
      "taskId": "d51e5882-f1d3-4d24-a7da-74547dfcaebb",
      "dateupdated": "2026-03-20 07:09:48"
    }
  }
}
```

## Поля результата `results.bankrot_legal.result.data[]`

| Поле | Описание |
|------|----------|
| `bankruptcy` | Список дел о банкротстве |
| `commmon` | Карточка компании из источника |
| `encumbrances` | Обременения, если они найдены |
| `publications` | Публикации по компании в ЕФРСБ |

## x-ai (метаданные для AI)

```json
{
  "tools": [
    {
      "name": "bankrot_legal",
      "description": "Проверка сведений о банкротстве юридического лица по ИНН через Федресурс.",
      "input_schema": {
        "inn": "string — ИНН юридического лица",
        "country": "string (ru)",
        "method": "string (bankrot_legal)",
        "webhook": "string (URL, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "bankrot_legal": {
            "taskId": "string",
            "dateupdated": "string",
            "result": {
              "status": "number",
              "data": "array — карточки компаний и сведения о банкротстве"
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь хочет проверить банкротство юридического лица по ИНН, используй метод bankrot_legal."
}
```
