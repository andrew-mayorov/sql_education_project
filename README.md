# Marketplace SQL Analytics Portfolio

Учебный портфолио-проект по SQL для позиции **Data Analyst Intern / Junior Data Analyst**.  
Проект показывает, как с помощью SQL можно анализировать данные маркетплейса: продажи, клиентов, товары, маркетинг, доставку и обращения в поддержку.

Данные синтетические, но структура приближена к реальному продукту: есть клиенты, заказы, товарные строки, платежи, доставки, пользовательские сессии, маркетинговые расходы и тикеты поддержки.

## Цель проекта

Показать практические навыки аналитика данных:

- формулирование бизнес-вопроса в виде SQL-запроса;
- работа с несколькими связанными таблицами;
- расчёт продуктовых, маркетинговых и операционных метрик;
- использование CTE, оконных функций и условной логики;
- оформление решения в Jupyter Notebook.

## Стек

- **SQL**: SQLite
- **Python**: pandas, sqlite3
- **Notebook**: Jupyter
- **Данные**: CSV + SQLite database

## Структура репозитория

```text
sql_internship_analytics_portfolio/
├── data/
│   ├── marketplace.sqlite          # готовая SQLite-база для выполнения запросов
│   └── csv/                        # исходные CSV-таблицы
├── docs/
│   ├── database_schema.md          # описание таблиц и ключевых полей
│   └── github_profile_text.md      # короткое описание проекта для профиля GitHub
├── notebooks/                      # SQL-задачи и решения в Jupyter Notebook
├── requirements.txt                # зависимости для запуска ноутбуков
└── README.md
```

## Данные

В проекте используется модель данных небольшого маркетплейса.

| Таблица | Описание |
|---|---|
| `customers` | клиенты, город, дата регистрации, канал привлечения |
| `products` | товары, категории, цена, себестоимость |
| `orders` | заказы, дата заказа, статус, промокод, способ оплаты |
| `order_items` | товары внутри заказа, количество, цена, скидка |
| `payments` | платежи, сумма, статус оплаты |
| `shipments` | доставки, перевозчик, срок доставки, SLA |
| `sessions` | пользовательские сессии и шаги воронки |
| `marketing_spend` | расходы на маркетинг по каналам и месяцам |
| `support_tickets` | обращения клиентов в поддержку |

Подробное описание схемы лежит в [`docs/database_schema.md`](docs/database_schema.md).

## SQL-задачи

| № | Notebook | Что анализируется | Основные SQL-приёмы |
|---:|---|---|---|
| 1 | [`01_monthly_revenue_and_aov.ipynb`](notebooks/01_monthly_revenue_and_aov.ipynb) | выручка, прибыль, средний чек по месяцам | `JOIN`, `GROUP BY`, CTE |
| 2 | [`02_category_margin_analysis.ipynb`](notebooks/02_category_margin_analysis.ipynb) | маржинальность категорий | агрегации, расчёт долей |
| 3 | [`03_top_products_by_category.ipynb`](notebooks/03_top_products_by_category.ipynb) | топ товаров внутри категорий | `RANK()`, оконные функции |
| 4 | [`04_customer_repeat_purchases_ltv.ipynb`](notebooks/04_customer_repeat_purchases_ltv.ipynb) | повторные покупки и LTV | CTE, агрегация по клиентам |
| 5 | [`05_rfm_segmentation.ipynb`](notebooks/05_rfm_segmentation.ipynb) | RFM-сегментация клиентов | `CASE`, даты, скоринг |
| 6 | [`06_signup_cohort_retention.ipynb`](notebooks/06_signup_cohort_retention.ipynb) | когортное удержание | работа с датами, когорты |
| 7 | [`07_funnel_conversion_by_channel.ipynb`](notebooks/07_funnel_conversion_by_channel.ipynb) | конверсия воронки по каналам | условные агрегации |
| 8 | [`08_promo_code_effectiveness.ipynb`](notebooks/08_promo_code_effectiveness.ipynb) | эффективность промокодов | сравнение групп, метрики заказов |
| 9 | [`09_marketing_roi_by_channel.ipynb`](notebooks/09_marketing_roi_by_channel.ipynb) | ROI маркетинговых каналов | объединение выручки и расходов |
| 10 | [`10_delivery_sla_analysis.ipynb`](notebooks/10_delivery_sla_analysis.ipynb) | выполнение SLA доставки | `HAVING`, расчёт просрочек |
| 11 | [`11_refunds_and_support_tickets.ipynb`](notebooks/11_refunds_and_support_tickets.ipynb) | возвраты и обращения в поддержку | `LEFT JOIN`, `COUNT DISTINCT` |
| 12 | [`12_abc_analysis_products.ipynb`](notebooks/12_abc_analysis_products.ipynb) | ABC-анализ товаров | `SUM() OVER`, накопительная доля |

## Как запустить проект

Склонируйте репозиторий и установите зависимости:

```bash
git clone <repository-url>
cd sql_internship_analytics_portfolio

python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Запустите Jupyter Notebook:

```bash
jupyter notebook
```

Откройте любой файл из папки `notebooks/`. Все ноутбуки используют готовую SQLite-базу:

```text
data/marketplace.sqlite
```

## Пример подключения к базе

```python
import sqlite3
from pathlib import Path

import pandas as pd

DB_PATH = Path('../data/marketplace.sqlite')
conn = sqlite3.connect(DB_PATH)

query = """
SELECT COUNT(*) AS orders_cnt
FROM orders;
"""

pd.read_sql_query(query, conn)
```

## Какие навыки демонстрирует проект

- написание SQL-запросов для аналитических задач;
- понимание продуктовых метрик: выручка, средний чек, LTV, retention;
- понимание маркетинговых метрик: CAC, ROI, эффективность каналов;
- анализ клиентского поведения и сегментация;
- работа с операционными метриками: доставка, SLA, возвраты, поддержка;
- аккуратное оформление аналитики в ноутбуках.

## Возможное описание для резюме

> Подготовил SQL-проект на синтетических данных маркетплейса: создал набор аналитических ноутбуков для расчёта выручки, маржинальности, LTV, RFM, retention, маркетингового ROI, SLA доставки и ABC-анализа товаров. Использовал SQLite, CTE, оконные функции, условные агрегации и pandas для отображения результатов.

## Что можно добавить дальше

- дашборд в Power BI, Tableau или DataLens;
- визуализации ключевых метрик в Python;
- отдельный файл с ER-диаграммой;
- SQL-тесты для проверки качества данных;
- сравнение результатов по месяцам и подготовку краткого аналитического отчёта.
