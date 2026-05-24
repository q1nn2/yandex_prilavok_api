# БР-8 — POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при отсутствующем или невалидном типе quantity

- **Приоритет:** Major
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://b9c52f5b-aed7-4de2-a78b-69c29b57eb0d.serverhub.praktikum-services.ru/api/v1/kits/12/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": [
    {
      "id": 1
    }
  ]
}'

## Шаги воспроизведения

1. Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. В body передать productsList с некорректным quantity: 
              не передать поле quantity,
              передать массив [1,2,3] или объект {}.
4. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с понятным сообщением о некорректном поле quantity.

## ФР

Сервер возвращает 500 Internal Server Error

## Комментарий

{
    "code": 500,
    "message": "invalid input syntax for integer: \"NaN\""
}

## Окружение

Windows 11 Pro 21H2; 
Тестовый стенд API; 
Яндекс.Прилавок 3.1.1.
