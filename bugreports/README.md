# Баг-репорты

Всего дефектов: **25**.

| ID | Название | Приоритет | Статус |
|----|----------|-----------|--------|
| [БР-1](BR-1.md) | POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при передаче невалидного id набора | Major | Open |
| [БР-2](BR-2.md) | POST /api/v1/kits/{id}/products возвращает 200 OK при добавлении продуктов сверх ограничения 30 товаров | Critical | Open |
| [БР-3](BR-3.md) | POST /api/v1/kits/{id}/products возвращает 200 OK при отсутствующем, пустом или неверно названном поле productsList | Major | Open |
| [БР-4](BR-4.md) | POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при невалидном типе поля productsList | Major | Open |
| [БР-5](BR-5.md) | POST /api/v1/kits/{id}/products возвращает 200 OK при Content-Type: text/plain | Major | Open |
| [БР-6](BR-6.md) | POST /api/v1/kits/{id}/products возвращает 200 OK при добавлении продукта с несуществующим, нулевым или отрицательным id | Critical | Open |
| [БР-7](BR-7.md) | POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при невалидном типе или формате id продукта в productsList | Major | Open |
| [БР-8](BR-8.md) | POST /api/v1/kits/{id}/products возвращает 500 Internal Server Error при отсутствующем или невалидном типе quantity | Major | Open |
| [БР-9](BR-9.md) | POST /api/v1/kits/{id}/products возвращает 200 OK при невалидном значении quantity | Critical | Open |
| [БР-10](BR-10.md) | POST /fast-delivery/v3.1.1/calculate-delivery.xml возвращает 500 Internal Server Error при невалидном XML-запросе или отсутствии обязательных XML-элементов | Major | Open |
| [БР-11](BR-11.md) | POST /fast-delivery/v3.1.1/calculate-delivery.xml возвращает 200 OK при пустых обязательных XML-элементах | Major | Open |
| [БР-12](BR-12.md) | POST /fast-delivery/v3.1.1/calculate-delivery.xml возвращает 200 OK при невалидном значении deliveryTime | Major | Open |
| [БР-13](BR-13.md) | POST /fast-delivery/v3.1.1/calculate-delivery.xml возвращает 200 OK при невалидном значении productsCount | Major | Open |
| [БР-14](BR-14.md) | POST /fast-delivery/v3.1.1/calculate-delivery.xml возвращает 200 OK при невалидном значении productsWeight | Major | Open |
| [БР-15](BR-15.md) | PUT /api/v1/orders/{id} возвращает 500 Internal Server Error при невалидном id корзины | Major | Open |
| [БР-16](BR-16.md) | PUT /api/v1/orders/{id} возвращает 200 OK при отсутствующем, пустом или неверно названном поле productsList | Major | Open |
| [БР-17](BR-17.md) | PUT /api/v1/orders/{id} возвращает 500 Internal Server Error при невалидном типе поля productsList | Major | Open |
| [БР-18](BR-18.md) | PUT /api/v1/orders/{id} возвращает 200 OK при Content-Type: text/plain | Major | Open |
| [БР-19](BR-19.md) | PUT /api/v1/orders/{id} возвращает 409 Conflict вместо ошибки валидации при невалидном id продукта в productsList | Major | Open |
| [БР-20](BR-20.md) | PUT /api/v1/orders/{id} возвращает 500 Internal Server Error при невалидном типе или формате id продукта в productsList | Major | Open |
| [БР-21](BR-21.md) | PUT /api/v1/orders/{id} возвращает 200 OK при невалидном значении quantity в productsList | Critical | Open |
| [БР-22](BR-22.md) | PUT /api/v1/orders/{id} возвращает 409 Conflict вместо ошибки валидации при невалидном типе quantity | Major | Open |
| [БР-23](BR-23.md) | GET /api/v1/orders/{id} возвращает 500 Internal Server Error при невалидном id корзины | Major | Open |
| [БР-24](BR-24.md) | DELETE /api/v1/orders/{id} возвращает 404 Not Found при удалении существующей корзины | Critical | Open |
| [БР-25](BR-25.md) | POST /fast-delivery/v3.1.1/calculate-delivery.xml возвращает 200 OK без сообщения о невозможности доставки вне рабочего времени | Major | Open |
