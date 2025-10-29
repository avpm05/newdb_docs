# NEWDB API Documentation

Добро пожаловать в документацию API для NEWDB.

## Пример запроса

```bash
curl -X POST "{{api_prod}}" \
  -H "Content-Type: application/json" \
  -H "X-API-KEY: {{token}}" \
  -d '{ "params": { "seria": "4115", "number": "350298" }, "requestId": "32ec1efd" }'
```