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
    "inn": "3906988988",
    "country": "ru",
    "method": "bankrot_legal"
  },
  "requestId": "a5962f99-2916-4779-b52d-43c123faa822"
}
```

## Пример ответа

```json
{
  "params": {
    "inn": "3906988988",
    "country": "ru",
    "method": "bankrot_legal"
  },
  "requestId": "a5962f99-2916-4779-b52d-43c123faa822",
  "datecreated": "2026-03-21 23:23:12",
  "state": "complete",
  "balance": 9687,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "bankrot_legal": {
      "result": {
        "status": 200,
        "data": [
          {
            "bankruptcy": [
              {
                "case_number": "А21-11927/2025",
                "case_url": "https://fedresurs.ru/legalcases/7fbe07fa-5a5c-4f1c-92d4-b79e5eaf259c",
                "status": "Конкурсное производство",
                "messages": [
                  {
                    "message_info": "22080695 от 21.03.2026",
                    "url": "https://fedresurs.ru/bankruptmessages/c5b36afc-ede4-45dd-8b37-54f053327255",
                    "type": "Сообщение о судебном акте"
                  },
                  {
                    "message_info": "22010926 от 16.03.2026",
                    "url": "https://fedresurs.ru/bankruptmessages/5081cc01-0016-403d-9dc0-b6c51fad05da",
                    "type": "Сообщение о результатах проведения собрания кредиторов"
                  },
                  {
                    "message_info": "22005113 от 16.03.2026",
                    "url": "https://fedresurs.ru/bankruptmessages/403f7fc0-a72b-4233-b8e7-7cab05bd82e9",
                    "type": "Сообщение о наличии или об отсутствии признаков преднамеренного или фиктивного банкротства"
                  }
                ]
              }
            ],
            "commmon": {
              "type": "company",
              "name_or_fio": "ООО \"УК \"РЕЗУЛЬТАТ\"",
              "inn": "3906988988",
              "reg_number_type": "ОГРН",
              "reg_number": "1163926066303",
              "activity": "Деятельность по управлению финансово-промышленными группами",
              "address": "236006, КАЛИНИНГРАДСКАЯ ОБЛАСТЬ, Г. КАЛИНИНГРАД, УЛ. ЯЛТИНСКАЯ, Д. 134",
              "status": "В отношении юридического лица в деле о несостоятельности (банкротстве) введено наблюдение",
              "details_url": "https://fedresurs.ru/companies/6ba277d4-899f-4ee9-a19f-3e443e2b879a"
            },
            "encumbrances": [],
            "publications": [
              {
                "category": "О лице",
                "number_date": "22080695 от 21.03.2026",
                "title": "Сообщение о судебном акте. о признании должника банкротом и открытии конкурсного производства",
                "url": "https://fedresurs.ru/bankruptmessages/c5b36afc-ede4-45dd-8b37-54f053327255"
              },
              {
                "category": "О лице",
                "number_date": "22010926 от 16.03.2026",
                "title": "Сообщение о результатах проведения собрания кредиторов",
                "url": "https://fedresurs.ru/bankruptmessages/5081cc01-0016-403d-9dc0-b6c51fad05da"
              },
              {
                "category": "О лице",
                "number_date": "22005113 от 16.03.2026",
                "title": "Сообщение о наличии или об отсутствии признаков преднамеренного или фиктивного банкротства",
                "url": "https://fedresurs.ru/bankruptmessages/403f7fc0-a72b-4233-b8e7-7cab05bd82e9"
              }
            ]
          }
        ]
      },
      "taskId": "2232ad0e-5156-4fe8-b610-91c545c2d907",
      "dateupdated": "2026-03-21 23:23:38"
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

## Поля `bankruptcy[]`

| Поле | Описание |
|------|----------|
| `case_number` | Номер дела о банкротстве |
| `case_url` | Ссылка на карточку дела или подборку материалов в источнике |
| `status` | Текущая стадия процедуры банкротства по делу |
| `messages` | Список связанных сообщений по конкретному делу |

## Поля `bankruptcy[].messages[]`

| Поле | Описание |
|------|----------|
| `message_info` | Номер и дата сообщения |
| `url` | Ссылка на публикацию в Федресурсе |
| `type` | Тип сообщения |

## Поля `commmon`

| Поле | Описание |
|------|----------|
| `type` | Тип субъекта. Для юрлица обычно `company` |
| `name_or_fio` | Наименование юридического лица |
| `inn` | ИНН компании |
| `reg_number_type` | Тип регистрационного номера, например `ОГРН` |
| `reg_number` | Регистрационный номер компании |
| `activity` | Основной вид деятельности |
| `address` | Адрес компании |
| `status` | Статус компании или формулировка статуса банкротной процедуры |
| `details_url` | Ссылка на карточку компании в Федресурсе |

## Поля `publications[]`

| Поле | Описание |
|------|----------|
| `category` | Категория публикации |
| `number_date` | Номер и дата публикации |
| `title` | Заголовок публикации |
| `url` | Ссылка на публикацию |

## Пример ответа (данные не найдены)

```json
{
  "state": "complete",
  "results": {
    "bankrot_legal": {
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
              "data": [
                {
                  "bankruptcy": [
                    {
                      "case_number": "string — номер дела",
                      "case_url": "string — ссылка на дело",
                      "status": "string — стадия процедуры",
                      "messages": [
                        {
                          "message_info": "string — номер и дата сообщения",
                          "url": "string — ссылка на публикацию",
                          "type": "string — тип сообщения"
                        }
                      ]
                    }
                  ],
                  "commmon": {
                    "type": "string — тип субъекта",
                    "name_or_fio": "string — наименование компании",
                    "inn": "string — ИНН",
                    "reg_number_type": "string — тип регистрационного номера",
                    "reg_number": "string — регистрационный номер",
                    "activity": "string — основной вид деятельности",
                    "address": "string — адрес",
                    "status": "string — текущий статус",
                    "details_url": "string — ссылка на карточку"
                  },
                  "encumbrances": "array — найденные обременения, если есть",
                  "publications": [
                    {
                      "category": "string — категория публикации",
                      "number_date": "string — номер и дата",
                      "title": "string — заголовок публикации",
                      "url": "string — ссылка на публикацию"
                    }
                  ]
                }
              ]
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
