# БР-7 — POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при невалидном типе или формате id продукта в productsList

- **Приоритет:** Major
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://b9c52f5b-aed7-4de2-a78b-69c29b57eb0d.serverhub.praktikum-services.ru/api/v1/kits/9/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": [
    {
      "quantity": 1,
      "id": 1.5
    }
  ]
}'

## Шаги воспроизведения

1. Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. В body передать productsList с невалидным значением id продукта: 
            1.5, 
             null, 
             строка "12", 
             "apple", 
             "яблоко", 
             "%_", 
             массив [1,2,3],
             объект {},
             true,
             false,
             9999999999, 
             либо не передать поле id внутри объекта продукта.
4. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с понятным сообщением о невалидном id продукта. Продукт в набор не добавляется.

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
