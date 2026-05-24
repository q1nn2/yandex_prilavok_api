# БР-1 — POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при передаче невалидного id набора

- **Приоритет:** Major
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://948b8d20-2d67-4144-b8a9-76f38b79fc75.serverhub.praktikum-services.ru/api/v1/kits/1.5/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": [
    {
      "id": 1,
      "quantity": 1
    }
  ]
}'

## Шаги воспроизведения

1.Отправить POST-запрос на /api/v1/kits/{id}/products.
2.В path-параметр id передать невалидное значение: 1.5, tomato, Привет, @3, 9999999999, null, true или false.
3.Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с понятным сообщением о невалидном id набора. Продукт в набор не добавляется.

## ФР

Сервер возвращает 500 Internal Server Error. Для значений id = 1.5, tomato, Привет, @3, 9999999999, null, true, false запрос падает с серверной ошибкой.

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
