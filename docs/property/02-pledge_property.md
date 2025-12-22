---
title: "pledge_property — проверка залога по  идентификатору предмета"
description: "Метод NEWDB pledge_property ищет сведения о залогах, лизинге и иных обременениях по  идентификатору предмета в реестре ФНП и Федресурсе."
canonical_url: https://newdb.net/docs/property/02-pledge_property/
meta:
  - name: keywords
    content: "NEWDB API, pledge_property, залог,   идентификатор предмета, ФНП, Федресурс"
  - property: og:title
    content: "Проверка залога по ID— метод pledge_property"
  - property: og:description
    content: "Получите данные ФНП и Федресурса о залоге, лизинге и других обременениях предмета по  идентификатору через API NEWDB."
---

# pledge_property — Проверка залога и обременений по VIN/ID (ФНП + Федресурс)

POST `https://api.newdb.net/v2`

Метод выполняет поиск сведений о залоге, лизинге и других обременениях конкретного предмета по его VIN или идентификатору.  
Используются данные:

- **ФНП** — Реестр уведомлений о залоге движимого имущества;
- **Федресурс** — сообщения о праве залога, договорах лизинга и изменениях к ним.

Поиск осуществляется по параметру `propertyid`, куда можно передать VIN или иной идентификатор предмета залога.

---

## Заголовки

```text
Content-Type: application/json
X-API-KEY: <your_token>
```

## Пример запроса (по VIN/ID)

POST /v2 HTTP/1.1  
Host: api.newdb.net  
Content-Type: application/json  
X-API-KEY: YOUR_TOKEN

```json
{
  "params": {
    "method": "pledge_property",
    "country": "ru",
    "propertyid": "187401"
  },
  "requestId": "a5962f88-2926-4279-b59d-43c023faa495"
}
```

## Пример ответа (укороченный список `subjects`)

```json
{
  "params": {
    "method": "pledge_property",
    "country": "ru",
    "propertyid": "187401",
    "newdb_qid": "EMULIPOwvrO0MygD"
  },
  "requestId": "a5962f88-2926-4279-b59d-43c023faa495",
  "datecreated": "2025-12-22 17:21:15",
  "state": "complete",
  "balance": 7975,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "pledge_property": {
      "result": {
        "status": 200,
        "data": [
          {
            "fnp": [
              {
                "source": "ФНП",
                "registry": "Реестр уведомлений о залоге движимого имущества",
                "message_number_and_date": "2016-000-052966-961 от 11.02.2016",
                "reference_number": "2016-000-052966-961",
                "message_type": "Возникновение залога",
                "pledge_subject_ids_raw": "187401",
                "pledgor": "ОАО \"ГПР №1\"",
                "pledgee": "Акционерный коммерческий банк «Банк Москвы» (открытое акционерное общество)",
                "guid": "174acd3f-c5b9-3d54-b0f8-422381b0f04b",
                "fnp_url": "https://www.reestr-zalogov.ru/search/notification/174acd3f-c5b9-3d54-b0f8-422381b0f04b"
              },
              {
                "source": "ФНП",
                "registry": "Реестр уведомлений о залоге движимого имущества",
                "message_number_and_date": "2021-006-140820-013 от 05.07.2021",
                "reference_number": "2021-006-140820-013",
                "message_type": "Возникновение залога",
                "pledge_subject_ids_raw": "XUS22270280002514, 15218-1, 15274-1, ...",
                "pledgor": "АКЦИОНЕРНОЕ ОБЩЕСТВО \"МОРДОВЦЕМЕНТ\"",
                "pledgee": "Публичное акционерное общество «Сбербанк России»",
                "guid": "c65096bd-92e1-33e4-9a3c-5632bac143c7",
                "fnp_url": "https://www.reestr-zalogov.ru/search/notification/c65096bd-92e1-33e4-9a3c-5632bac143c7",
                "json_extra": {
                  "registrationTime": "2021-07-05T12:15:00",
                  "referenceNumber": "2021-006-140820-013",
                  "guid": "c65096bd-92e1-33e4-9a3c-5632bac143c7",
                  "pledgors": [
                    "АКЦИОНЕРНОЕ ОБЩЕСТВО \"МОРДОВЦЕМЕНТ\""
                  ],
                  "pledgees": [
                    "Публичное акционерное общество «Сбербанк России»"
                  ],
                  "subjects": [
                    "XUS22270280002514",
                    "15218-1",
                    "15274-1",
                    "15276-1",
                    "15275-1",
                    "15278-1",
                    "15279-1",
                    "15282-1",
                    "15283-1",
                    "15286-1"
                  ],
                  "fnpUrl": "https://www.reestr-zalogov.ru/search/notification/c65096bd-92e1-33e4-9a3c-5632bac143c7"
                }
              }
            ],
            "fedresurs": [
              {
                "source": "Федресурс",
                "message_number_and_date": "15261912 от 18.04.2023",
                "message_number": "15261912",
                "message_url": "https://fedresurs.ru/sfactmessages/1636ff6c-f774-4c26-bc2e-147e57305aaa",
                "message_type": "Заключение договора финансовой аренды (лизинга)",
                "lessee": "ООО \"АОН+\"",
                "lessor": "Сведения скрыты",
                "found_in_message": "... 1104338000073, ИНН: 4318004332 Договор: 08634-КРВ-23-АМ-Л от 10.03.2023 Предмет финансовой аренды: , 0106013 Специализированная техника, СТ Основной договор: 187401 ...",
                "links": [
                  {
                    "text": "15261912 от 18.04.2023",
                    "url": "https://fedresurs.ru/sfactmessages/1636ff6c-f774-4c26-bc2e-147e57305aaa"
                  }
                ],
                "encumbrance_guid": "1636ff6c-f774-4c26-bc2e-147e57305aaa",
                "encumbrance_publish_date": "2023-04-18T12:00:30.1",
                "encumbrance_type": "FinancialLeaseContract",
                "encumbrance_highlights_text": "1104338000073, ИНН: 4318004332\nДоговор: 08634-КРВ-23-АМ-Л от 10.03.2023\nПредмет финансовой аренды: , 0106013 Специализированная техника, СТ\nОсновной договор: 187401",
                "encumbrance_message_url": "https://fedresurs.ru/message/1636ff6c-f774-4c26-bc2e-147e57305aaa"
              },
              {
                "source": "Федресурс",
                "message_number_and_date": "30997687 от 01.10.2025",
                "message_number": "30997687",
                "message_url": "https://fedresurs.ru/sfactmessages/aa2f2251-7511-46dd-ab36-cfdb0529ba92",
                "message_type": "Изменение договора финансовой аренды (лизинга)",
                "lessee": "ООО \"АОН+\"",
                "lessor": "Сведения скрыты",
                "found_in_message": "... 4318004332 Договор: 08634-КРВ-23-АМ-Л от 10.03.2023 Предмет финансовой аренды: CLG855HZHPL788031, 0106013 Специализированная техника, СТ Основной договор: 187401 ...",
                "links": [
                  {
                    "text": "30997687 от 01.10.2025",
                    "url": "https://fedresurs.ru/sfactmessages/aa2f2251-7511-46dd-ab36-cfdb0529ba92"
                  }
                ],
                "encumbrance_guid": "aa2f2251-7511-46dd-ab36-cfdb0529ba92",
                "encumbrance_publish_date": "2025-10-01T05:08:22.487244",
                "encumbrance_type": "ChangeFinancialLeaseContract2",
                "encumbrance_highlights_text": "4318004332\nДоговор: 08634-КРВ-23-АМ-Л от 10.03.2023\nПредмет финансовой аренды: CLG855HZHPL788031, 0106013 Специализированная техника, СТ\nОсновной договор: 187401",
                "encumbrance_message_url": "https://fedresurs.ru/message/aa2f2251-7511-46dd-ab36-cfdb0529ba92"
              }
            ],
            "fnp_urls": [
              "https://www.reestr-zalogov.ru/search/notification/174acd3f-c5b9-3d54-b0f8-422381b0f04b",
              "https://www.reestr-zalogov.ru/search/notification/c65096bd-92e1-33e4-9a3c-5632bac143c7"
            ]
          }
        ]
      },
      "dateupdated": "2025-12-22 17:21:29"
    }
  }
}
```

