# Яндекс Прилавок — API Manual QA

Ручное тестирование API сервиса **Яндекс Прилавок 3.1.1**: проверка REST/XML endpoints, негативные сценарии, валидация параметров и оформление баг-репортов.

![Manual QA](https://img.shields.io/badge/Type-API%20Manual%20QA-blue)
![Scope](https://img.shields.io/badge/Scope-Checklist%20%2B%20Bug%20Reports-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Focus](https://img.shields.io/badge/Focus-REST%20%26%20XML-purple)
![Bugs](https://img.shields.io/badge/Bugs-25_total%20%7C%205_critical-red)

---

## Содержание

- [Описание](#описание)
- [Ссылки](#ссылки)
- [Артефакты](#артефакты)
- [Ключевые дефекты](#ключевые-дефекты)
- [Итоги тестирования](#итоги-тестирования)
- [Окружение](#окружение)
- [Вывод](#вывод)
- [Автор](#автор)

---

## Описание

Цель работы — оценить качество реализации API **Яндекс Прилавок 3.1.1** по ключевым сценариям:

- добавление продуктов в набор через `POST /api/v1/kits/{id}/products`;
- расчёт быстрой доставки через `POST /fast-delivery/v3.1.1/calculate-delivery.xml`;
- добавление товаров в корзину через `PUT /api/v1/orders/{id}`;
- получение продуктов в корзине через `GET /api/v1/orders/{id}`;
- удаление корзины через `DELETE /api/v1/orders/{id}`.

Основной фокус — негативные проверки валидации path-параметров, JSON/XML-тела запроса, типов данных, обязательных полей и граничных значений.

---

## Ссылки

- **Общая таблица проекта:** [Google Sheets — Яндекс Прилавок API](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit)
- **Чек-лист и результаты:** [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015)
- **Баг-репорты:** [gid=290693736](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=290693736#gid=290693736)

---

## Артефакты

| Артефакт | Формат | Google Sheets | GitHub |
|----------|--------|---------------|--------|
| Чек-лист API | Google Sheets | [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015) | [`checklists/`](checklists) |
| Main.Kits — добавление продуктов | Markdown | [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015) | [`checklists/kits-products.md`](checklists/kits-products.md) |
| Couriers — расчёт доставки XML | Markdown | [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015) | [`checklists/fast-delivery.md`](checklists/fast-delivery.md) |
| Main.Basket — добавление товаров | Markdown | [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015) | [`checklists/basket-put-orders.md`](checklists/basket-put-orders.md) |
| Main.Basket — получение продуктов | Markdown | [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015) | [`checklists/basket-get-orders.md`](checklists/basket-get-orders.md) |
| Main.Basket — удаление корзины | Markdown | [gid=2006427015](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=2006427015#gid=2006427015) | [`checklists/basket-delete-orders.md`](checklists/basket-delete-orders.md) |
| Баг-репорты | Markdown | [gid=290693736](https://docs.google.com/spreadsheets/d/1ExH5hJQVSB176ZGiANEou0rDb-ka-0HkGd2agBQe5AI/edit?gid=290693736#gid=290693736) | [`bugreports/`](bugreports) |

---

## Ключевые дефекты

**Критичные:** [БР-2](bugreports/BR-2.md), [БР-6](bugreports/BR-6.md), [БР-9](bugreports/BR-9.md), [БР-21](bugreports/BR-21.md), [БР-24](bugreports/BR-24.md).

**Major:** 20 дефектов, в основном по серверным ошибкам `500 Internal Server Error`, неверным успешным ответам `200 OK` на невалидные данные и некорректной обработке JSON/XML.

Наиболее рискованные зоны:

- endpoint `POST /api/v1/kits/{id}/products` принимает невалидные данные или падает с `500`;
- XML endpoint расчёта доставки возвращает успешные ответы на невалидные обязательные поля;
- `PUT /api/v1/orders/{id}` некорректно валидирует `productsList`, `id` и `quantity`;
- `GET`/`DELETE /api/v1/orders/{id}` возвращают серверные ошибки на невалидные path-параметры.

---

## Итоги тестирования

### Чек-лист API

| Метрика | Значение |
|--------|---------:|
| Всего проверок | **237** |
| Passed | **83** |
| Failed | **154** |

### Баг-репорты

| Метрика | Значение |
|--------|---------:|
| Всего багов | **25** |
| Critical | **5** |
| Major | **20** |
| Open | **25** |

### KPI

| Показатель | Значение |
|-----------|---------:|
| Pass Rate | **35.0%** (83/237) |
| Fail Rate | **65.0%** (154/237) |
| Доля Critical от общего числа багов | **20.0%** (5/25) |

---

## Окружение

- **OS:** Windows 11 Pro 21H2
- **Инструмент:** Postman / curl
- **Тестируемая версия:** Яндекс Прилавок 3.1.1
- **Тип тестирования:** API Manual QA

---

## Вывод

> По результатам проверки найдено **25** дефектов, включая **5 Critical**. Основные проблемы связаны с отсутствием корректной валидации входных данных, успешными ответами на невалидные запросы и серверными ошибками `500 Internal Server Error`.
>
> В текущем состоянии релиз **не рекомендуется** до исправления критичных дефектов и повторного API-регресса по затронутым endpoints.

---

## Автор

**Anatoly Elnikov**  
Manual QA Engineer
