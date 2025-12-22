---
title: "complex_by_passport — комплексная проверка по паспорту"
description: "Метод NEWDB complex_by_passport объединяет проверки МВД, ФНС и ФССП для полного анализа физлица по данным паспорта."
canonical_url: https://newdb.net/docs/fiz/04-complex_by_passport/
meta:
  - name: keywords
    content: "NEWDB API, complex_by_passport, композитная проверка, ФНС, МВД, ФССП"
  - property: og:title
    content: "Комплексная проверка по паспорту — метод complex_by_passport"
  - property: og:description
    content: "Единый API запрос, объединяющий проверки паспорта, ИНН и исполнительных производств."
---

# complex_by_passport — Комплексная проверка по данным паспорта

POST `https://api.newdb.net/v2`

Метод выполняет комплексную проверку физического лица по серии и номеру паспорта РФ.  
Выполняются следующие этапы:

- проверка паспорта на действительность по линии МВД (действительный / недействительный / данные не найдены),
- проверка паспорта и получение ИНН по линии ФНС России,
- поиск исполнительных производств  ФССП

---

## Заголовки

 

Content-Type: application/json
X-API-KEY: <your_token>

 

## Входная схема (request)

```json
{
  "params": {
    "seria": "string (серия паспорта)",
    "number": "string (номер паспорта)",
    "firstname": "string",
    "lastname": "string",
    "secondname": "string",
    "dob": "YYYY-MM-DD",
    "country": "ru",
    "regioncode": "number",
    "method": "complex_by_passport"
  },
  "webhook": "https://your.host/whook",
  "requestId": "optional-string"
}
```

---

## Пример запроса

```json
POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
  "params": {
    "seria": "1234",
    "number": "123456",
    "method": "complex_by_passport",
    "firstname": "Петр",
    "secondname": "Петрович",
    "lastname": "Иванов",
    "dob": "1987-01-08",
    "country": "ru",
    "regioncode": 77
  },
  "requestId": "869c6cd0-d07c239b-78def834-bd6befec"
}
```

---

## Пример ответа

```json
{
  "params": {
    "seria": "1234",
    "number": "123456",
    "method": "complex_by_passport",
    "firstname": "Петр",
    "secondname": "Петрович",
    "lastname": "Иванов",
    "dob": "1987-01-08",
    "country": "ru",
    "regioncode": 77
  },
  "requestId": "869c6cd0-d07c239b-78def834-bd6befec",
  "datecreated": "2025-11-28 17:06:59",
  "state": "complete",
  "balance": 9958,
  "steps": {
    "fssp_person": {
      "status": "complete",
      "error": null,
      "requestId": "c8916c2c-349c-4d6e-819c-76603b27fd04"
    },
    "passport_mvd": {
      "status": "complete",
      "error": null,
      "requestId": "5d37cf3f-b8be-49e1-b9de-dc9d9269b916"
    },
    "passport_fns": {
      "status": "complete",
      "error": null,
      "requestId": "d3efeede-4d6a-494e-ade0-99a83cd0220a"
    }
  },
  "results": {
    "passport_fns": {
      "taskId": "1c1ccaab-9c8a-458c-9fdb-46c2288e01d7",
      "result": {
        "status": 200,
        "data": [
          {
            "innfiz": "272116001938"
          }
        ]
      },
      "dateupdated": "2025-11-28 17:07:20"
    },
    "passport_mvd": {
      "taskId": "d6327b35-22c7-4e2b-b308-48e2ca8eef8a",
      "dateupdated": "2025-11-28 17:07:36",
      "result": {
        "status": 200,
        "data": [
          {
            "doc_status": "Действительный"
          }
        ]
      }
    },
    "fssp_person": {
      "taskId": "0acb4ac8-abb2-4600-a250-396de8fc6799",
      "dateupdated": "2025-11-28 17:07:39",
      "result": {
        "status": 200,
        "data": []
      }
    }
  },
  "finished_at": "2025-11-28 17:07:42"
}
```

---

## x-ai (метаданные для AI)

```json
{
  "tools": [
    {
      "name": "complex_by_passport",
      "description": "Комплексная проверка человека по серии и номеру паспорта РФ. Выполняет проверки МВД (действительность паспорта), ФНС (ИНН), ФССП (исполнительные производства) и сверку ФИО/даты рождения.",
      "input_schema": {
        "seria": "string — серия паспорта",
        "number": "string — номер паспорта",
        "firstname": "string",
        "lastname": "string",
        "secondname": "string",
        "dob": "string (YYYY-MM-DD)",
        "country": "string (ru)",
        "regioncode": "number",
        "method": "string (complex_by_passport)",
        "webhook": "string (URL)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "passport_mvd": {
            "taskId": "string",
            "dateupdated": "string",
            "result": {
              "status": "number",
              "data": [
                { "doc_status": "string — статус паспорта" }
              ]
            }
          },
          "passport_fns": {
            "taskId": "string",
            "dateupdated": "string",
            "result": {
              "status": "number",
              "data": [
                { "innfiz": "string — ИНН физического лица" }
              ]
            }
          },
          "fssp_person": {
            "taskId": "string",
            "dateupdated": "string",
            "result": {
              "status": "number",
              "data": "array — данные по исполнительным производствам"
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "seria": "1234",
            "number": "123456",
            "firstname": "Петр",
            "secondname": "Петрович",
            "lastname": "Иванов",
            "dob": "1987-01-08",
            "country": "ru",
            "regioncode": 77,
            "method": "complex_by_passport"
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь предоставляет серию, номер паспорта , ФИО, регион проживанивания , дату рождения — вызывай метод complex_by_passport, который возвращает проверки по МВД, ФНС и ФССП."
}
```

---

 