## Пример ответа (данные не найдены)

```json
{
  "state": "complete",
  "results": {
    "pledge_property": {
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
      "name": "pledge_property",
      "description": "Проверка залогов, лизинга и иных обременений конкретного предмета по VIN или идентификатору. Используются данные ФНП (реестр залогов движимого имущества) и Федресурса.",
      "input_schema": {
        "propertyid": "string — VIN или иной идентификатор предмета залога",
        "country": "string (ru)",
        "method": "string (pledge_property)",
        "webhook": "string (URL для webhook, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "pledge_property": {
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
                      "pledge_subject_ids_raw": "string — идентификатор(ы) предмета залога (VIN/ID)",
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
            "method": "pledge_property",
            "country": "ru",
            "propertyid": "187401"
          },
          "requestId": "a5962f88-2926-4279-b59d-43c023faa495"
        },
        "response_with_data": {
          "state": "complete",
          "results": {
            "pledge_property": {
              "result": {
                "status": 200,
                "data": [
                  {
                    "fnp": [
                      {
                        "source": "ФНП",
                        "message_number_and_date": "2016-000-052966-961 от 11.02.2016",
                        "pledgor": "ОАО \"ГПР №1\"",
                        "pledgee": "Акционерный коммерческий банк «Банк Москвы» (открытое акционерное общество)"
                      }
                    ],
                    "fedresurs": [
                      {
                        "source": "Федресурс",
                        "message_number_and_date": "15261912 от 18.04.2023",
                        "message_type": "Заключение договора финансовой аренды (лизинга)",
                        "lessee": "ООО \"АОН+\""
                      }
                    ]
                  }
                ]
              }
            }
          }
        },
        "response_empty": {
          "state": "complete",
          "results": {
            "pledge_property": {
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
  "policy": "Если пользователь хочет проверить конкретный предмет на залог, лизинг или иное обременение в ФНП и Федресурсе — используй метод pledge_property и верни найденные уведомления и сообщения."
}
```
