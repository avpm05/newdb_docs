---
title: "rosreestr — проверка объекта недвижимости по кадастровому номеру или адресу"
description: "Метод NEWDB rosreestr получает сведения об объекте недвижимости из Росреестра по кадастровому номеру (КН) или текстовому адресу, включая права и обременения."
canonical_url: https://newdb.net/docs/property/01-rosreestr/
meta:
  - name: keywords
    content: "NEWDB API, rosreestr, Росреестр, кадастровый номер, адрес, недвижимость, права, обременения, ипотека"
  - property: og:title
    content: "Проверка недвижимости в Росреестре — метод rosreestr"
  - property: og:description
    content: "Получите сведения Росреестра по объекту недвижимости: кадастровый номер, площадь, права собственности и обременения по КН или адресу через API NEWDB."
---

# rosreestr — Проверка объекта недвижимости (Росреестр)

POST `https://api.newdb.net/v2`

Метод выполняет поиск и получение сведений об объекте недвижимости из Росреестра.  
Поиск можно выполнить:

- по **кадастровому номеру** (например: `50:20:0030112:1658`)
- по **текстовому адресу** (например: `Одинцово Белорусская д.3 кв. 382`)

---

## Заголовки

Content-Type: application/json
X-API-KEY: <your_token>

## Входная схема (request)

```json
{
  "params": {
    "address": "string (кадастровый номер или адрес строкой)",
    "method": "rosreestr",
    "country": "ru"
  },
  "webhook": "https://your.host/whook",
  "requestId": "optional-string"
}

```

## Пример запроса (по кадастровому номеру)

POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

```json
{
  "params": {
    "address": "50:20:0030112:1658",
    "method": "rosreestr",
    "country": "ru"
  },
  "webhook":"https://webhook_url/",
  "requestId":"19342f89-2916-4779-b59d-43c001f1a119"
}
```

## Пример запроса (по адресу)

POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

```json
{
  "params": {
    "address": "Одинцово Белорусская д.3 кв. 382",
    "method": "rosreestr",
    "country": "ru"
  },
  "webhook":"https://webhook_url/",
  "requestId":"19342f89-2916-4779-b59d-43c001f1a112"
}
```

## Пример ответа

```json
{
  "params": {
    "address": "Одинцово Белорусская д.3 кв. 382",
    "method": "rosreestr",
    "country": "ru",
    "newdb_qid": "EOUIIJHP3ZaxMygD"
  },
  "webhook": "https://webhook_url/",
  "requestId": "19342f89-2916-4779-b59d-43c001f1a112",
  "datecreated": "2025-12-12 16:54:25",
  "state": "complete",
  "balance": 9920,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "rosreestr": {
      "dateupdated": "2025-12-12 16:55:09",
      "result": {
        "status": 200,
        "data": [
          {
            "objectId": null,
            "databaseName": null,
            "regionKey": null,
            "cadNumber": "50:20:0030112:1658",
            "cadQuarter": "50:20:0020410",
            "status": "1",
            "objType": "002001003000",
            "area": "42.40",
            "address": {
              "region": null,
              "district": null,
              "city": null,
              "cityType": null,
              "urbanDistrict": null,
              "urbanDistrictType": null,
              "sovietVillage": null,
              "sovietVillageType": null,
              "locality": null,
              "localityType": null,
              "street": null,
              "streetType": null,
              "house": null,
              "houseType": null,
              "building": null,
              "buildingType": null,
              "structure": null,
              "structureType": null,
              "apartment": null,
              "apartmentType": null,
              "liter": null,
              "addition": null,
              "address": null,
              "readableAddress": null,
              "fiasGuid": null
            },
            "regDate": "09.04.2014",
            "cancelDate": null,
            "rights": [
              {
                "rightType": "001001000000",
                "rightRegDate": "01.03.2013",
                "rightNumber": "50-50-20/020/2013-320",
                "part": null,
                "ownershipType": null,
                "rightTypeDesc": "Собственность",
                "sharedOwnershipType": false
              }
            ],
            "encumbrances": [
              {
                "startDate": "01.03.2013",
                "encumbranceNumber": "50-50-20/020/2013-322",
                "encumbranceDate": null,
                "type": "022008000000",
                "typeDesc": "Ипотека в силу закона",
                "rightNum": null
              },
              {
                "startDate": "23.08.2021",
                "encumbranceNumber": "50:20:0030112:1658-50/422/2021-2",
                "encumbranceDate": null,
                "type": "022007000000",
                "typeDesc": "Ипотека",
                "rightNum": null
              }
            ],
            "oldNumbers": [
              {
                "numType": "Условный номер",
                "numValue": "50-50-20/049/2012-410"
              },
              {
                "numType": "Инвентарный номер",
                "numValue": "46:241:002:000219530:0001(10382)"
              }
            ],
            "landCategory": null,
            "permittedUse": null,
            "permittedUseByDoc": null,
            "cadCost": "5133262.85",
            "cadCostDate": null,
            "cadCostDeterminationDate": "01.01.2023",
            "cadCostRegistrationDate": "09.12.2023",
            "infoUpdateDate": "06.12.2025",
            "cadEngFIO": null,
            "cadEngCertNumber": null,
            "cadEngPhone": null,
            "floor": null,
            "undergroundFloor": null,
            "levelFloor": "18",
            "ownershipType": null,
            "oksWallMaterial": null,
            "oksCommisioningYear": null,
            "oksYearBuild": null,
            "purpose": "206002000000",
            "childCadNumbers": null,
            "parentCadNumber": null,
            "mainCharacters": [
              {
                "code": "05",
                "description": "Площадь",
                "value": 42.4,
                "unitCode": "012002001000",
                "unitDescription": "кв.м"
              }
            ],
            "objType_text": "Помещение",
            "purpose_text": "Жилое"
          }
        ]
      }
    }
  }
}
```

