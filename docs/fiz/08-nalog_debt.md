---
title: "nalog_debt — проверка налоговой задолженности физлица по ИНН"
description: "Метод NEWDB nalog_debt проверяет задолженность физического лица по налогам и сборам по ИНН."
canonical_url: https://newdb.net/docs/fiz/08-nalog_debt/
meta:
  - name: keywords
    content: "NEWDB API, nalog_debt, налоговая задолженность, долги, ИНН, физлицо"
  - property: og:title
    content: "Налоговая задолженность физлица по ИНН — метод nalog_debt"
  - property: og:description
    content: "Проверка налоговых долгов физического лица по ИНН через API NEWDB."
---

# nalog_debt — Проверка налоговой задолженности по ИНН

POST `https://api.newdb.net/v2`

Метод выполняет проверку налоговой задолженности физического лица по ИНН. В ответе возвращаются сведения по найденной задолженности, а также технические данные выполнения запроса.

**Рекомендуем также:** проверка исполнительных производств — [fssp_person](01-fssp_person.md), проверка банкротства — [fedresurs_bankrot](05-fedresurs_bankrot.md).

## Заголовки
```http
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "inn": "string (ИНН физического лица)",
    "email": "string (email для проверки)",
    "country": "ru",
    "method": "nalog_debt"
  },
  "webhook": "https://your.host/whook",
  "requestId": "optional-string"
}
```

## Параметры

- `inn` — ИНН физического лица.
- `email` — email, используемый при выполнении проверки.
- `country` — код страны. Для РФ используйте `ru`.
- `method` — имя метода, всегда `nalog_debt`.

## Пример запроса
```http
POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
  "params": {
    "inn": "270392288605",
    "email": "pa@mail.ru",
    "country": "ru",
    "method": "nalog_debt"
  },
  "requestId": "a5962f88-2916-4779-b59d-43c023faa899"
}
```

## Пример ответа
```json
{
  "params": {
    "inn": "270392288605",
    "email": "pa@mail.ru",
    "country": "ru",
    "method": "nalog_debt"
  },
  "requestId": "a5962f88-2916-4779-b59d-43c023faa899",
  "datecreated": "2026-03-15 23:15:44",
  "state": "complete",
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "nalog_debt": {
      "taskId": "nalog-debt-local-task",
      "dateupdated": "2026-03-15 23:15:59",
      "result": {
        "status": 200,
        "data": [
          {
            "debt": {
              "total": "0.00",
              "items": []
            },
            "form": {
              "inn": "270392288605",
              "email": "pa@mail.ru"
            },
            "http": {
              "status": 200
            },
            "network": {
              "final_url": "https://avtonalogi.ru/"
            },
            "page": {
              "title": "Проверка задолженности"
            },
            "request": {
              "method": "nalog_debt"
            }
          }
        ]
      }
    }
  },
  "finished": 1
}
```

## Что возвращает метод

- `results.nalog_debt.result.status` — HTTP-статус выполнения проверки.
- `results.nalog_debt.result.data[].debt` — сведения о найденной задолженности.
- `results.nalog_debt.result.data[].form` — данные, переданные в форму проверки.
- `results.nalog_debt.result.data[].http` — технические сведения HTTP-запроса.
- `results.nalog_debt.result.data[].network` — сетевые метаданные выполнения.
- `results.nalog_debt.result.data[].page` — сведения о странице/источнике.
- `results.nalog_debt.result.data[].request` — параметры исполненного запроса.

## x-ai (метаданные для AI)
```json
{
  "tools": [
    {
      "name": "nalog_debt",
      "description": "Проверка налоговой задолженности физического лица по ИНН. Возвращает найденные долги и технические детали выполнения проверки.",
      "input_schema": {
        "inn": "string — ИНН физического лица",
        "email": "string — email для выполнения проверки",
        "country": "string (ru)",
        "method": "string (nalog_debt)",
        "webhook": "string (URL, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "nalog_debt": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "debt": "object — сведения о задолженности",
                  "form": "object — отправленные данные формы",
                  "http": "object — HTTP-метаданные",
                  "network": "object — сетевые метаданные",
                  "page": "object — сведения о странице результата",
                  "request": "object — исполненный запрос"
                }
              ]
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "inn": "270392288605",
            "email": "pa@mail.ru",
            "country": "ru",
            "method": "nalog_debt"
          },
          "requestId": "a5962f88-2916-4779-b59d-43c023faa899"
        },
        "response": {
          "state": "complete",
          "results": {
            "nalog_debt": {
              "result": {
                "status": 200,
                "data": [
                  {
                    "debt": {
                      "total": "0.00",
                      "items": []
                    }
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
  "policy": "Если пользователь хочет проверить налоговую задолженность физического лица по ИНН, долги по налогам, задолженность перед ФНС или налоговые начисления физлица — используй метод nalog_debt."
}
```
