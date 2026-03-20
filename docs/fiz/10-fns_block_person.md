---
title: "fns_block_person — блокировки счетов физлица (ФНС)"
description: "Метод NEWDB fns_block_person проверяет решения ФНС о приостановлении операций по счетам физического лица по ИНН."
canonical_url: https://newdb.net/docs/fiz/10-fns_block_person/
meta:
  - name: keywords
    content: "NEWDB API, fns_block_person, ФНС, блокировка счетов, физлица"
  - property: og:title
    content: "Блокировки счетов физлица — метод fns_block_person"
  - property: og:description
    content: "Проверка решений ФНС о приостановлении операций по счетам по ИНН физического лица через API NEWDB."
---

# fns_block_person — Проверка блокировок счетов физлица (ФНС)

POST `https://api.newdb.net/v2`

Метод возвращает сведения о решениях ФНС по приостановлению операций по банковским счетам физического лица по ИНН.

Для запроса нужно передавать `innfiz` из 12 цифр.

## Заголовки

```text
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)

```json
{
  "params": {
    "innfiz": "string (ИНН физлица, 12 цифр)",
    "country": "string (ru)",
    "method": "fns_block_person"
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
    "innfiz": "132620072012",
    "country": "ru",
    "method": "fns_block_person"
  },
  "webhook": "https://newer.net/whook",
  "requestId": "81862f18-2316-4779-b59d-45c011faa898"
}
```

## Пример ответа

```json
{
  "params": {
    "innfiz": "132620072012",
    "country": "ru",
    "method": "fns_block_person",
    "newdb_qid": "EKgiIKn56YPJMygD"
  },
  "webhook": "https://newer.net/whook",
  "requestId": "81862f18-2316-4779-b59d-45c011faa898",
  "datecreated": "2026-02-24 19:27:51",
  "state": "complete",
  "balance": 9778,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "fns_block": {
      "taskId": "c3311e4f-36ae-4d6d-9610-73bf41662782",
      "dateupdated": "2026-02-24 19:28:01",
      "result": {
        "status": 200,
        "data": [
          {
            "DATASTART": "03.03.2022",
            "NOMER": "990",
            "DATA": "03.03.2022",
            "KODOSNOV": "02",
            "SALDO": "(Отсутствует значение)",
            "IFNS": "1326",
            "BIK": "048952615",
            "DATABI": "06.03.2022 04:06:09"
          },
          {
            "DATASTART": "01.07.2022",
            "NOMER": "786",
            "DATA": "01.07.2022",
            "KODOSNOV": "02",
            "SALDO": "(Отсутствует значение)",
            "IFNS": "1300",
            "BIK": "048952615",
            "DATABI": "06.07.2022 21:45:00"
          }
        ],
        "query": {
          "inn": "1326200720",
          "bik": "442455546"
        }
      }
    }
  }
}
```

## Особенность ответа

Несмотря на метод `fns_block_person`, данные в ответе приходят в блоке `results.fns_block`.

## Поля результата `results.fns_block.result.data[]`

| Поле | Описание |
|------|----------|
| `DATASTART` | Дата начала действия решения о приостановлении операций |
| `NOMER` | Номер решения |
| `DATA` | Дата решения |
| `KODOSNOV` | Код основания |
| `SALDO` | Остаток/сальдо, может отсутствовать |
| `IFNS` | Код налогового органа |
| `BIK` | БИК банка |
| `DATABI` | Дата и время публикации записи |

## x-ai (метаданные для AI)

```json
{
  "tools": [
    {
      "name": "fns_block_person",
      "description": "Проверка решений ФНС о приостановлении операций по счетам физического лица по ИНН.",
      "input_schema": {
        "innfiz": "string — ИНН физического лица, 12 цифр",
        "country": "string (ru)",
        "method": "string (fns_block_person)",
        "webhook": "string (URL, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "fns_block": {
            "taskId": "string",
            "dateupdated": "string",
            "result": {
              "status": "number",
              "data": "array — решения о блокировке счетов",
              "query": "object — параметры поиска"
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь хочет проверить блокировки счетов физлица по ИНН, используй метод fns_block_person и ожидай результат в results.fns_block."
}
```
