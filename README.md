Оформление задачи находится в predict-user-order.ipynb

# Overview

Нам доступны данные сервиса доставки продуктов ozon fresh https://www.ozon.ru/category/supermarket-25000/?miniapp=supermarket.

Для оценки бюджета маркетинга, вам нужно предсказать, совершит ли пользователь любую покупку за следующий месяц (с 2024-08-01 по 2024-08-31).

Все данные доступны за часть 2024 года (в данных могут быть выбросы), но не позднее 2024-07-31.

Подробнее про данные смотрите в разделе Data.

# Data

## Files

- `actions_history` - parquet, кликстрим пользователей в ozon fresh (нет данных о просмотрах товаров)
- `search_history` - parquet, история поисковых запросов
- `product_information.csv` - информация о товарах из ozon fresh
- `action_type_info.csv` - расшифровка действий из кликстрима
- `widget_info.csv` - расшифровка названий виджетов
- `test_users.csv` - id юзеров, для которых нужно предсказать вероятность покупки в следующий месяц
- `baseline_1_submission.csv` - пример submission из baseline_1.ipynb

## actions_history Columns

- `user_id` - id пользователя
- `timestamp` - timestamp совершенного действия
- `product_id` - id товара
- `page_product_id` - id товара, на странице которого было совершенно действие (например, вы кликнули на товар молоко из виджета рекомендаций, находясь на - странице кефира, тогда молоко - product_id, кефир - page_product_id)
- `action_type_id` - id действия, смотри action_type_info.csv
- `widget_name_id` - id виджета, смотри widget_info.csv

## search_history Columns

- `user_id` - id пользователя
- `timestamp` - timestamp совершенного действия
- `search_query` - текст запроса
- `action_type_id` - id действия, смотри action_type_info.csv
- `widget_name_id` - id виджета, смотри widget_info.csv

## product_information.csv Columns

- `product_id` - id товара
- `name` - полное название товара
- `brand` - название бренда товара
- `type` - тип товара
- `category_id` - id категории товара
- `category_name` - название категории
- `price` - цена товара
- `discount_price` - цена товара со скидкой

# Evaluation

Метрика качества - ROC AUC.