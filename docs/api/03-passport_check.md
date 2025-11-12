# passport_check — Проверка паспорта РФ

POST `${{ extra.api_base_url }}/run`

Проверяет паспорт РФ по серии/номеру и (опционально) ФИО/дате рождения.

## Заголовки
```
Content-Type: application/json
X-API-KEY: <your_token>
```

## Входная схема (request)
```json
{
  "params": {
    "seria": "string",
    "number": "string",
    "firstname": "string",
    "lastname": "string",
    "secondname": "string",
    "dob": "YYYY-MM-DD",
    "method": "passport",
    "country": "ru"
  }
}
```

## Пример запроса
```http
POST /v2/run HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
  "params": {
    "seria": "0802",
    "number": "649286",
    "firstname": "Петр",
    "lastname": "Семенов",
    "secondname": "Николаевич",
    "dob": "1937-01-03",
    "country": "ru",
    "method": "passport"
  }
}
```

## Пример ответа
```json
{
    "params": {
        "seria": "0802",
        "number": "649116",
        "method": "passport_mvd",
        "firstname": "Петр",
        "lastname": "Иванов",
    },
    "requestId": "32ec1efd-3f6a-76a2-9c4b-68cbf4b52089",
    "token": "6fa1aa70-ecfe-41f5-b56e-d9da2b79fc90",
    "tasks": 203,
    "is_repeat": false,
    "results": {
        "passport_mvd": {
            "taskId": "a8e29673-2978-4e28-95a1-a42d0ad4328e",
            "dateupdated": "2025-11-05 08:49:13",
            "result": {
                "status": 200,
                "data": [
                    {
                        "status": "Действительный"
                    }
                ]
            }
        }
    },
    "finished": 1,
    "state": "complete",
    "datecreated": "2025-11-02 22:48:00"
}
```

## x-ai (метаданные для AI)
```json
{
  "tools": [
    {
      "name": "passport_check",
      "description": "Проверка паспорта РФ по серии и номеру",
      "input_schema": {
        "seria": "string",
        "number": "string",
        "firstname": "string",
        "lastname": "string",
        "secondname": "string",
        "dob": "YYYY-MM-DD",
        "country": "string"
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь просит проверить паспорт — спроси серию и номер, затем вызови passport_check."
}
```
