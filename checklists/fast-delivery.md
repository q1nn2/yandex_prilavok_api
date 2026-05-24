# Couriers — Расчёт доставки "Привезём быстро"

Источник: `Чек-лист и результаты выполнения тестов API Яндекс.Прилавок 3.1.1`.

## Couriers — Расчёт доставки "Привезём быстро" POST /fast-delivery/v3.1.1/calculate-delivery.xml

### Формат XML и обязательные поля

| № | Описание | ОР | Статус | Баг-репорт |
|---:|----------|----|--------|------------|
| 68 | Отправить валидный XML с productsCount=2, productsWeight=1.5, deliveryTime=9 | 200 OK; ответ в XML; response@name='Привезём быстро'; есть isItPossibleToDeliver, hostDeliveryCost, clientDeliveryCost, toBeDeliveredTime. | PASSED |  |
| 69 | Проверить, что ответ содержит время доставки 25-30 минут при валидном запросе | 200 OK; в ответе toBeDeliveredTime/min=25 и toBeDeliveredTime/max=30. | PASSED |  |
| 70 | Проверить расчёт стоимости доставки при productsCount = 5, productsWeight = 1, deliveryTime = 9 | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 71 | Проверить расчёт стоимости доставки при productsCount = 8, productsWeight = 1, deliveryTime = 9 | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=43; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 71.1 | Проверить расчёт стоимости доставки при productsCount = 1, productsWeight = 2.6, deliveryTime = 9 | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=43; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 72 | Отправить запрос без элемента productsCount | 400 Bad Request; обязательный параметр productsCount не принят. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 73 | Отправить запрос без элемента productsWeight | 400 Bad Request; обязательный параметр productsWeight не принят. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 74 | Отправить запрос без элемента deliveryTime | 400 Bad Request; обязательный параметр deliveryTime не принят. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 75 | Отправить пустое тело запроса | 400 Bad Request; обязательные XML-элементы отсутствуют. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 76 | Отправить невалидный XML с незакрытым тегом | 400 Bad Request; XML не распарсен; расчёт доставки не выполнен. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 77 | Отправить XML с неправильным корневым элементом | 400 Bad Request; структура запроса не соответствует документации. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 78 | Отправить JSON вместо XML | 400 Bad Request; расчёт доставки не выполнен. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 79 | Отправить валидный XML с Content-Type: application/json | 400 Bad Request; тело не принято как XML. | FAILED | [БР-10](../bugreports/BR-10.md) |
| 80 | Отправить XML с пустыми элементами productsCount, productsWeight и deliveryTime | 400 Bad Request; пустые значения обязательных параметров не приняты. | FAILED | [БР-11](../bugreports/BR-11.md) |

### deliveryTime

| № | Описание | ОР | Статус | Баг-репорт |
|---:|----------|----|--------|------------|
| 81 | Передать deliveryTime = 7 — начало рабочего времени службы | 200 OK; isItPossibleToDeliver='true'. | PASSED |  |
| 82 | Передать deliveryTime = 8 — внутри рабочего времени службы | 200 OK; isItPossibleToDeliver='true'. | PASSED |  |
| 83 | Передать deliveryTime = 20 — внутри рабочего времени службы | 200 OK; isItPossibleToDeliver='true'. | PASSED |  |
| 84 | Передать deliveryTime = 21 — конец рабочего времени службы | 200 OK; isItPossibleToDeliver='true'. | PASSED |  |
| 85 | Передать deliveryTime = 6 — до начала рабочего времени | 200 OK; isItPossibleToDeliver='false'; доставка службой недоступна. | FAILED | [БР-25](../bugreports/BR-25.md) |
| 86 | Передать deliveryTime = 22 — после окончания рабочего времени | 200 OK; isItPossibleToDeliver='false'; доставка службой недоступна. | FAILED | [БР-25](../bugreports/BR-25.md) |
| 87 | Передать deliveryTime = 23 — после окончания рабочего времени | 200 OK; isItPossibleToDeliver='false'; доставка службой недоступна. | FAILED | [БР-25](../bugreports/BR-25.md) |
| 88 | Передать deliveryTime = 0 — вне рабочего времени | 200 OK; isItPossibleToDeliver='false'; доставка службой недоступна. | FAILED | [БР-25](../bugreports/BR-25.md) |
| 89 | Передать deliveryTime = -1 | 400 Bad Request; время доставки не принято. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 90 | Передать deliveryTime = 24 | 400 Bad Request; время доставки должно быть в диапазоне 0-23. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 91 | Передать deliveryTime = 20.5 | 400 Bad Request; время доставки должно быть целым числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 92 | Передать deliveryTime = null | 400 Bad Request; время доставки обязательно. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 93 | Передать deliveryTime как строку с числом '20' | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 94 | Передать deliveryTime как строку с русскими буквами 'Привет' | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 95 | Передать deliveryTime как строку с английскими буквами 'Hello' | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 96 | Передать deliveryTime со спецсимволами '%_' | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 97 | Передать deliveryTime как массив [1,2,3] | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 98 | Передать deliveryTime как объект {} | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 99 | Передать deliveryTime как true | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |
| 100 | Передать deliveryTime как false | 400 Bad Request; время доставки должно быть числом. | FAILED | [БР-12](../bugreports/BR-12.md) |

