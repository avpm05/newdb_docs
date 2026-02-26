---
title: "rkl — проверка по реестру контролируемых лиц"
description: "Метод NEWDB rkl выполняет проверку по реестру контролируемых лиц через форму Госуслуг."
canonical_url: https://newdb.net/docs/foreign/06-foreign_rkl/
meta:
  - name: keywords
    content: "NEWDB API, rkl, реестр контролируемых лиц, Госуслуги"
  - property: og:title
    content: "Проверка по реестру контролируемых лиц — метод rkl"
  - property: og:description
    content: "Параметры запроса rkl, форматы dob_info и логика заполнения формы."
---

# rkl — Проверка по реестру контролируемых лиц

POST `https://api.newdb.net/v2`

Метод выполняет проверку лица по форме сервиса Госуслуг "Реестр контролируемых лиц".

## Заголовки

```http
Content-Type: application/json
X-API-KEY: <your_token>
```

## Пример параметров запроса (`params`)

Ниже пример в формате, который фактически передается в spider (`params_raw`):

```python
params_raw = json.dumps({
    "method": "rkl",
    "country": "ru",
    "lastname": "Зиёдулла",
    "firstname": "Бегимов",
    "secondname": "Камолович ",
    "dob_info": "01.2002",
    "issue_date": "31.01.2002",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "newdb_qid": "EKYiIMO21ZnJMygA",
    "taskId": "test-rkl-003"
})
```

Для `dob_info = "01.2002"` spider выберет режим частичной даты рождения "Месяц и год" (`optional = "3"`), год `2002`, месяц `1` (в форме: `Янв 2002`).

## Пример API-запроса

```json
{
  "params": {
    "method": "rkl",
    "country": "ru",
    "lastname": "Зиёдулла",
    "firstname": "Бегимов",
    "secondname": "Камолович ",
    "dob_info": "01.2002",
    "issue_date": "31.01.2002",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "newdb_qid": "EKYiIMO21ZnJMygA",
    "taskId": "test-rkl-003"
  },
  "requestId": "optional-string",
  "webhook": "https://your.host/webhook"
}
```

### Пример API-запроса (`dob_info` = только год)

Для `dob_info = "2002"` spider выберет режим "Только год" (`optional = "2"`), в форме будет выбран год `2002`.

```json
{
  "params": {
    "method": "rkl",
    "country": "ru",
    "lastname": "Зиёдулла",
    "firstname": "Бегимов",
    "secondname": "Камолович ",
    "dob_info": "2002",
    "issue_date": "31.01.2002",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "newdb_qid": "EKYiIMO21ZnJMygA",
    "taskId": "test-rkl-003-year"
  },
  "requestId": "optional-string",
  "webhook": "https://your.host/webhook"
}
```

### Пример API-запроса (`dob_info` = полная дата)

Для `dob_info = "31.01.2002"` spider выберет режим "Полная дата" (`optional = "1"`), поле даты рождения будет заполнено значением `31012002`.

```json
{
  "params": {
    "method": "rkl",
    "country": "ru",
    "lastname": "Зиёдулла",
    "firstname": "Бегимов",
    "secondname": "Камолович ",
    "dob_info": "31.01.2002",
    "issue_date": "31.01.2002",
    "id_doc_seria": "FA",
    "id_doc_number": "2001901",
    "newdb_qid": "EKYiIMO21ZnJMygA",
    "taskId": "test-rkl-003-full-date"
  },
  "requestId": "optional-string",
  "webhook": "https://your.host/webhook"
}
```

## Входные параметры (`params`)

```json
{
  "method": "rkl",
  "country": "ru",
  "lastname": "string",
  "firstname": "string",
  "secondname": "string",
  "dob_info": "string",
  "issue_date": "string",
  "id_doc_seria": "string",
  "id_doc_number": "string",
  "taskId": "string"
}
```

Основные поля:

- `id_doc_seria` — серия документа.
- `id_doc_number` — номер документа (обязательное поле).
- `issue_date` — дата выдачи документа (обязательное поле, нормализуется в `DD.MM.YYYY`).
- `dob_info` — дата рождения в полном или частичном формате (подробно ниже).

