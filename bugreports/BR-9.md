# БР-9 — POST /api/v1/kits/{id}/products возвращает 200 OK при невалидном значении quantity

- **Приоритет:** Critical
- **Статус:** Open

## Предусловия

Создать набор:


curl --location 'https://b9c52f5b-aed7-4de2-a78b-69c29b57eb0d.serverhub.praktikum-services.ru/api/v1/kits/12/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": [
    {
      "id": 1,
      "quantity": 0
    }
  ]
}'

## Шаги воспроизведения

1. Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. В body передать productsList с невалидным значением quantity: 
               0, 
              -1, 
               1.5, 
               null или строку "12".
4. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с понятным сообщением о невалидном значении quantity.

## ФР

Сервер возвращает 200 OK. Запрос считается успешным при передаче невалидного значения quantity.

Комментарий

## Комментарий

{
    "id": 12,
    "name": "Test Kit API",
    "productsList": [
        {
            "id": 1,
            "name": "Сок Jumex апельсин без сахара",
            "price": 149,
            "weight": 473,
            "units": "мл",
            "quantity": 34
        }
    ],
    "productsCount": 34
}

## Окружение

Windows 11 Pro 21H2; 
Тестовый стенд API; 
Яндекс.Прилавок 3.1.1.