### productsCount

| № | Описание | ОР | Статус | Баг-репорт |
|---:|----------|----|--------|------------|
| 101 | Передать productsCount = 0 при productsWeight = 1 и deliveryTime = 9 | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 102 | Передать productsCount = 1 при productsWeight = 1 и deliveryTime = 9 | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 103 | Передать productsCount = 7 при productsWeight = 1 и deliveryTime = 9 — верхняя граница дешёвого тарифа | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 104 | Передать productsCount = 8 при productsWeight = 1 и deliveryTime = 9 — нижняя граница второго тарифа | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=43; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 105 | Передать productsCount = 14 при productsWeight = 1 и deliveryTime = 9 — верхняя граница второго тарифа | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=43; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 106 | Передать productsCount = 15 при productsWeight = 1 и deliveryTime = 9 — выше лимита службы | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=99; hostDeliveryCost=43; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 107 | Передать productsCount = -1 при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров не принято. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 108 | Передать productsCount = 1.5 при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть целым числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 109 | Передать productsCount = null при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров обязательно. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 110 | Передать productsCount как строку с числом '20' при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 111 | Передать productsCount как строку с русскими буквами 'Привет' при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 112 | Передать productsCount как строку с английскими буквами 'Hello' при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 113 | Передать productsCount со спецсимволами '%_' при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 114 | Передать productsCount как массив [1,2,3] при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 115 | Передать productsCount как объект {} при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 116 | Передать productsCount как true при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 117 | Передать productsCount как false при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; количество товаров должно быть числом. | FAILED | [БР-13](../bugreports/BR-13.md) |
| 118 | Передать productsCount за пределами int = 9999999999 при productsWeight = 1 и deliveryTime = 9 | 400 Bad Request; некорректное количество товаров не принято. | FAILED | [БР-13](../bugreports/BR-13.md) |

### productsWeight

| № | Описание | ОР | Статус | Баг-репорт |
|---:|----------|----|--------|------------|
| 119 | Передать productsWeight = 0 при productsCount = 1 и deliveryTime = 9 | 200 OK; isPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; deliveryTime=25-30. | PASSED |  |
| 120 | Передать productsWeight = 0.1 при productsCount = 1 и deliveryTime = 9 | 200 OK; isPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; deliveryTime=25-30. | PASSED |  |
| 121 | Передать productsWeight = 2.5 при productsCount = 1 и deliveryTime = 9 — верхняя граница дешёвого тарифа | 200 OK; isPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=23; deliveryTime=25-30. | PASSED |  |
| 122 | Передать productsWeight = 2.6 при productsCount = 1 и deliveryTime = 9 — нижняя граница второго тарифа | 200 OK; isPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=43; deliveryTime=25-30. | PASSED |  |
| 123 | Передать productsWeight = 6.0 при productsCount = 1 и deliveryTime = 9 — верхняя граница второго тарифа | 200 OK; isPossibleToDeliver=true; clientDeliveryCost=0; hostDeliveryCost=43; deliveryTime=25-30. | PASSED |  |
| 124 | Передать productsWeight = 6.1 при productsCount = 1 и deliveryTime = 9 — выше лимита службы | 200 OK; isItPossibleToDeliver=true; clientDeliveryCost=99; hostDeliveryCost=43; toBeDeliveredTime min=25, max=30. | PASSED |  |
| 125 | Передать productsWeight = -0.1 при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров не принят. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 126 | Передать productsWeight = null при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров обязателен. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 127 | Передать productsWeight как строку с числом '2.5' при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 128 | Передать productsWeight как строку с русскими буквами 'Привет' при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 129 | Передать productsWeight как строку с английскими буквами 'Hello' при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 130 | Передать productsWeight со спецсимволами '%_' при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 131 | Передать productsWeight как массив [1,2,3] при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 132 | Передать productsWeight как объект {} при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 133 | Передать productsWeight как true при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 134 | Передать productsWeight как false при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; вес товаров должен быть числом. | FAILED | [БР-14](../bugreports/BR-14.md) |
| 135 | Передать productsWeight за пределами разумного диапазона = 99999999 при productsCount = 1 и deliveryTime = 9 | 400 Bad Request; некорректный вес товаров не принят. | FAILED | [БР-14](../bugreports/BR-14.md) |
