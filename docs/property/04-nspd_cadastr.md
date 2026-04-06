---
title: "nspd_cadastr — геоданные по кадастровому номеру"
description: "Метод NEWDB nspd_cadastr получает геоданные и сведения об объекте недвижимости по кадастровому номеру: координаты, контур, адрес, площадь и кадастровую стоимость."
canonical_url: https://newdb.net/docs/property/04-nspd_cadastr/
meta:
  - name: keywords
    content: "NEWDB API, nspd_cadastr, кадастровый номер, геоданные, недвижимость, координаты, контур, НСПД"
  - property: og:title
    content: "Геоданные по кадастровому номеру — метод nspd_cadastr"
  - property: og:description
    content: "Получите геоданные, контур и характеристики объекта недвижимости по кадастровому номеру через API NEWDB."
---

# nspd_cadastr — Получение геоданных по кадастровому номеру

POST `https://api.newdb.net/v2`

Метод возвращает сведения об объекте недвижимости по кадастровому номеру, включая:

- координаты центра объекта
- точки контура
- геометрию объекта в формате `Polygon`
- адрес, площадь, этажность, год постройки
- назначение, вид права и кадастровую стоимость

**Раздел:** [Имущество](index.md)

## Связанные страницы

- [Обзор раздела имущество](index.md)
- [pledge_vin — Проверка залога и обременений по VIN (ФНП + Федресурс)](03-pledge_vin.md)
- [pledge_property — Проверка залога и обременений по ID (ФНП + Федресурс)](02-pledge_property.md)
- [rosreestr — Проверка объекта недвижимости (Росреестр)](01-rosreestr.md)

## Когда использовать

Используйте метод, когда нужно проверить объект недвижимости, транспорт или сведения о залоге и обременениях.

## Типовые кейсы

- Проверка объекта перед сделкой или выдачей займа
- Получение сведений о залоге, кадастровых данных или геометрии объекта
- Обогащение карточки имущества структурированными данными из внешнего реестра

## Заголовки

Content-Type: application/json
X-API-KEY: <your_token>

## Входная схема (request)

```json
{
  "requestId": "optional-string",
  "taskId": "optional-string",
  "params": {
    "method": "nspd_cadastr",
    "cad_num": "50:20:0020402:2230",
    "country": "ru"
  }
}
```

## Параметры запроса

| Поле | Тип | Обязательное | Описание |
| --- | --- | --- | --- |
| `requestId` | `string` | Нет | Уникальный идентификатор запроса на стороне клиента. |
| `taskId` | `string` | Нет | Внутренний идентификатор задачи, если используется в вашей интеграции. |
| `params.method` | `string` | Да | Значение должно быть `nspd_cadastr`. |
| `params.cad_num` | `string` | Да | Кадастровый номер объекта недвижимости. |
| `params.country` | `string` | Да | Код страны. Для России используйте `ru`. |

## Пример запроса

POST /v2 HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

```json
{
  "requestId": "a5962f88-2916-4779-b59d-43c023fa1894",
  "taskId": "nspd-cadastr-local-test-001",
  "params": {
    "method": "nspd_cadastr",
    "cad_num": "50:20:0020402:2230",
    "country": "ru"
  }
}
```

## Пример ответа

