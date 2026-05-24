# БР-6 — POST /api/v1/kits/{id}/products возвращает 200 OK при добавлении продукта с несуществующим, нулевым или отрицательным id

- **Приоритет:** Critical
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://b9c52f5b-aed7-4de2-a78b-69c29b57eb0d.serverhub.praktikum-services.ru/api/v1/kits/9/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": [
    {
      "quantity": 1,
      "id": 999999
    }
  ]
}'

## Шаги воспроизведения

1. Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. В body передать productsList с некорректным id продукта: 
                                                        999999, 
                                                        0 или -1.
4. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с понятным сообщением о невалидном продукте. Продукт в набор не добавляется.

## ФР

Сервер возвращает 200 OK. Запрос считается успешным при передаче id продукта, которого нет в БД, а также при id = 0 и id = -1.

## Комментарий

{
    "id": 9,
    "name": "Test Kit API",
    "productsList": [
        {
            "id": 1,
            "name": "Сок Jumex апельсин без сахара",
            "price": 149,
            "weight": 473,
            "units": "мл",
            "quantity": 1
        },
        {
            "quantity": 1
        }
    ],
    "productsCount": 2
}

## Окружение

Windows 11 Pro 21H2; 
Тестовый стенд API; 
Яндекс.Прилавок 3.1.1.
