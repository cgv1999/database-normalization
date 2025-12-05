# Нормализация базы данных

## Описание проекта
Проект демонстрирует процесс нормализации базы данных от первой нормальной формы (1НФ) до третьей нормальной формы (3НФ) на примере данных о транзакциях и клиентах.

## Цель
- Привести базу данных к 3НФ
- Устранить избыточность данных
- Обеспечить целостность данных через внешние ключи
- Создать оптимальную структуру для хранения данных

## Исходные данные
Исходно имелись две денормализованные таблицы:
- `transaction` - данные о транзакциях
- `customer` - данные о клиентах

## Нормализованная структура
После нормализации создано 4 таблицы:

### Таблицы:
1. **locations** - географические данные (86 записей)
2. **customers** - данные клиентов (99 записей) 
3. **products** - данные продуктов (61 запись)
4. **transactions** - данные транзакций (4 записи)

### Связи:
- customers → locations (один-ко-многим)
- transactions → customers (один-ко-многим)
- transactions → products (один-ко-многим)

## Структура базы данных
```sql
Table locations {
  postcode VARCHAR(10) [primary key]
  state VARCHAR(50) [not null]
  country VARCHAR(50) [not null]
}

Table customers {
  customer_id INTEGER [primary key]
  first_name VARCHAR(100)
  last_name VARCHAR(100)
  gender VARCHAR(10)
  dob DATE
  job_title VARCHAR(100)
  job_industry_category VARCHAR(100)
  wealth_segment VARCHAR(50)
  deceased_indicator VARCHAR(1)
  owns_car VARCHAR(3)
  address VARCHAR(200)
  postcode VARCHAR(10)
  property_valuation INTEGER
}

Table products {
  product_id INTEGER [primary key]
  brand VARCHAR(100) [not null]
  product_line VARCHAR(50)
  product_class VARCHAR(20)
  product_size VARCHAR(20)
  standard_cost DECIMAL(10,2)
}

Table transactions {
  transaction_id INTEGER [primary key]
  product_id INTEGER [not null]
  customer_id INTEGER [not null]
  transaction_date DATE
  online_order BOOLEAN
  order_status VARCHAR(50)
  list_price DECIMAL(10,2)
}

Ref: customers.postcode > locations.postcode
Ref: transactions.customer_id > customers.customer_id  
Ref: transactions.product_id > products.product_id
```

## Достигнутые нормальные формы
- **1НФ** - Все значения атомарны, нет повторяющихся групп
- **2НФ** - Все неключевые атрибуты зависят от полного первичного ключа
- **3НФ** - Нет транзитивных зависимостей

## Технологии
- PostgreSQL
- DBeaver
- SQL
