# БР-5 — POST /api/v1/kits/{id}/products возвращает 200 OK при Content-Type: text/plain

- **Приоритет:** Major
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://b9c52f5b-aed7-4de2-a78b-69c29b57eb0d.serverhub.praktikum-services.ru/api/v1/kits/7/products' \
--header 'Content-Type: text/plain' \
--data '{
  "productsList": [
    {
      "id": 1,
      "quantity": 1
    }
  ]
}'

## Шаги воспроизведения

1. Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. В body передать валидный JSON с productsList.
4. В Headers указать Content-Type: text/plain.
5. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request или 415 Unsupported Media Type(имхо), так как endpoint должен принимать JSON с Content-Type: application/json.

## ФР

Сервер возвращает 200 OK и обрабатывает запрос как успешный, несмотря на Content-Type: text/plain.

## Комментарий

{
    "id": 7,
    "name": "Test Kit API",
    "productsList": [
        {
            "id": 1,
            "name": "Сок Jumex апельсин без сахара",
            "price": 149,
            "weight": 473,
            "units": "мл",
            "quantity": 64
        },
        {
            "id": 2,
            "name": "Evervess Тоник напиток сильногазированный",
            "price": 89,
            "weight": 1,
            "units": "л",
            "quantity": 1
        },
        {
            "id": 3,
            "name": "Газированный напиток Pepsi",
            "price": 109,
            "weight": 1,
            "units": "л",
            "quantity": 1
        },
        {
            "id": 5,
            "name": "Сок Rich яблоко-киви-шпинат",
            "price": 349,
            "weight": 900,
            "units": "мл",
            "quantity": 1
        },
        {
            "id": 4,
            "name": "Sprite классический",
            "price": 79,
            "weight": 900,
            "units": "мл",
            "quantity": 1
        }
    ],
    "productsCount": 68
}

## Окружение

Windows 11 Pro 21H2; 
Тестовый стенд API; 
Яндекс.Прилавок 3.1.1.