## `dob_info`: как парсится

Поле `dob_info` поддерживает несколько форматов. По нему spider определяет, какой режим даты рождения выбрать в форме.

Поддерживаемые форматы:

- `DD.MM.YYYY` (также допускаются разделители `-`, `/`) -> полная дата рождения.
- `MM.YYYY` (также `MM-YYYY`, `MM/YYYY`) -> месяц и год рождения.
- `YYYY` -> только год рождения.
- `YYYY.MM` / `YYYY-MM` / `YYYY/MM` -> также принимается для обратной совместимости и трактуется как год+месяц.

Дополнительно:

- Если переданы `optional`, `by`, `bm`, `bd`, то они имеют приоритет над `dob_info`.
- Если `dob_info` не совпал с шаблонами, используется `dateutil.parse(..., dayfirst=True)` как fallback.

## `dob_info`: как выставляется в форме

Spider переводит `dob_info` в один из режимов формы:

- `optional = "1"` (полная дата):
  - заполняется поле `c_birth_date`
  - значение вводится как `DDMMYYYY` (цифрами, без разделителей)
- `optional = "3"` (месяц и год):
  - включается чекбокс "дата рождения указана не полностью"
  - выбирается radio `radio_birth_date = 1` ("Месяц и год")
  - заполняется month-picker `c_birth_month_and_year`
- `optional = "2"` (только год):
  - включается чекбокс "дата рождения указана не полностью"
  - выбирается radio `radio_birth_date = 2` ("Только год")
  - выбирается год в dropdown `c_birth_year`

### Примеры

- `dob_info = "01.2002"` -> режим "Месяц и год", в форме: `Янв 2002`
- `dob_info = "2002"` -> режим "Только год", в форме: `2002`
- `dob_info = "31.01.2002"` -> режим "Полная дата", в форме поле даты: `31012002`

## Валидация и ошибки

- Для полной даты (`optional = "1"`) требуется корректная `dob_info`, иначе будет ошибка `dob_info is required`.
- Для частичной даты (`optional = "2"` / `optional = "3"`) обязателен год (`by`), иначе будет ошибка `birth year is required for partial date mode`.
- Если месяц некорректный (не `1..12`) в режиме `MM.YYYY`, будет ошибка `Invalid month for partial DOB`.

## Пример ответа

Ниже пример структуры ответа NEWDB для метода `rkl`. Значение `registry_status` определяется из текста результата на экране Госуслуг:

Формат ответа одинаковый для всех вариантов `dob_info` (`MM.YYYY`, `YYYY`, `DD.MM.YYYY`); меняется только значение, переданное в `params.dob_info`.

- `not_found` — если в заголовке найдено "отсутствует в реестре контролируемых лиц"
- `found` — если в заголовке найдено "в реестре контролируемых лиц"
- `unknown` — если статус не удалось определить по заголовку

```json
{
  "params": {
    "params": {
      "method": "rkl",
      "country": "ru",
      "lastname": "Зиёдулла",
      "firstname": "Бегимов",
      "secondname": "Камолович ",
      "dob_info": "01.2002",
      "issue_date": "31.01.2002",
      "id_doc_seria": "FA",
      "id_doc_number": "2001901",
      "newdb_qid": "EKYiIMO21ZnJMygA",
      "taskId": "test-rkl-003"
    }
  },
  "requestId": "optional-string",
  "state": "complete",
  "results": {
    "rkl": {
      "taskId": "test-rkl-003",
      "dateupdated": "2026-02-25 12:00:00",
      "result": {
        "status": 200,
        "data": [
          {
            "title": "Сведения о проверяемом лице отсутствуют в реестре контролируемых лиц",
            "details": [
              "Проверка выполнена по данным документа и дате рождения."
            ],
            "raw": "Сведения о проверяемом лице отсутствуют в реестре контролируемых лиц Проверка выполнена по данным документа и дате рождения.",
            "registry_status": "not_found"
          }
        ]
      }
    }
  }
}
```
