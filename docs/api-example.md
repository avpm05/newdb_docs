---
title: "Пример вызова API"
description: "Синхронный и асинхронный варианты вызова API с примерами запросов и ответов."
---

# Пример вызова API

Ниже приведены два типовых сценария: синхронный (ожидание результата в одном запросе) и асинхронный (запрос + отдельное получение результата).

## Синхронный метод (run)

Синхронный режим ставит задачу в очередь и удерживает соединение до получения результата или таймаута. Максимальное время ожидания — 3600 секунд. Если `requestId` не передан, он будет создан автоматически. Если `requestId` уже существует, API вернёт ранее сохранённый результат.

**Пример запроса**

```http
GET https://api.newdb.net/v2/run?method=passport_mvd&seria=4115&number=350298&firstname=Александр&lastname=Сидоров&country=ru&token=<your_token>&requestId=<uuid4>
```

**Успешный ответ (пример)**

```json
{
  "requestId": "b4c61a6b-34cc-430e-bbeb-a6518014bca4",
  "state": "complete",
  "results": {
    "passport_mvd": {
      "result": {
        "status": 200,
        "data": [
          {
            "doc_status": "Данные не найдены"
          }
        ]
      }
    }
  }
}
```

**Ответ по таймауту**

```json
{
  "requestId": "b4c61a6b-34cc-430e-bbeb-a6518014bca4",
  "state": "timeout",
  "error": "Task execution timeout"
}
```

## Асинхронный метод (run + data)

Асинхронный режим состоит из двух шагов: отправка запроса и последующее получение результата по `requestId`.

**Шаг 1. Отправка запроса**

Отправьте POST на `https://api.newdb.net/v2` и передайте токен в заголовке `X-API-KEY`.

```json
{
  "params": {
    "seria": "4115",
    "number": "350298",
    "method": "passport_mvd",
    "firstname": "Александр",
    "lastname": "Сидоров",
    "country": "ru"
  },
  "requestId": "b4c61a6b-34cc-430e-bbeb-a6518014bca4"
}
```

**Шаг 2. Получение результата**

```http
GET https://api.newdb.net/v2/data?requestId=b4c61a6b-34cc-430e-bbeb-a6518014bca4
```

**Пример ответа**

```json
{
  "params": {
    "seria": "4115",
    "number": "350298",
    "method": "passport_mvd",
    "firstname": "Александр",
    "lastname": "Сидоров",
    "country": "ru",
    "newdb_qid": "EL4VILiX9MW7MygB"
  },
  "requestId": "b4c61a6b-34cc-430e-bbeb-a6518014bca4",
  "datecreated": "2026-01-13 22:02:33",
  "state": "complete",
  "balance": 9884,
  "tasks": 1,
  "is_repeat": false,
  "results": {
    "passport_mvd": {
      "taskId": "f7bb40dd-703c-40c6-8c9b-2a0d4306f90b",
      "dateupdated": "2026-01-13 22:03:19",
      "result": {
        "status": 200,
        "data": [
          {
            "doc_status": "Данные не найдены"
          }
        ]
      }
    }
  }
}
```
