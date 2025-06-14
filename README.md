# Прогнозирование покупок клиентов интернет-магазина

Модель машинного обучения для предсказания вероятности совершения покупки клиентами интернет-магазина в течение следующих 90 дней.  
Проект разработан для оптимизации маркетинговых кампаний и повышения эффективности рассылок.

## 🎯 Цель проекта

- Предсказывать вероятность совершения покупки в течение 90 дней (бинарная классификация)
- Выявить ключевые факторы, влияющие на покупательскую активность
- Предоставить инструмент для оптимизации маркетинговых стратегий

## 💡 Использованные технологии

- Python 3.x
- pandas, numpy, matplotlib, seaborn
- scikit-learn, lightgbm, phik
- StandardScaler, OneHotEncoder, OrdinalEncoder, SimpleImputer
- Jupyter Notebook

## 🧪 Как запустить проект

```bash
git clone https://github.com/kagor4/Purchase-Prediction-for-Online-Store.git
cd Purchase-Prediction-for-Online-Store
pip install -r requirements.txt
```

Затем откройте и запустите файл `project_marketing_(2).py` или ноутбук с аналогичным кодом в Jupyter. Убедитесь, что датасеты `apparel-purchases.csv`, `apparel-messages.csv` и `apparel-target_binary.csv` доступны.

## 📊 Описание данных

Датасет содержит информацию о покупках и маркетинговой активности:
- **apparel-purchases** (история покупок):
  - `client_id` — идентификатор пользователя
  - `quantity` — количество товаров в заказе
  - `price` — цена товара
  - `category_ids` — категории товаров
  - `purchase_date` — дата покупки
  - `bulk_campaign_id_extracted` — идентификатор рекламной кампании
- **apparel-messages** (история рассылок):
  - `bulk_campaign_id` — идентификатор кампании
  - `client_id` — идентификатор пользователя
  - `event` — тип действия (send, open, click, purchase, etc.)
  - `channel` — канал рассылки (email, mobile_push)
  - `message_date` — дата рассылки
  - `created_at` — время создания сообщения
- **apparel-target_binary**:
  - `client_id` — идентификатор пользователя
  - `target` — целевой признак (0 — не совершил покупку, 1 — совершил)
- **Производные признаки**:
  - `last_purchase_date`, `first_purchase_date` — дни с момента последней и первой покупки
  - `category_event` — категоризация событий (good, bad, other)
  - Агрегированные признаки: суммы событий (`event_click`, `event_open`, etc.), каналов (`channel_email`, `channel_mobile_push`), и др.

## 🔍 Краткие результаты

- Лучшая модель: **LightGBM** (оптимизирована через RandomizedSearchCV)
- Метрики:
  - ROC AUC (кросс-валидация): 0.7368
  - ROC AUC (тестовая выборка): 0.7527
- Ключевые факторы (по корреляции Phi_k и важности признаков):
  - `last_purchase_date` — наиболее важный признак
  - `event_click`, `event_open`, `event_purchase`, `channel_mobile_push`, `category_event_good`, `quantity`
  - Меньшее влияние: `price`, `event_hard_bounce`
- Основные выводы:
  - Недавняя покупательская активность (`last_purchase_date`) и взаимодействие с рассылками (`event_click`, `event_open`) сильно влияют на вероятность покупки
  - Пуш-уведомления (`channel_mobile_push`) более эффективны, чем email
  - Дисбаланс классов (98% — не совершили покупку) требует учета при обучении
- Рекомендации:
  - Увеличить объем данных о покупках для повышения качества модели
  - Исследовать дополнительные признаки, такие как поведение на сайте или демографические данные
  - Оптимизировать стратегию рассылок, фокусируясь на пуш-уведомлениях

## 📁 Структура проекта

```
📦 Purchase-Prediction/
├── project_marketing.ipynb   # анализ и обучение модели
├── requirements.txt          # зависимости
└── README.md                 # описание проекта
```

## ✅ TODO

- Провести дополнительный анализ дисбаланса классов и применить методы балансировки (SMOTE, взвешивание классов)
- Исследовать ансамблевые методы (XGBoost, CatBoost) для улучшения метрик
- Добавить визуализацию предсказаний для интерпретации результатов
- Интегрировать данные о поведении клиентов на сайте или в приложении

## © Автор

Автор: [kagor4](https://github.com/kagor4)  
Свяжитесь со мной: [@egor_kagor](https://t.me/egor_kagor)
