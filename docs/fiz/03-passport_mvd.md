---
title: "passport_mvd — проверка паспорта РФ на действительность"
description: "Метод NEWDB passport_mvd подтверждает действительность паспорта РФ по серии, номеру и ФИО через базы МВД."
meta:
  - name: keywords
    content: "NEWDB API, passport_mvd, проверка паспорта, МВД, верификация личности"
  - property: og:title
    content: "Проверка паспорта РФ — метод passport_mvd"
  - property: og:description
    content: "Спецификация запроса, заголовков и ответов метода passport_mvd для подтверждения действительности паспорта."
---

# passport_mvd — Проверка паспорта РФ на действительность

POST `https://api.newdb.net/v2`

Проверяет паспорт РФ по серии/номеру и фамилии, имени.

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
    "dob": "YYYY-MM-DD",
    "method": "passport_mvd",
    "country": "ru"
  },
  "webhook": "https://your.host/whook",
  "requestId": "optional-string"
}
}
```

## Пример запроса

POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN
```
{
  "params": {
    "seria": "0802",
    "number": "649286",
    "firstname": "Петр",
    "lastname": "Семенов",
    "secondname": "Николаевич",
    "dob": "1937-01-03",
    "country": "ru",
    "method": "passport_mvd"
  },
  "webhook": "https://webhook_url/",
  "requestId": "19342f89-2916-4779-b59d-43c012f1a781"
}
```

## Пример ответа
```json
{
    "params": {
        "seria": "0802",
        "number": "649116",
        "method": "passport_mvd",
        "firstname": "Петр",
        "lastname": "Иванов",
    },
    "requestId": "32ec1efd-3f6a-76a2-9c4b-68cbf4b52089",
    "token": "6fa1aa70-ecfe-41f5-b56e-d9da2b79fc90",
    "tasks": 203,
    "is_repeat": false,
    "results": {
        "passport_mvd": {
            "taskId": "a8e29673-2978-4e28-95a1-a42d0ad4328e",
            "dateupdated": "2025-11-05 08:49:13",
            "result": {
                "status": 200,
                "data": [
                    {
                        "status": "Действительный"
                    }
                ]
            }
        }
    },
    "finished": 1,
    "state": "complete",
    "datecreated": "2025-11-02 22:48:00"
}
```




## x-ai (метаданные для AI)
```json
{
  "tools": [
    {
      "name": "passport_check",
      "description": "Проверка паспорта РФ по серии и номеру на действительность",
      "input_schema": {
        "seria": "string (4 цифры)",
        "number": "string (6 цифр)",
        "firstname": "string (optional)",
        "lastname": "string (optional)",
        "secondname": "string (optional)",
        "dob": "string (YYYY-MM-DD)",
        "country": "string ('ru')",
        "method": "string ('passport_mvd')",
        "webhook": "string (optional, URL)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|in_progress|error)",
        "results": {
          "passport_mvd": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "status": "string ('Действительный' | 'Недействительный')",
             
                  "error": "string (optional — причина ошибки)",
                  
                }
              ]
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "seria": "0802",
            "number": "649286",
            "firstname": "Петр",
            "lastname": "Семенов",
            "secondname": "Николаевич",
            "dob": "1937-01-03",
            "country": "ru",
            "method": "passport_mvd"
          }
        },
        "response_valid": {
          "state": "complete",
          "results": {
            "passport_mvd": {
              "result": {
                "status": 200,
                "data": [{ "status": "Действительный" }]
              }
            }
          }
        },
        "response_invalid": {
          "state": "complete",
          "results": {
            "passport_mvd": {
              "result": {
                "status": 500,
                "data": [
                  {
                    "error": "Service unavailable",
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
  "policy": "Если пользователь просит проверить паспорт РФ, запрашивай серию и номер, фамилию и имя. Затем вызывай passport_mvd  method='passport_mvd' и верни статус действия паспорта. Если серия/номер не указаны — вежливо запроси их."
}

```
