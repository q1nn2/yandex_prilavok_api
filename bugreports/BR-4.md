# БР-4 — POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при невалидном типе поля productsList

- **Приоритет:** Major
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://b9c52f5b-aed7-4de2-a78b-69c29b57eb0d.serverhub.praktikum-services.ru/api/v1/kits/null/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": null
}'

## Шаги воспроизведения

1. Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. В body передать productsList в одном из невалидных типов: 
                                                         null, 
                                                         строка "123", 
                                                         число 13, 
                                                         объект {"id":1,"quantity":1}, 
                                                         true, 
                                                         false.
4. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с понятным сообщением о некорректном типе поля productsList.

## ФР

Сервер возвращает 500 Internal Server Error.

## Комментарий

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <title>Error</title>
</head>

<body>
    <pre>Internal Server Error</pre>
</body>

</html>

## Окружение

Windows 11 Pro 21H2; 
Тестовый стенд API; 
Яндекс.Прилавок 3.1.1.
