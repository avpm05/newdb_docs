---
title: "patent_msk — проверка патента"
description: "Метод NEWDB patent_msk для проверки статуса патента иностранного гражданина в Москве."
canonical_url: https://newdb.net/docs/foreign/02-foreign_patent/
meta:
  - name: keywords
    content: "NEWDB API, patent_msk, патент, иностранные граждане, Москва"
  - property: og:title
    content: "Проверка патента в Москве — метод patent_msk"
  - property: og:description
    content: "Описание запроса, схемы и ответа метода patent_msk."
---

# patent_msk — Патент (Москва)

POST `https://api.newdb.net/v2`

Метод выполняет проверку статуса патента иностранного гражданина в Москве.

**Раздел:** [Иностранные граждане](index.md)

## Связанные страницы

- [Обзор раздела иностранные граждане](index.md)
- [foreign_vng — Вид на жительство (ВНЖ)](01-foreign_vng.md)
- [foreign_rvp_stamp — РВП (штамп в паспорте)](03-foreign_rvp_stamp.md)
- [foreign_rvp_blank — РВП (бланк)](04-foreign_rvp_blank.md)

## Когда использовать

Используйте метод, когда нужно проверить статус документа или разрешительного основания иностранного гражданина.

## Типовые кейсы

- Проверка ВНЖ, патента, РВП или разрешения на работу перед оформлением
- Контроль миграционных документов в HR или compliance-процессе
- Подтверждение статуса документа по данным анкеты и реквизитам

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "method": "patent_msk",
    "firstname": "string",
    "lastname": "string",
    "secondname": "string",
    "id_doc_seria": "string",
    "id_doc_number": "string",
    "citizenship": "string (optional)",
    "country": "ru"
  },
  "requestId": "optional-string"
}
```

## Пояснения к полям
- `firstname`, `lastname`, `secondname` — ФИО заявителя.
- `id_doc_seria` и `id_doc_number` — серия и номер документа, удостоверяющего личность.
- `citizenship` — гражданство (например, `Узбекистан`).
Если поле не передано, выполняется проверка по трем странам: `Узбекистан`, `Таджикистан`, `Кыргызстан`.
- `country` — страна запроса (`ru`). Если поле не передано, используется `ru`.

## Справочник citizenship
- Поле `citizenship` принимает строковое значение страны из справочника стран формы проверки.
- Рекомендуемые значения для проверки патента: `Узбекистан`, `Таджикистан`, `Кыргызстан`.
- Если `citizenship` не передано, проверка выполняется автоматически по трем странам:
`Узбекистан`, `Таджикистан`, `Кыргызстан`.

Пример элемента справочника (HTML `select`):

```html
<select name="citizenship" id="citizenship">
  <option value="-1"></option>
  <option value="102316">Узбекистан</option>
  <option value="102239">Таджикистан</option>
  <option value="139762">Кыргызстан</option>
  <option value="102197">Россия</option>
  <option value="102223">Украина</option>
  <option value="102213">Казахстан</option>
  <option value="102404">Киргизия</option>
  <option value="102370">Соединенные Штаты</option>
  <option value="102244">Германия</option>
  <option value="102447">Франция</option>
</select>
```

## Пример запроса
```json
{
  "params": {
    "method": "patent_msk",
    "firstname": "Алишер",
    "lastname": "Рахимов",
    "secondname": "Саидович",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "citizenship": "Узбекистан",
    "country": "ru"
  },
  "requestId": "b4c66a6b-45cc-430e-bbeb-a6528014bca4"
}
```

## Пример ответа
```json
{
  "params": {
    "method": "patent_msk",
    "firstname": "Алишер",
    "lastname": "Рахимов",
    "secondname": "Саидович",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "citizenship": "Узбекистан",
    "country": "ru",
    "newdb_qid": "ENkjILTX38_LMygB"
  },
  "requestId": "b4c66a6b-45cc-430e-bbeb-a6528014bca4",
  "datecreated": "2026-03-04 20:49:17",
  "state": "complete",
  "balance": 9811,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "patent_msk": {
      "taskId": "b83f85ba-0e0f-4050-850d-b18961ea9677",
      "dateupdated": "2026-03-04 20:49:36",
      "result": {
        "status": 200,
        "data": [
          {
            "citizenship": "Узбекистан",
            "message": "Срок действия Вашего патента истек 26.08.2025 Для работы в Москве необходимо оформить новый патент.",
            "status": "expired"
          }
        ]
      }
    }
  }
}
```

## Статус в ответе
- `status: "expired"` — срок действия патента истек.
- `status: "not_found"` — патент не найден.
- `status: "valid"` — патент действителен.

Поле `captcha_failed` в ответе не используется.

## AI Summary

<details>
<summary>Компактные метаданные для AI и агентных систем</summary>

```json
{
  "method": "patent_msk",
  "intent": "Проверка патента иностранного гражданина",
  "endpoint": "POST https://api.newdb.net/v2",
  "required_headers": ["X-API-KEY"],
  "required_fields": ["method", "firstname", "lastname", "secondname", "id_doc_seria", "id_doc_number", "citizenship", "country", "requestId"],
  "returns": ["state", "results.patent_msk.result.status", "results.patent_msk.result.data"]
}
```

</details>


