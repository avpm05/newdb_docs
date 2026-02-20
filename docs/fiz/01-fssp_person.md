---
title: "fssp_person — проверка физлица по базе ФССП"
description: "API метод NEWDB fssp_person: поиск исполнительных производств по ФИО, дате рождения и региону в базе ФССП."
canonical_url: https://newdb.net/docs/fiz/01-fssp_person/
meta:
  - name: keywords
    content: "NEWDB API, fssp_person, ФССП, проверка должников, исполнительные производства"
  - property: og:title
    content: "Проверка физлица по базе ФССП — метод fssp_person"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода fssp_person для поиска исполнительных производств."
---

# fssp_person — Проверка ФЛ по базе ФССП

POST `https://api.newdb.net/v2`

Метод осуществляет поиск исполнительных производств в ФССП по ФИО, дате рождения и коду региона.

**Рекомендуем также:** комплексная проверка по паспорту — [complex_by_passport](04-complex_by_passport.md).

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "firstname": "string",
    "lastname": "string",
    "secondname": "string",
    "dob": "YYYY-MM-DD",
    "regioncode": "number",
    "country": "ru",
    "method": "fssp_person"
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
    "firstname": "Иванова",
    "lastname": "Алиса",
    "secondname": "Егоровна",
    "dob": "1987-11-27",
    "country": "ru",
    "method": "fssp_person",
    "regioncode": 66
  },
  "webhook": "https://newer.net/whook",
  "requestId": "19342f89-2916-4779-b59d-43c012f1a781"
}
```

## Пример ответа
```json
{
  "params": {
    "firstname": "АЛИСА",
    "lastname": "Иванова",
    "secondname": "Егоровна",
    "dob": "1987-11-27",
    "country": "ru",
    "method": "fssp_person",
    "regioncode": 66
  },
  "webhook": "https://newer.net/whook",
  "requestId": "3122f8c9-08ff-439a-8550-54ca099e3124",
  "datecreated": "2025-11-09 23:58:38",
  "state": "complete",
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "fssp_person": {
      "taskId": "eeaaac06-aacc-45d9-964a-431022fe2fdd",
      "dateupdated": "2025-11-09 20:59:43",
      "result": {
        "status": 200,
        "data": [
          {
            "Debtor": "ИВАНОВА АЛИСА ЕГОРОВНА 27.11.1987 Г. СЕВЕРОУРАЛЬСК СВЕРДЛОВСКАЯ ОБЛАСТЬ",
            "EnforcementProceeding": "88442/25/66049-ИП от 09.09.2025",
            "WritDetails": "Исполнительный лист от 05.09.2025 № 66RS0050#2-19/2025#1 СЕВЕРОУРАЛЬСКИЙ ГОРОДСКОЙ СУД",
            "CompletionDateOrReason": "",
            "Service": "",
            "SubjectAndDebtAmount": "Иные взыскания имущественного характера в пользу физических и юридических лиц Сумма долга: 30000.00 руб. Остаток долга по исполнительному документу: 30000.00 руб.",
            "BailiffDepartment": "Североуральское РОСП 624480, Россия, Свердловская обл., , г. Североуральск, , ул. Ватутина, д. 18, ,",
            "Phone": "+7(34380)2-36-40",
            "BailiffOfficer": "БАРАБАНОВА С. В."
          },
          {
            "Debtor": "ИВАНОВА АЛИСА ЕГОРОВНА 27.11.1987 Г. СЕВЕРОУРАЛЬСК СВЕРДЛОВСКАЯ ОБЛАСТЬ",
            "EnforcementProceeding": "92119/25/66049-ИП от 24.09.2025",
            "WritDetails": "Исполнительный лист от 18.09.2025 № 66RS0050#2-19/2025#3 СЕВЕРОУРАЛЬСКИЙ ГОРОДСКОЙ СУД",
            "CompletionDateOrReason": "",
            "Service": "",
            "SubjectAndDebtAmount": "Иные взыскания имущественного характера в пользу физических и юридических лиц Сумма долга: 40000.00 руб. Остаток долга по исполнительному документу: 40000.00 руб.",
            "BailiffDepartment": "Североуральское РОСП 624480, Россия, Свердловская обл., , г. Североуральск, , ул. Ватутина, д. 18, ,",
            "Phone": "+7(34380)2-36-40",
            "BailiffOfficer": "БАРАБАНОВА С. В."
          },
          {
            "Debtor": "ИВАНОВА АЛИСА ЕГОРОВНА 27.11.1987 СВЕРДЛОВСКАЯ ОБЛ., Г. СЕВЕРОУРАЛЬСК",
            "EnforcementProceeding": "98696/25/66049-ИП от 08.10.2025",
            "WritDetails": "Судебный приказ от 27.03.2025 № 2-1412/2025 СУДЕБНЫЙ УЧАСТОК № 1 СУДЕБНОГО РАЙОНА, В КОТОРОМ СОЗДАН СЕВЕРОУРАЛЬСКИЙ ГОРОДСКОЙ СУД СВЕРДЛОВСКОЙ ОБЛАСТИ 7710140679 Постановление о взыскании исполнительского сбора",
            "CompletionDateOrReason": "",
            "Service": "",
            "SubjectAndDebtAmount": "Задолженность по кредитным платежам (кроме ипотеки) Сумма долга: 244751.96 руб. Остаток долга по исполнительному документу: 228740.15 руб. Исполнительский сбор: 16011.81 руб.",
            "BailiffDepartment": "Североуральское РОСП 624480, Россия, Свердловская обл., , г. Североуральск, , ул. Ватутина, д. 18, ,",
            "Phone": "+7(34380)2-36-40",
            "BailiffOfficer": "БАРАБАНОВА С. В."
          }
        ]
      }
    }
  },
  "finished": 1
}
```

## x-ai (метаданные для AI)
```
{
  "tools": [
    {
      "name": "fssp_person",
      "description": "Проверка физического лица по базе исполнительных производств ФССП России. Возвращает сведения о долгах, судебных приказах и судебных приставах по ФИО, дате рождения и региону.",
      "input_schema": {
        "firstname": "string",
        "lastname": "string",
        "secondname": "string",
        "dob": "string (YYYY-MM-DD)",
        "regioncode": "number",
        "country": "string (ru)",
        "method": "string (fssp_person)",
        "webhook": "string (URL)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "requestId": "string",
        "datecreated": "string (YYYY-MM-DD HH:MM:SS)",
        "state": "string (complete|processing|error)",
        "results": {
          "fssp_person": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "Debtor": "string — ФИО и дата рождения должника",
                  "EnforcementProceeding": "string — Номер и дата исполнительного производства",
                  "WritDetails": "string — Реквизиты исполнительного листа или судебного приказа",
                  "SubjectAndDebtAmount": "string — Сумма долга и тип взыскания",
                  "BailiffDepartment": "string — Отдел судебных приставов",
                  "BailiffOfficer": "string — ФИО пристава-исполнителя",
                  "Phone": "string — Контактный телефон отдела"
                }
              ]
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "firstname": "Алиса",
            "lastname": "Иванова",
            "secondname": "Егоровна",
            "dob": "1987-11-27",
            "regioncode": 66,
            "country": "ru",
            "method": "fssp_person"
          },
          "webhook": "https://newer.net/whook"
        },
        "response": {
          "requestId": "3122f8c9-08ff-439a-8550-54ca099e3124",
          "datecreated": "2025-11-09 23:58:38",
          "state": "complete",
          "results": {
            "fssp_person": {
              "taskId": "eeaaac06-aacc-45d9-964a-431022fe2fdd",
              "dateupdated": "2025-11-09 20:59:43",
              "result": {
                "status": 200,
                "data": [
                  {
                    "Debtor": "ИВАНОВА АЛИСА ЕГОРОВНА 27.11.1987 Г. СЕВЕРОУРАЛЬСК",
                    "EnforcementProceeding": "88442/25/66049-ИП от 09.09.2025",
                    "WritDetails": "Исполнительный лист № 2-19/2025 от 05.09.2025 СЕВЕРОУРАЛЬСКИЙ ГОРОДСКОЙ СУД",
                    "SubjectAndDebtAmount": "Сумма долга: 30000.00 руб.",
                    "BailiffDepartment": "Североуральское РОСП, ул. Ватутина, д. 18",
                    "BailiffOfficer": "БАРАБАНОВА С. В.",
                    "Phone": "+7(34380)2-36-40"
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
  "policy": "Если пользователь спрашивает о долгах, судебных приставах, исполнительных производствах или хочет проверить человека по ФИО и дате рождения — вызывай метод fssp_person и верни сведения из базы ФССП."
}
```
