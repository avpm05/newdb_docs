---
title: "fssp_legal — исполнительные производства ФССП по ИНН юрлица"
description: "Метод NEWDB fssp_legal выполняет поиск исполнительных производств ФССП по ИНН юридического лица."
canonical_url: https://newdb.net/docs/legal/05-fssp_legal/
meta:
  - name: keywords
    content: "NEWDB API, fssp_legal, ФССП, исполнительные производства, юрлица, ИНН"
  - property: og:title
    content: "ФССП по ИНН юрлица — метод fssp_legal"
  - property: og:description
    content: "Проверка исполнительных производств ФССП по ИНН юридического лица через API NEWDB."
---

# fssp_legal — Исполнительные производства ФССП по ИНН юрлица

POST `https://api.newdb.net/v2`

Метод выполняет поиск исполнительных производств в базе ФССП по ИНН юридического лица. В ответе возвращаются найденные производства, сведения о должнике-организации, реквизиты исполнительного документа и данные о завершении производства.

**Рекомендуем также:** блокировки счетов по ФНС — [fns_block](02-fns_block.md), сведения о компании — [egrul](04-egrul.md).

## ЗаголовкиG

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
    "method": "fssp_legal"
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
    "inn": "7735106398",
    "country": "ru",
    "method": "fssp_legal"
  },
  "webhook": "https://newer.net/whook",
  "requestId": "5fe0f4ff-a60a-4bca-8767-70006a3b4ec4"
}
```

## Пример ответа

```json
{
  "params": {
    "inn": "7735106398",
    "country": "ru",
    "method": "fssp_legal"
  },
  "webhook": "https://newer.net/whook",
  "requestId": "5fe0f4ff-a60a-4bca-8767-70006a3b4ec4",
  "datecreated": "2026-03-21 15:34:01",
  "state": "complete",
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "fssp_legal": {
      "taskId": "4b39f3ef-2b13-4b84-9d81-0b55c9f89e83",
      "dateupdated": "2026-03-21 15:34:02",
      "result": {
        "status": 200,
        "data": [
          {
            "Debtor": {
              "Type": "LegalEntity",
              "Name": "ООО ЗЕЛЕНОГРАДСКОЕ ТАКСИ 1027700586484 124365",
              "LegalAddress": "77, КРЮКОВО (ЗЕЛАО) Р-Н,ЗЕЛЕНОГРАД, 1 МАЯ, 1, ОФ.3",
              "ActualAddress": null,
              "INN": "7735106398",
              "raw": "ООО ЗЕЛЕНОГРАДСКОЕ ТАКСИ 1027700586484 124365,77, КРЮКОВО (ЗЕЛАО) Р-Н,ЗЕЛЕНОГРАД, 1 МАЯ, 1, ОФ.3 7735106398"
            },
            "EnforcementProceeding": {
              "Number": "647113/25/77012-ИП",
              "InitiationDate": "28.10.2025",
              "raw": "647113/25/77012-ИП от 28.10.2025"
            },
            "WritDetails": {
              "Type": "Постановление судебного пристава-исполнителя",
              "IssuedDate": "28.10.2025",
              "Number": "77012/25/1799768",
              "IssuerName": "ОТДЕЛ СУДЕБНЫХ ПРИСТАВОВ ПО ЗЕЛЕНОГРАДСКОМУ АДМИНИСТРАТИВНОМУ ОКРУГУ ГУФССП РОССИИ ПО Г. МОСКВЕ Постановление о взыскании исполнительского сбора",
              "ClaimantOrganizationINN": null,
              "raw": "Постановление судебного пристава-исполнителя от 28.10.2025 № 77012/25/1799768 ОТДЕЛ СУДЕБНЫХ ПРИСТАВОВ ПО ЗЕЛЕНОГРАДСКОМУ АДМИНИСТРАТИВНОМУ ОКРУГУ ГУФССП РОССИИ ПО Г. МОСКВЕ Постановление о взыскании исполнительского сбора"
            },
            "CompletionDateOrReason": {
              "CompletionDate": null,
              "Article": null,
              "Part": null,
              "Point": null,
              "raw": ""
            }
          }
        ]
      }
    }
  },
  "finished": 1
}
```

## Поля результата `results.fssp_legal.result.data[]`

| Поле | Описание |
|------|----------|
| `Debtor` | Блок сведений о должнике-юридическом лице |
| `EnforcementProceeding` | Номер и дата возбуждения исполнительного производства |
| `WritDetails` | Данные исполнительного документа |
| `CompletionDateOrReason` | Сведения о завершении производства или правовом основании завершения |

## Поля `Debtor`

| Поле | Описание |
|------|----------|
| `Type` | Тип должника. Для компаний обычно `LegalEntity` |
| `Name` | Наименование должника в том виде, как оно опубликовано в ФССП |
| `LegalAddress` | Юридический адрес организации |
| `ActualAddress` | Фактический адрес, если он был найден |
| `INN` | ИНН юридического лица |
| `raw` | Исходная строка должника из источника без нормализации |

## Поля `EnforcementProceeding`

| Поле | Описание |
|------|----------|
| `Number` | Номер исполнительного производства |
| `InitiationDate` | Дата возбуждения исполнительного производства |
| `raw` | Исходная строка с номером и датой производства |

## Поля `WritDetails`

| Поле | Описание |
|------|----------|
| `Type` | Вид исполнительного документа |
| `IssuedDate` | Дата выдачи или вынесения документа |
| `Number` | Номер исполнительного документа |
| `IssuerName` | Орган или должностное лицо, выдавшее документ |
| `ClaimantOrganizationINN` | ИНН взыскателя-организации, если присутствует в источнике |
| `raw` | Исходная строка исполнительного документа из ФССП |

## Поля `CompletionDateOrReason`

| Поле | Описание |
|------|----------|
| `CompletionDate` | Дата завершения или окончания исполнительного производства |
| `Article` | Статья закона, указанная как основание завершения |
| `Part` | Часть статьи |
| `Point` | Пункт статьи |
| `raw` | Исходная строка с причиной завершения. Может быть пустой, если производство активно |

## Пример ответа (данные не найдены)

```json
{
  "state": "complete",
  "results": {
    "fssp_legal": {
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
      "name": "fssp_legal",
      "description": "Проверка исполнительных производств ФССП по ИНН юридического лица. Возвращает найденные производства, сведения о должнике и реквизиты исполнительного документа.",
      "input_schema": {
        "inn": "string — ИНН юридического лица",
        "country": "string (ru)",
        "method": "string (fssp_legal)",
        "webhook": "string (URL, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "fssp_legal": {
            "taskId": "string",
            "dateupdated": "string (YYYY-MM-DD HH:MM:SS)",
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "Debtor": {
                    "Type": "string — тип должника",
                    "Name": "string — наименование организации",
                    "LegalAddress": "string|null — юридический адрес",
                    "ActualAddress": "string|null — фактический адрес",
                    "INN": "string — ИНН юрлица",
                    "raw": "string — исходная строка из источника"
                  },
                  "EnforcementProceeding": {
                    "Number": "string — номер исполнительного производства",
                    "InitiationDate": "string (DD.MM.YYYY) — дата возбуждения",
                    "raw": "string — исходная строка"
                  },
                  "WritDetails": {
                    "Type": "string — тип исполнительного документа",
                    "IssuedDate": "string (DD.MM.YYYY) — дата документа",
                    "Number": "string — номер документа",
                    "IssuerName": "string — орган или должностное лицо",
                    "ClaimantOrganizationINN": "string|null — ИНН взыскателя",
                    "raw": "string — исходная строка"
                  },
                  "CompletionDateOrReason": {
                    "CompletionDate": "string|null — дата завершения",
                    "Article": "string|null — статья основания",
                    "Part": "string|null — часть статьи",
                    "Point": "string|null — пункт статьи",
                    "raw": "string — причина завершения или пустая строка"
                  }
                }
              ]
            }
          }
        }
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь хочет проверить исполнительные производства, долги у судебных приставов или записи ФССП по ИНН компании, используй метод fssp_legal."
}
```
