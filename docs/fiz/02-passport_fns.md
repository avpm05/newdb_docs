---
title: "passport_fns — проверка паспорта и ИНН через ФНС"
description: "Метод NEWDB passport_fns для проверки паспорта РФ и поиска ИНН физлица через сервисы Федеральной налоговой службы."
meta:
  - name: keywords
    content: "NEWDB API, passport_fns, ФНС, проверка паспорта, ИНН"
  - property: og:title
    content: "Проверка паспорта и ИНН через ФНС — метод passport_fns"
  - property: og:description
    content: "JSON-схема запроса и ответы метода passport_fns для получения ИНН по паспортным данным."
---

# passport_fns — Проверка  паспорта/ИНН через ФНС

POST `https://api.newdb.net/v2`

Проверка паспорта и ИНН через сервисы ФНС.

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "seria": "string",
    "number": "string",
    "firstname": "string",
    "lastname": "string",
    "secondname": "string",
    "dob": "string" //yyyy-mm-dd,
    "country": "ru",
    "method": "passport_fns"
  },
  "webhook": "https://webhook_url/",
  "requestId": "19342f89-2916-4779-b59d-43c012f1a781"
}
```

## Пример запроса
```http
POST /v2  HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
"params":{
"seria":"4015",
"number":"350278",
"firstname": "Александр", 
"secondname": "Сергеевич",
"lastname": "Малина", 

"dob": "1990-12-17",
"country": "ru",
"method":"passport_fns"
},
"webhook":"https://webhook_url/",
"requestId":"19342f89-2916-4779-b59d-43c012f1a781"
}
```

## Пример ответа (ИНН найден)
```json
{
  "state": "complete",
  "results": {
    "company": {
      "result": {
        "status": 200,
        "data": [
          { "innfiz": "7703245603"  }
        ]
      }
    }
  }
}
```


## Пример ответа (ИНН не найден)
```json
{
  "state": "complete",
  "results": {
    "company": {
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
      "name": "inn_company",
      "description": "Проверка паспорта РФ и получение ИНН физического лица через Федеральную налоговую службу России (ФНС). Возвращает ИНН, если он найден по введённым паспортным данным.",
      "input_schema": {
        "seria": "string — серия паспорта РФ (4 цифры)",
        "number": "string — номер паспорта РФ (6 цифр)",
        "firstname": "string — имя",
        "lastname": "string — фамилия",
        "secondname": "string — отчество",
        "dob": "string (YYYY-MM-DD) — дата рождения",
        "country": "string (ru)",
        "method": "string (passport_fns)",
        "webhook": "string (URL для webhook)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "company": {
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "innfiz": "string — найденный ИНН физического лица"
                }
              ]
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "seria": "4015",
            "number": "350278",
            "firstname": "Александр",
            "secondname": "Сергеевич",
            "lastname": "Малина",
            "dob": "1990-12-17",
            "country": "ru",
            "method": "passport_fns"
          },
          "webhook": "https://webhook_url/",
          "requestId": "19342f89-2916-4779-b59d-43c012f1a781"
        },
        "response_success": {
          "state": "complete",
          "results": {
            "company": {
              "result": {
                "status": 200,
                "data": [
                  { "innfiz": "7703245603" }
                ]
              }
            }
          }
        },
        "response_empty": {
          "state": "complete",
          "results": {
            "company": {
              "result": {
                "status": 200,
                "data": []
              }
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь прислал паспортные данные (серия, номер, ФИО, дата рождения) или спрашивает 'найти ИНН по паспорту', 'узнать ИНН', 'проверить налоговую регистрацию' — вызывай метод inn_company (passport_fns) и верни найденный ИНН физического лица."
}
```
