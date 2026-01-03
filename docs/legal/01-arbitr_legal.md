---
title: "arbitr_legal — арбитражные дела юрлиц (КАД)"
description: "Метод arbitr_legal находит арбитражные дела по ИНН юридического лица, включая участников, статус и судебные акты. На основе анализа PDF текста выделяются суммы , суть дел, проивзодится классификация дела (споры, банкротсво, имущество, налоги и др)"
canonical_url: https://newdb.net/docs/legal/01-arbitr_legal/
meta:
  - name: keywords
    content: "NEWDB API, arbitr_legal, арбитражные дела, КАД, арбитраж, юрлица, суд"
  - property: og:title
    content: "Арбитражные дела юрлиц — метод arbitr_legal"
  - property: og:description
    content: "Получите сведения об арбитражных делах юридического лица из КАД по ИНН через API NEWDB."
---

# arbitr_legal — Проверка арбитражных дел (юрлица, КАД)

POST `https://api.newdb.net/v2`

Метод обеспечивает поиск и анализ зарегистрированных в системе КАД (kad.arbitr.ru) арбитражных дел участия юридического лица (идентификация по ИНН) со следующими сведениями: процессуальный статус дела, состав участников судопроизводства, комплект судебных актов и хронология судебных действий. На основе автоматизированного анализа судебной документации в формате PDF осуществляется: выделение денежных требований и санкций, определение существа споров, классификация дела по категориям (договорные споры, банкротство, имущественные претензии, налоговые доначисления и иные категории), выделение применимого законодательства и юридических оснований для вынесения судебного решения"

---

## Заголовки

Content-Type: application/json  
X-API-KEY: <your_token>

---

## Входная схема (request)

```json
{
  "params": {
    "inn": "string (ИНН юрлица)",
    "country": "string (ru)",
    "method": "arbitr_legal"
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
    "inn": "7707332613",
    "country": "ru",
    "method": "arbitr_legal"
  },
  "requestId": "a5962f88-2916-5779-b59d-43c023faa913"
}
```

---

## Пример ответа

