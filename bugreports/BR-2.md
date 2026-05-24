# БР-2 — POST /api/v1/kits/{id}/products возвращает 200 OK при добавлении продуктов сверх ограничения 30 товаров

- **Приоритет:** Critical
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://948b8d20-2d67-4144-b8a9-76f38b79fc75.serverhub.praktikum-services.ru/api/v1/kits/7/products' \
--header 'Content-Type: application/json' \
--data '{
  "productsList": [
    {
      "id": 1,
      "quantity": 30
    }
  ]
}'

## Шаги воспроизведения

1.Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id= 7 существующего набора.
3. В body передать productsList, после добавления которого итоговое количество товаров в наборе станет 31.
4. Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request. Продукты не добавляются, потому что количество товаров в наборе не должно превышать 30.

## ФР

Сервер возвращает 200 OK. Запрос считается успешным, хотя итоговое количество товаров в наборе превышает 30.

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
            "quantity": 65
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
    "productsCount": 69
}

## Окружение

Windows 11 Pro 21H2; 
Тестовый стенд API; 
Яндекс.Прилавок 3.1.1.