## Пример ответа (данные не найдены

```json
{
  "state": "complete",
  "results": {
    "rosreestr": {
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
      "name": "rosreestr",
      "description": "Получение сведений об объекте недвижимости из Росреестра по кадастровому номеру или текстовому адресу. Возвращает параметры объекта, кадастровую стоимость, права и обременения (например, ипотека).",
      "input_schema": {
        "address": "string — кадастровый номер (пример: 50:20:0030112:1658) или адрес строкой",
        "country": "string (ru)",
        "method": "string (rosreestr)",
        "webhook": "string (URL для webhook, optional)",
        "requestId": "string (optional)"
      },
      "output_schema": {
        "state": "string (complete|processing|error)",
        "results": {
          "rosreestr": {
            "result": {
              "status": "number (HTTP status)",
              "data": [
                {
                  "cadNumber": "string — кадастровый номер",
                  "cadQuarter": "string — кадастровый квартал",
                  "objType_text": "string — тип объекта (текст)",
                  "purpose_text": "string — назначение (текст)",
                  "area": "string — площадь",
                  "regDate": "string — дата постановки/регистрации",
                  "cadCost": "string — кадастровая стоимость",
                  "cadCostDeterminationDate": "string — дата оценки",
                  "cadCostRegistrationDate": "string — дата внесения стоимости",
                  "infoUpdateDate": "string — дата обновления сведений",
                  "rights": [
                    {
                      "rightTypeDesc": "string — тип права (например, Собственность)",
                      "rightRegDate": "string — дата регистрации права",
                      "rightNumber": "string — номер регистрации права"
                    }
                  ],
                  "encumbrances": [
                    {
                      "typeDesc": "string — тип обременения (например, Ипотека)",
                      "startDate": "string — дата начала",
                      "encumbranceNumber": "string — номер записи обременения"
                    }
                  ],
                  "oldNumbers": [
                    {
                      "numType": "string — тип номера",
                      "numValue": "string — значение"
                    }
                  ]
                }
              ]
            }
          }
        }
      },
      "example": {
        "request_by_cad": {
          "params": {
            "address": "50:20:0030112:1658",
            "method": "rosreestr",
            "country": "ru"
          },
          "webhook": "https://webhook_url/",
          "requestId": "19342f89-2916-4779-b59d-43c001f1a119"
        },
        "request_by_address": {
          "params": {
            "address": "Одинцово Белорусская д.3 кв. 382",
            "method": "rosreestr",
            "country": "ru"
          },
          "webhook": "https://webhook_url/",
          "requestId": "19342f89-2916-4779-b59d-43c001f1a112"
        },
        "response_empty": {
          "state": "complete",
          "results": {
            "rosreestr": {
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
  "policy": "Если пользователь хочет проверить объект недвижимости по кадастровому номеру или адресу (права, обременения, ипотека, кадастровая стоимость) — вызывай метод rosreestr и верни найденные сведения."
}
```