```json
{
  "params": {
    "inn": "7707332613",
    "country": "ru",
    "method": "arbitr_legal",
    "newdb_qid": "ELwLIIfhofu3MygC"
  },
  "requestId": "a5962f88-2916-5779-b59d-43c023faa913",
  "datecreated": "2026-01-02 18:51:49",
  "state": "complete",
  "balance": 9891,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "arbitr_legal": {
      "result": {
        "status": 200,
        "data": [
          {
            "case_number": "А40-283685/2023",
            "status": "Рассмотрение дела завершено",
            "participants": {
              "plaintiffs": [
                {
                  "name": "Филиал № 10 Отделения Фонда пенсионного и социального страхования РФ по Москве и МО",
                  "address": "125375, Россия, г. Москва, г. Москва, ул. б-р. Тверской, д. 18 строение 1"
                }
              ],
              "defendants": [
                {
                  "name": "ООО \"АПЕКС КОНСАЛТ\"",
                  "address": "127473, Россия, г Москва, г. Москва, переулок 1-й Самотечный, д. 2 строение 2, офис 3"
                }
              ],
              "third_parties": [],
              "others": []
            },
            "judges": [
              {
                "court": "АС города Москвы",
                "name": "Поздняков В. Д."
              }
            ],
            "acts": [
              {
                "date": "06.12.2023",
                "type": "Судебный приказ; Иск удовлетворить полностью",
                "link": "https://kad.arbitr.ru/Kad/PdfDocument/e55e8888-fd43-486b-b9ee-50b64f3dddbd/a4fe2fc6-0709-4674-a962-cf8f5068bf5d/A40-283685-2023_20231206_Reshenija_i_postanovlenija.pdf"
              }
            ],
            "calendar_events": [
              {
                "date": "04.12.2023",
                "description": "Заявление",
                "result": "Заявление о выдаче судебного приказа",
                "link": "",
                "documents": []
              },
              {
                "date": "06.12.2023",
                "description": "Решения и постановления",
                "result": "Судебный приказ",
                "link": "https://kad.arbitr.ru/Kad/PdfDocument/e55e8888-fd43-486b-b9ee-50b64f3dddbd/a4fe2fc6-0709-4674-a962-cf8f5068bf5d/A40-283685-2023_20231206_Reshenija_i_postanovlenija.pdf",
                "documents": [
                  {
                    "name": "Судебный приказ",
                    "link": "https://kad.arbitr.ru/Kad/PdfDocument/e55e8888-fd43-486b-b9ee-50b64f3dddbd/a4fe2fc6-0709-4674-a962-cf8f5068bf5d/A40-283685-2023_20231206_Reshenija_i_postanovlenija.pdf"
                  }
                ]
              }
            ],
            "electronic_case_files": [
              {
                "date": "06.12.2023",
                "document_name": "Иск удовлетворить полностью",
                "declarer": "Поздняков В. Д.",
                "link": "https://kad.arbitr.ru/Kad/PdfDocument/e55e8888-fd43-486b-b9ee-50b64f3dddbd/a4fe2fc6-0709-4674-a962-cf8f5068bf5d/A40-283685-2023_20231206_Reshenija_i_postanovlenija.pdf"
              }
            ],
            "card_pdf_analysis": {
              "pdf_link": "https://kad.arbitr.ru/Kad/PdfDocument/e55e8888-fd43-486b-b9ee-50b64f3dddbd/a4fe2fc6-0709-4674-a962-cf8f5068bf5d/A40-283685-2023_20231206_Reshenija_i_postanovlenija.pdf",
              "detail_info": {
                "case_info": {
                  "case_number": "А40-283685/23-93-2309",
                  "court": "Арбитражный суд города Москвы",
                  "decision_date": "2023-12-06",
                  "judge": "Поздняков В.Д.",
                  "document_type": "судебный приказ"
                },
                "classification": {
                  "case_type": "SOCIAL_CONTRIBUTIONS",
                  "case_subtype": null,
                  "confidence": 1,
                  "classification_rationale": "Взыскание обязательных платежей и санкций за нарушение законодательства об индивидуальном учёте"
                },
                "parties": {
                  "claimant": {
                    "name": "Отделение Фонда пенсионного и социального страхования Российской Федерации по г. Москве и Московской области в лице филиала № 10",
                    "inn": "7703363868",
                    "ogrn": "1027703026075",
                    "address": "115419, город Москва, Стасовой улица, дом 14, корпус 2"
                  },
                  "debtor": {
                    "name": "Общество с ограниченной ответственностью 'АПЕКС КОНСАЛТ'",
                    "inn": "7707332613",
                    "ogrn": "1157746102535",
                    "address": "127473, город Москва, 1-й Самотёчный переулок, дом 2, строение 2, помещение 4 оф 3"
                  }
                },
                "financials": {
                  "main_debt": 500,
                  "state_fee": null,
                  "total_amount": 500,
                  "currency": "RUB"
                },
                "case_subject": {
                  "essence": "Взыскание обязательных платежей и санкций за нарушение законодательства об индивидуальном (персонифицированном) учёте в системе обязательного пенсионного страхования по форме СЗВ-М",
                  "period": "апрель 2020",
                  "legal_basis": [
                    "27-ФЗ",
                    "212–ФЗ"
                  ]
                },
                "summary": null
              }
            },
            "source_url": "https://kad.arbitr.ru/Card/e55e8888-fd43-486b-b9ee-50b64f3dddbd"
          },
          {
            "case_number": "А40-82292/2018",
            "status": "Рассмотрение дела завершено",
            "participants": {
              "plaintiffs": [
                {
                  "name": "ГУ ГЛАВНОЕ УПРАВЛЕНИЕ ПЕНСИОННОГО ФОНДА РОССИЙСКОЙ ФЕДЕРАЦИИ №10 ПО Г.МОСКВЕ И МОСКОВСКОЙ ОБЛАСТИ",
                  "address": "105082, Россия, г Москва, г. Москва, ул. Большая Почтовая, д. 40 строение 6"
                }
              ],
              "defendants": [
                {
                  "name": "ООО \"АПЕКС КОНСАЛТ\"",
                  "address": "127473, Россия, г Москва, г. Москва, переулок 1-й Самотечный, д. 2 строение 2, офис 3"
                }
              ],
              "third_parties": [],
              "others": []
            },
            "judges": [
              {
                "court": "АС города Москвы",
                "name": "Полякова А. Б."
              }
            ],
            "acts": [],
            "calendar_events": [
              {
                "date": "18.04.2018",
                "description": "Заявление",
                "result": "Заявление о выдаче судебного приказа",
                "link": "",
                "documents": []
              },
              {
                "date": "27.04.2018",
                "description": "Решения и постановления",
                "result": "Судебный приказ",
                "link": "https://kad.arbitr.ru/Kad/PdfDocument/21ab8c13-c41b-4015-a90d-bf61674c84e1/42230339-c6a6-4a9e-8860-6a30d3f37c1c/A40-82292-2018_20180427_Reshenija_i_postanovlenija.pdf",
                "documents": [
                  {
                    "name": "Судебный приказ",
                    "link": "https://kad.arbitr.ru/Kad/PdfDocument/21ab8c13-c41b-4015-a90d-bf61674c84e1/42230339-c6a6-4a9e-8860-6a30d3f37c1c/A40-82292-2018_20180427_Reshenija_i_postanovlenija.pdf"
                  }
                ]
              }
            ],
            "electronic_case_files": [
              {
                "date": "27.04.2018",
                "document_name": "Иск удовлетворить полностью",
                "declarer": "Полякова А. Б.",
                "link": "https://kad.arbitr.ru/Kad/PdfDocument/21ab8c13-c41b-4015-a90d-bf61674c84e1/42230339-c6a6-4a9e-8860-6a30d3f37c1c/A40-82292-2018_20180427_Reshenija_i_postanovlenija.pdf"
              }
            ],
            "card_pdf_analysis": {
              "pdf_link": "https://kad.arbitr.ru/Kad/PdfDocument/21ab8c13-c41b-4015-a90d-bf61674c84e1/42230339-c6a6-4a9e-8860-6a30d3f37c1c/A40-82292-2018_20180427_Reshenija_i_postanovlenija.pdf",
              "detail_info": {
                "case_info": {
                  "case_number": "А40-82292/18-17-946",
                  "court": "Арбитражный суд города Москвы",
                  "decision_date": "2018-04-00",
                  "judge": "А.Б. Полякова",
                  "document_type": "судебный приказ"
                },
                "classification": {
                  "case_type": "SOCIAL_CONTRIBUTIONS",
                  "case_subtype": null,
                  "confidence": 1,
                  "classification_rationale": "Взыскание финансовой санкции за нарушение сроков представления индивидуальных сведений"
                },
                "parties": {
                  "claimant": {
                    "name": "ГУ-ГУ ПФР № 10 по г. Москве и Московской области",
                    "inn": "7701319704",
                    "ogrn": "1027701022788",
                    "address": "125009, г. Москва, Тверской б-р, д. 18, стр. 1"
                  },
                  "debtor": {
                    "name": "ООО «Апект консалт»",
                    "inn": "7707332613",
                    "ogrn": "1157746102535",
                    "address": "127473, г. Москва, 1-й Самотёчный пер., д. 2, пом. 4, оф. 3"
                  }
                },
                "financials": {
                  "main_debt": 500,
                  "state_fee": 1000,
                  "total_amount": 1500,
                  "currency": "RUB"
                },
                "case_subject": {
                  "essence": "Взыскание финансовой санкции (штрафа) за нарушение сроков представления индивидуальных сведений персонифицированного учета",
                  "period": "январь 2017 г.",
                  "legal_basis": [
                    "Федеральный закон от 01.04.1996 № 27-ФЗ «Об индивидуальном (персонифицированном) учете в системе обязательного пенсионного страхования»",
                    "статьи 65, 229.-229.6 АПК РФ"
                  ]
                },
                "summary": "Взыскание с должника ООО «Апект консалт» финансовой санкции в размере 500 руб. и государственной пошлины в размере 1 000 руб."
              }
            },
            "source_url": "https://kad.arbitr.ru/Card/21ab8c13-c41b-4015-a90d-bf61674c84e1"
          }
        ]
      },
      "taskId": "40e2b318-0375-4b4e-a0ab-7e4d3e9a238d",
      "dateupdated": "2026-01-02 18:52:30"
    }
  }
}
```

---