```json
{
  "requestId": "a5962f88-2916-4779-b59d-43c023fa1894",
  "taskId": "nspd-cadastr-local-test-001",
  "params": {
    "method": "nspd_cadastr",
    "cad_num": "50:20:0020402:2230",
    "country": "ru"
  },
  "datecreated": "2026-04-06 23:10:57",
  "state": "complete",
  "balance": 9623,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "nspd_cadastr": {
      "taskId": "68360634-9601-4af5-9820-aa5c7c416e48",
      "dateupdated": "2026-04-06 23:11:28",
      "result": {
        "status": 200,
        "data": [
          {
            "count": 1,
            "items": [
              {
                "object": {
                  "id": 157240605,
                  "cad_num": "50:20:0020402:2230",
                  "category": "Здания",
                  "type": "Здание",
                  "name": "Индивидуальный жилой",
                  "address": "Российская Федерация, Московская область, г.о. Одинцовский, д Глазынино, д. 60Б",
                  "area": 174.2,
                  "floors": "1",
                  "year_built": "2022",
                  "status": "Учтенный",
                  "purpose": "Жилой дом",
                  "permitted_use": "Индивидуальный жилой дом",
                  "ownership_type": "Частная",
                  "right_type": "Собственность",
                  "cad_cost": 7020879.97
                },
                "geo": {
                  "center": {
                    "lat": 55.66651799,
                    "lon": 37.307048
                  },
                  "points": [
                    {
                      "lon": 37.30692886,
                      "lat": 55.66660437
                    },
                    {
                      "lon": 37.30697884,
                      "lat": 55.66642699
                    },
                    {
                      "lon": 37.30716713,
                      "lat": 55.66644389
                    },
                    {
                      "lon": 37.30712621,
                      "lat": 55.66658964
                    },
                    {
                      "lon": 37.3069899,
                      "lat": 55.66657738
                    },
                    {
                      "lon": 37.30698101,
                      "lat": 55.666609
                    },
                    {
                      "lon": 37.30692886,
                      "lat": 55.66660437
                    }
                  ],
                  "source_geometry": {
                    "type": "Polygon",
                    "coordinates": [
                      [
                        [
                          4152988.323135661,
                          7492330.286758492
                        ],
                        [
                          4152993.886819103,
                          7492295.2779500205
                        ],
                        [
                          4153014.847311023,
                          7492298.61263929
                        ],
                        [
                          4153010.2915783804,
                          7492327.380263791
                        ],
                        [
                          4152995.118216751,
                          7492324.959447225
                        ],
                        [
                          4152994.128032246,
                          7492331.20095866
                        ],
                        [
                          4152988.323135661,
                          7492330.286758492
                        ]
                      ]
                    ]
                  },
                  "geometry": {
                    "type": "Polygon",
                    "coordinates": [
                      [
                        [
                          37.30692886,
                          55.66660437
                        ],
                        [
                          37.30697884,
                          55.66642699
                        ],
                        [
                          37.30716713,
                          55.66644389
                        ],
                        [
                          37.30712621,
                          55.66658964
                        ],
                        [
                          37.3069899,
                          55.66657738
                        ],
                        [
                          37.30698101,
                          55.666609
                        ],
                        [
                          37.30692886,
                          55.66660437
                        ]
                      ]
                    ]
                  }
                }
              }
            ]
          }
        ]
      }
    }
  }
}
```

## Что возвращается в ответе

| Поле | Описание |
| --- | --- |
| `state` | Статус обработки запроса. |
| `results.nspd_cadastr.result.status` | HTTP-статус результата обработки. |
| `results.nspd_cadastr.result.data[].count` | Количество найденных объектов. |
| `results.nspd_cadastr.result.data[].items[].object` | Основные сведения об объекте: тип, адрес, площадь, этажность, назначение, форма собственности и кадастровая стоимость. |
| `results.nspd_cadastr.result.data[].items[].geo.center` | Центральная точка объекта в координатах WGS84. |
| `results.nspd_cadastr.result.data[].items[].geo.points` | Точки контура объекта в координатах WGS84. |
| `results.nspd_cadastr.result.data[].items[].geo.geometry` | Геометрия объекта в формате `Polygon` с координатами WGS84. |
| `results.nspd_cadastr.result.data[].items[].geo.source_geometry` | Исходная геометрия объекта в системе координат источника. |

## AI Summary

<details>
<summary>Компактные метаданные для AI и агентных систем</summary>

```json
{
  "method": "nspd_cadastr",
  "intent": "Получение геоданных и характеристик объекта недвижимости по кадастровому номеру",
  "endpoint": "POST https://api.newdb.net/v2",
  "required_headers": ["X-API-KEY"],
  "required_fields": ["cad_num", "method", "country"],
  "returns": ["state", "results.nspd_cadastr.result.status", "results.nspd_cadastr.result.data[].items[].geo"]
}
```

</details>


