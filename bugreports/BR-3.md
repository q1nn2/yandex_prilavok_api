# БР-3 — POST /api/v1/kits/{id}/products возвращает 200 OK при отсутствующем, пустом или неверно названном поле productsList

- **Приоритет:** Major
- **Статус:** Open

## Предусловия

Создать набор:

curl --location 'https://948b8d20-2d67-4144-b8a9-76f38b79fc75.serverhub.praktikum-services.ru/api/v1/kits/7/products' \
--header 'Content-Type: application/json' \
--data '{}'

## Шаги воспроизведения

1.Отправить POST-запрос на /api/v1/kits/{id}/products.
2. В path-параметр id передать id существующего набора.
3. Передать один из вариантов body:
                                   без поля productsList;
                                   "productsList": [];
                                   поле productList вместо productsList.
4.Нажать Send.

## Постусловия

Проверить БД

## ОР

Сервер возвращает 400 Bad Request с сообщением о некорректном теле запроса. Продукты в набор не добавляются.

## ФР

Сервер возвращает 200 OK, хотя обязательное поле productsList отсутствует, пустое или передано с неправильным названием.

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
