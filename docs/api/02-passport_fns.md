# inn_company — Проверка юридического лица по ИНН

POST `https://api.newdb.net/v2`

Проверка паспорта и ИНН через сервисы ФНС.

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
    "dob": "string" //yyyy-mm-dd,
    "country": "ru",
    "method": "passport_fns"
  },
  "webhook": "https://webhook_url/",
  "requestId": "19342f89-2916-4779-b59d-43c012f1a781"
}
```

## Пример запроса
```http
POST /v2  HTTP/1.1
Host: api.newdb.net
Content-Type: application/json
X-API-KEY: YOUR_TOKEN

{
"params":{
"seria":"4015",
"number":"350278",
"firstname": "Александр", 
"secondname": "Сергеевич",
"lastname": "Малина", 

"dob": "1990-12-17",
"country": "ru",
"method":"passport_fns"
},
"webhook":"https://webhook_url/",
"requestId":"19342f89-2916-4779-b59d-43c012f1a781"
}
```

## Пример ответа (ИНН найден)
```json
{
  "state": "complete",
  "results": {
    "company": {
      "result": {
        "status": 200,
        "data": [
          { "innfiz": "7703245603"  }
        ]
      }
    }
  }
}
```


## Пример ответа (ИНН не найден)
```json
{
  "state": "complete",
  "results": {
    "company": {
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
      "name": "inn_company",
      "description": "Проверка паспорта РФ и ИНН через ФНС России",
      "input_schema": {
        "innyur": "string",
        "country": "string"
      },
      "headers_required": ["X-API-KEY"]
    }
  ],
  "policy": "Если пользователь прислал  паспортаные данные — вызывай passport_fns и верни сведения по ИНН ."
}
```
