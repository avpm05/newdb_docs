---
title: "pledge_vin — проверка залога по VIN"
description: "Метод NEWDB pledge_vin ищет сведения о залогах и иных обременениях по VIN в реестре ФНП и Федресурсе."
canonical_url: https://newdb.net/docs/property/03-pledge_vin/
meta:
  - name: keywords
    content: "NEWDB API, pledge_vin, залог, VIN, ФНП, Федресурс"
  - property: og:title
    content: "Проверка залога по VIN — метод pledge_vin"
  - property: og:description
    content: "Получите данные ФНП и Федресурса о залоге, лизинге и обременениях транспортного средства по VIN через API NEWDB."
---

# pledge_vin — Проверка залога и обременений по VIN (ФНП + Федресурс)

POST `https://api.newdb.net/v2`

Метод выполняет поиск сведений о залоге, лизинге и других обременениях конкретного транспортного средства по его VIN.  
Используются данные:

- **ФНП** — Реестр уведомлений о залоге движимого имущества;
- **Федресурс** — сообщения о праве залога, договорах лизинга и изменениях.

Поиск осуществляется по параметру `vin`.

---

## Заголовки

```text
Content-Type: application/json
X-API-KEY: <your_token>
```

## Пример запроса

POST /v2 HTTP/1.1  
Host: api.newdb.net  
Content-Type: application/json  
X-API-KEY: YOUR_TOKEN

```json
{
  "params": {
    "method": "pledge_vin",
    "country": "ru",
    "vin": "JTEHD21A850036287"
  },
  "requestId": "a5962f88-2926-4279-b59d-43c023faa195"
}
```

## Пример ответа

```json
{
  "params": {
    "method": "pledge_vin",
    "country": "ru",
    "vin": "JTEHD21A850036287",
    "newdb_qid": "EK0LIPKclrO0MygC"
  },
  "requestId": "a5962f88-2926-4279-b59d-43c023faa195",
  "datecreated": "2025-12-22 17:10:18",
  "state": "complete",
  "balance": 7977,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "pledge_vin": {
      "result": {
        "status": 200,
        "data": [
          {
            "fnp": [
              {
                "source": "ФНП",
                "registry": "Реестр уведомлений о залоге движимого имущества",
                "message_number_and_date": "2015-000-291842-833 от 29.01.2015",
                "reference_number": "2015-000-291842-833",
                "message_type": "Возникновение залога",
                "pledge_subject_ids_raw": "JTEHD21A850036287",
                "pledgor": "Игорь Юрьевич Семенов",
                "pledgee": "АКЦИОНЕРНЫЙ БАНК \"ИНТЕРПРОГРЕССБАНК\" (ЗАКРЫТОЕ АКЦИОНЕРНОЕ ОБЩЕСТВО)",
                "guid": "e612c5ce-2e10-3d20-9112-cf520df444ac",
                "fnp_url": "https://www.reestr-zalogov.ru/search/notification/e612c5ce-2e10-3d20-9112-cf520df444ac",
                "json_extra": {
                  "registrationTime": "2015-01-29T16:40:08",
                  "referenceNumber": "2015-000-291842-833",
                  "guid": "e612c5ce-2e10-3d20-9112-cf520df444ac",
                  "pledgors": [
                    "Игорь Юрьевич Семенов"
                  ],
                  "pledgees": [
                    "АКЦИОНЕРНЫЙ БАНК \"ИНТЕРПРОГРЕССБАНК\" (ЗАКРЫТОЕ АКЦИОНЕРНОЕ ОБЩЕСТВО)"
                  ],
                  "subjects": [
                    "JTEHD21A850036287"
                  ],
                  "fnpUrl": "https://www.reestr-zalogov.ru/search/notification/e612c5ce-2e10-3d20-9112-cf520df444ac"
                }
              }
            ],
            "fedresurs": [],
            "fnp_urls": [
              "https://www.reestr-zalogov.ru/search/notification/e612c5ce-2e10-3d20-9112-cf520df444ac"
            ]
          }
        ]
      },
      "dateupdated": "2025-12-22 17:10:33"
    }
  }
}
```

## Пример ответа (данные не найдены)

```json
{
  "state": "complete",
  "results": {
    "pledge_vin": {
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
      "name": "pledge_vin",
      "description": "Проверка залогов, лизинга и иных обременений транспортного средства по VIN. Используются данные ФНП (реестр залогов движимого имущества) и Федресурса.",
      "input_schema": {
        "vin": "string — VIN транспортного средства",
        "country": "string (ru)",
        "method": "string (pledge_vin)",
        "webhook": "string (URL для webhook, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "pledge_vin": {
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "fnp": [
                    {
                      "source": "string — источник (ФНП)",
                      "registry": "string — название реестра",
                      "message_number_and_date": "string — номер и дата уведомления",
                      "reference_number": "string — референс-номер уведомления",
                      "message_type": "string — тип сообщения (например, Возникновение залога)",
                      "pledge_subject_ids_raw": "string — VIN",
                      "pledgor": "string — залогодатель (ФИО/организация)",
                      "pledgee": "string — залогодержатель (банк/организация)",
                      "guid": "string — GUID уведомления",
                      "fnp_url": "string — ссылка на уведомление в реестре ФНП"
                    }
                  ],
                  "fedresurs": [
                    {
                      "source": "string — источник (Федресурс)",
                      "message_number_and_date": "string — номер и дата сообщения",
                      "message_number": "string — номер сообщения",
                      "message_url": "string — ссылка на карточку сообщения",
                      "message_type": "string — тип сообщения (лизинг, залог, прочее)",
                      "lessee": "string — лизингополучатель, если есть",
                      "lessor": "string — лизингодатель/кредитор, если есть",
                      "found_in_message": "string — фрагмент текста, по которому найдено совпадение",
                      "links": [
                        {
                          "text": "string — текст ссылки",
                          "url": "string — URL сообщения"
                        }
                      ],
                      "encumbrance_guid": "string — GUID обременения",
                      "encumbrance_publish_date": "string — дата публикации (ISO)",
                      "encumbrance_type": "string — тип обременения",
                      "encumbrance_message_url": "string — ссылка на сообщение об обременении"
                    }
                  ],
                  "fnp_urls": [
                    "string — список ссылок на уведомления ФНП"
                  ]
                }
              ]
            }
          }
        }
      },
      "example": {
        "request": {
          "params": {
            "method": "pledge_vin",
            "country": "ru",
            "vin": "JTEHD21A850036287"
          },
          "requestId": "a5962f88-2926-4279-b59d-43c023faa195"
        },
        "response_with_data": {
          "state": "complete",
          "results": {
            "pledge_vin": {
              "result": {
                "status": 200,
                "data": [
                  {
                    "fnp": [
                      {
                        "source": "ФНП",
                        "message_number_and_date": "2015-000-291842-833 от 29.01.2015",
                        "pledgor": "Игорь Юрьевич Семенов",
                        "pledgee": "АКБ \"ИНТЕРПРОГРЕССБАНК\""
                      }
                    ],
                    "fedresurs": []
                  }
                ]
              }
            }
          }
        },
        "response_empty": {
          "state": "complete",
          "results": {
            "pledge_vin": {
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
  "policy": "Если пользователь хочет проверить транспортное средство по VIN на залог, лизинг или иное обременение в ФНП и Федресурсе — используй метод pledge_vin и верни найденные уведомления и сообщения."
}
```

