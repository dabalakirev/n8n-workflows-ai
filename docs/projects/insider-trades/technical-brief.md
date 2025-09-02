# Level 2: Технический бриф - Insider Trades

## 🎯 Техническая архитектура системы

**Insider Trades** реализуется как автоматизированная система на базе n8n с интеграцией 5 внешних сервисов и MongoDB для персистентного хранения данных. Система выполняет полный цикл обработки каждые 60 минут через единый main workflow.

---

## 1. End-to-End технический сценарий

### 1.1 Плановый запуск (каждые 60 минут)
- **Триггер:** Cron-based расписание n8n
- **Точка входа:** Единый main workflow
- **Сессия:** Все операции в рамках одного запуска считаются единой сессией
- **Логирование:** Базовое (старт/стоп, счетчики объектов на каждом этапе)

### 1.2 Сбор инсайдерских сделок (FMP API)

**Endpoint:** Latest Insider Trading  
```
GET https://financialmodelingprep.com/stable/insider-trading/latest
?page=0&limit=500&apikey={{FMP_API_KEY}}
```

**Фильтрация (строгая):**
- `transactionType == "P-Purchase"` (только покупки)  
- `securityName ∈ {"Common Stock", "Class A Common Stock"}` (только указанные типы ценных бумаг)

**Early Exit:** Если после фильтрации массив пустой → завершение цикла

### 1.3 Обновление карточек компаний (MongoDB)

**Алгоритм идемпотентной обработки:**

Для каждой отфильтрованной сделки:

1. **Проверка дедупликации:**
   - Ключ уникальности: `symbol + transaction_date + insider_name + shares + price + sec_url`
   - Если найдена → пропустить сделку

2. **Поиск существующей карточки:**
   - Query: 30 последних карточек по `created_at DESC`
   - Filter: `symbol == текущий_symbol`

3. **Создание новой карточки** (если карточки нет):
   - Статус: `"New"`
   - Запрос Company Profile от FMP
   - Генерация `chart_url`
   - Добавление сделки в массив `trades[]`

4. **Обновление существующей карточки:**
   - Если в текущей сессии → статус остается `"New"`
   - Если в следующих запусках → статус меняется на `"Renew"`
   - Добавление сделки в `trades[]`

### 1.4 Подготовка к AI анализу
- **Выборка:** Карточки со статусом `"New"` только
- **Формирование списка:** `symbol[]` для AI Agent запросов

### 1.5 AI Agent анализ (DeepSeek + Web Search)

**AI Agent архитектура:**
```
AI Agent (DeepSeek Chat Model) + SerpApi (Google Search) Tool
```

**Для каждой компании из списка "New":**

**Input данные:**
- Название компании из `company_name`
- Фиксированный список вопросов (редактируемый в одном месте)

**Стандартные вопросы:**
1. "Каково текущее состояние финансового здоровья компании?"
2. "Каковы катализаторы роста этой компании?"
3. "Каковы основные риски для инвестирования в эту компанию на данный момент?"
4. "Что конкретно производит компания и какова динамика продаж продукции за последние два года по кварталам?"

**AI Agent автономное поведение:**
- **Автоматически определяет** необходимость web search для каждого вопроса
- **Автоматически формирует** Google поисковые запросы через SerpApi
- **Автоматически выбирает** релевантные источники из результатов поиска
- **Использует актуальную информацию** из интернета для формирования ответов
- **Принимает решения** о том, какие сайты и данные использовать

**Output спецификация:**
- Формат: JSON
- Структура: `[{q: "вопрос", a: "ответ"}]`
- Ограничения: каждый ответ до 1000 символов
- Язык: русский
- Источник данных: актуальная информация из Google search

**Сохранение результатов:**
- Коллекция: `surveys`
- Учет токенов: `usage.input_tokens`, `usage.output_tokens`
- Стоимость: `cost_usd = input_tokens * 0.56e-6 + output_tokens * 1.68e-6`

### 1.6 Создание статей (Telegraph API)

**Для каждой записи в surveys:**

**Параметры статьи:**
- **Заголовок:** `"Company Name (SYMBOL)"`
- **Контент:** Параграфы по количеству вопросов
- **Язык:** русский
- **Author fields:** не критичны

**Обратная связь:**
- Сохранение `telegraph_url` в соответствующую запись `surveys`

### 1.7 Публикация в Telegram

**Канал:** ID `3049635154`  
**Формат:** Отдельное сообщение для каждой карточки со статусом "New"

**Структура сообщения:**
- **Фото:** `chart_url` (если недоступен → сообщение без фото)
- **Текст:** 
  - Информация о компании (`company_name`, `industry`, форматированный `company_marketcap`)
  - Список сделок инсайдеров из `trades[]` массива
- **Кнопки:** Inline-кнопка "ПОДРОБНЕЕ" → `telegraph_url`
- **Parse Mode:** HTML

**Fallback обработка:**
- Если отправка неуспешна → карточка остается `"New"/"Renew"` для повторной отправки в следующем цикле

### 1.8 Завершение цикла

**После успешной публикации:**
- Установка `posted_at = текущая_timestamp`
- Перевод статуса карточек в `"Old"`
- Завершение workflow до следующего запуска

---

## 2. Источники данных и API интеграции

### 2.1 FMP API (Financial Modeling Prep)

**Используемые endpoints:**

**Latest Insider Trading:**
```http
GET /stable/insider-trading/latest?page=0&limit=500&apikey={{FMP_API_KEY}}
```

**Response format:**
```json
[
  {
    "symbol": "APA",
    "filingDate": "2025-02-04",
    "transactionDate": "2025-02-01",
    "reportingCik": "0001380034",
    "companyCik": "0001841666",
    "transactionType": "P-Purchase",
    "securitiesOwned": 104398,
    "reportingName": "Hoyt Rebecca A",
    "typeOfOwner": "officer: Sr. VP, Chief Acct Officer",
    "acquisitionOrDisposition": "A",
    "directOrIndirect": "D",
    "formType": "4",
    "securitiesTransacted": 3450,
    "price": 125.67,
    "securityName": "Common Stock",
    "url": "https://www.sec.gov/Archives/.../index.htm"
  }
]
```

**Company Profile:**
```http
GET /stable/profile?symbol={{SYMBOL}}&apikey={{FMP_API_KEY}}
```

**Response format:**
```json
[
  {
    "symbol": "AAPL",
    "price": 232.8,
    "marketCap": 3500823120000,
    "companyName": "Apple Inc.",
    "industry": "Consumer Electronics",
    "description": "Apple Inc. designs, manufactures, and markets smartphones...",
    "exchange": "NASDAQ",
    "website": "https://www.apple.com",
    "image": "https://images.financialmodelingprep.com/symbol/AAPL.png",
    "ipoDate": "1980-12-12",
    "isActivelyTrading": true
  }
]
```

### 2.2 AI Agent + DeepSeek + SerpApi Integration

**Архитектура компонентов:**

**AI Agent узел** (`@n8n/n8n-nodes-langchain.agent`):
- Автономная система принятия решений
- Управляет использованием внешних tools
- Определяет необходимость web search

**DeepSeek Chat Model** (`@n8n/n8n-nodes-langchain.lmChatDeepSeek`):
- Языковая модель для AI Agent
- Генерация ответов на русском языке
- API совместимость с OpenAI

**SerpApi Tool** (`@n8n/n8n-nodes-langchain.toolSerpApi`):
- Google Search интеграция
- Автоматический поиск актуальной информации
- Результаты для AI Agent analysis

**Конфигурация SerpApi:**
- **Country:** "us" (по умолчанию)
- **Device:** "desktop" 
- **Language:** "en" (Google search), результаты переводятся в ответах
- **Google Domain:** "google.com"

**Автономное поведение AI Agent:**
1. Получает название компании и вопросы
2. Анализирует каждый вопрос на необходимость актуальных данных
3. Формирует поисковые запросы в Google через SerpApi
4. Анализирует результаты поиска и выбирает релевантные
5. Формирует ответы на русском языке с использованием найденной информации

### 2.3 Telegraph API

**Создание статьи:**
```http
POST https://api.telegra.ph/createPage
```

**Параметры:**
- `access_token`: из n8n Credentials
- `title`: "Company Name (SYMBOL)"
- `content`: массив параграфов из AI Agent ответов
- `return_content`: false

### 2.4 Telegram Bot API

**Отправка фото с подписью:**
```http
POST https://api.telegram.org/bot{{BOT_TOKEN}}/sendPhoto
```

**Параметры:**
- `chat_id`: `3049635154`
- `photo`: `chart_url`
- `caption`: HTML-форматированный текст
- `parse_mode`: "HTML"
- `reply_markup`: inline keyboard с кнопкой "ПОДРОБНЕЕ"

### 2.5 Finviz (через proxy)

**Chart URL generation:**
```
https://images.weserv.nl/?url=finviz.com/chart.ashx%3Ft%3D{{SYMBOL}}
```

**Fallback:** Если URL недоступен → публикация без фото

---

## 3. Структуры данных и маппинг

### 3.1 MongoDB коллекция: deals

**Полная схема:**
```json
{
  "trade_status": "New | Renew | Old",
  "symbol": "AAPL",
  "company_name": "Apple Inc.",
  "company_marketcap": 3500000000000,
  "industry": "Consumer Electronics",
  "chart_url": "https://images.weserv.nl/?url=finviz.com/chart.ashx%3Ft%3DAAPL",
  "company_about": "Designs and sells smartphones, computers and services.",
  "created_at": "2025-09-01T09:00:00Z",
  "updated_at": "2025-09-01T09:00:00Z",
  "posted_at": null,
  "trades": [
    {
      "insider_name": "Tim Cook",
      "role": "CEO",
      "filing_date": "2025-07-15",
      "transaction_date": "2025-07-10",
      "price": 225.3,
      "shares": 6654,
      "value": 1500000,
      "code": "P",
      "ownership_type": "Direct",
      "sec_url": "https://www.sec.gov/..."
    }
  ]
}
```

**Индексы (минимальные):**
- `symbol` (single field)
- `created_at` (для выборки 30 последних)
- Композитный индекс для дедупликации (по мере необходимости)

### 3.2 Маппинг данных FMP → deals

**Latest Insider Trading → deals.trades[]:**
- `reportingName` → `insider_name`
- `typeOfOwner` → `role`
- `filingDate` → `filing_date`
- `transactionDate` → `transaction_date`
- `price` → `price`
- `securitiesTransacted` → `shares`
- `value = round(price * shares, 2)` (вычисляемое поле)
- `transactionType` ("P-Purchase") → `code = "P"`
- `directOrIndirect` ("D"/"I") → `ownership_type` ("Direct"/"Indirect")
- `url` → `sec_url`

**Company Profile → deals (корневой уровень):**
- `companyName` → `company_name`
- `marketCap` → `company_marketcap`
- `industry` → `industry`
- `description` → `company_about`
- `symbol` → `symbol` (валидация соответствия)

**Служебные поля:**
- `chart_url` = `https://images.weserv.nl/?url=finviz.com/chart.ashx%3Ft%3D{SYMBOL}`
- `trade_status` ∈ {New, Renew, Old}
- `created_at`, `updated_at`, `posted_at` (UTC, ISO-8601)

### 3.3 MongoDB коллекция: surveys

**Полная схема:**
```json
{
  "symbol": "NVDA",
  "polled_at": "2025-09-01T09:00:00Z",
  "qa": [
    { "q": "Каково текущее состояние финансового здоровья компании?", "a": "..." },
    { "q": "Каковы катализаторы роста этой компании?", "a": "..." },
    { "q": "Каковы основные риски для инвестирования в эту компанию на данный момент?", "a": "..." },
    { "q": "Что конкретно производит компания и какова динамика продаж продукции за последние два года по кварталам?", "a": "..." }
  ],
  "tokens_used": { "input": 1820, "output": 350, "total": 2170 },
  "cost_usd": 0.09,
  "telegraph_url": "https://telegra.ph/..."
}
```

---

## 4. Алгоритмы и бизнес-логика

### 4.1 Ключ уникальности сделки

**Композитный ключ:**
```
symbol + transaction_date + insider_name + shares + price + sec_url
```

**Применение:** Проверка перед добавлением каждой сделки в существующие `trades[]` массивы

### 4.2 Статусная модель карточек

**Состояния:**
- **New:** Карточка создана в текущей сессии
- **Renew:** Карточка обновлена в последующих сессиях  
- **Old:** Карточка опубликована в Telegram

**Переходы:**
```
[Создание] → New
New + [Добавление сделки в той же сессии] → New
New + [Добавление сделки в следующей сессии] → Renew
Renew + [Добавление сделки] → Renew
New/Renew + [Успешная публикация] → Old
```

### 4.3 Окно поиска карточек

**Логика:** При поиске существующей карточки по symbol, проверяется только 30 последних карточек по `created_at DESC`

**Обоснование:** Оптимизация производительности при росте объема данных

### 4.4 Формулы и вычисления

**Value сделки:**
```
value = round(price * shares, 2)
```

**Стоимость DeepSeek:**
```
cost_usd = input_tokens * 0.56e-6 + output_tokens * 1.68e-6
```
(округление до $0.01)

**MarketCap форматирование:**
- В базе: числовое значение
- В отображении: человекочитаемый формат (3.5T, 950B, 12.3B)

---

## 5. Обработка ошибок и edge cases

### 5.1 API Failures

**Стратегия:** Простые retry с экспоненциальной задержкой
- **Попытки:** 1-2 повтора
- **Задержка:** 2s → 5s
- **При неуспехе:** Пропуск объекта + логирование

**Применяется к:**
- FMP API calls
- AI Agent processing
- SerpApi search calls
- Telegraph API calls
- Telegram API calls

### 5.2 Data Inconsistencies

**Chart URL недоступен:** Публикация без фото
**Company Profile отсутствует:** Пропуск создания карточки
**AI Agent не вернул JSON:** Пропуск создания survey
**Telegraph создание неуспешно:** Survey остается без telegraph_url
**SerpApi недоступен:** AI Agent использует базовые знания модели

### 5.3 Telegram Publishing Failures

**Сценарий:** Telegraph статья создана, но Telegram сообщение не отправлено

**Поведение:**
- Карточка остается в статусе `"New"`/`"Renew"`
- `posted_at` остается `null`
- В следующем цикле карточка будет повторно обработана
- Telegraph статья может быть создана повторно (дубликат)

**Обоснование:** Простое решение без сложной recovery логики

### 5.4 Empty Results Handling

**Нет отфильтрованных сделок:** Завершение цикла
**Нет карточек со статусом "New":** Пропуск AI анализа и публикации  
**AI Agent не смог найти информацию:** Пропуск создания survey

---

## 6. Конфигурационные параметры

### 6.1 FMP API
- `FMP_API_KEY` - API ключ (из Credentials)
- `FMP_LATEST_LIMIT=500` - размер выборки сделок
- `FMP_LATEST_PAGE=0` - стартовая страница (фиксированная)

### 6.2 AI Agent + DeepSeek + SerpApi
- `DEEPSEEK_API_KEY` - API ключ DeepSeek (из Credentials)
- `SERPAPI_KEY` - API ключ SerpApi (из Credentials)
- `DEEPSEEK_MAX_ANSWER_LEN=1000` - лимит символов в ответе
- `SERPAPI_COUNTRY=us` - страна поиска Google
- `SERPAPI_DEVICE=desktop` - устройство для поиска
- `SERPAPI_LANGUAGE=en` - язык Google поиска

### 6.3 Telegram
- `TELEGRAM_BOT_TOKEN` - токен бота (из Credentials)
- `TELEGRAM_CHANNEL_ID=3049635154` - ID целевого канала
- `MESSAGE_PARSE_MODE=HTML` - режим парсинга

### 6.4 System
- `LAST_CARDS_WINDOW=30` - окно поиска карточек
- `MAIN_SCHEDULE="0 */60 * * * *"` - расписание cron (каждые 60 минут)

---

## 7. Logging и мониторинг

### 7.1 Базовое логирование

**Старт цикла:**
- Timestamp запуска
- Версия workflow

**Промежуточные этапы:**
- Количество полученных сделок от FMP
- Количество сделок после фильтрации
- Количество новых карточек создано
- Количество карточек обновлено  
- Количество компаний отправлено на AI Agent анализ
- Количество статей Telegraph создано
- Количество сообщений Telegram отправлено

**Завершение цикла:**
- Общее время выполнения
- Итоговые счетчики
- Статус завершения (success/partial/failure)

### 7.2 Error logging

**НЕ логировать:**
- API ключи и токены
- Полные тела запросов с секретами

**Логировать:**
- HTTP статус коды ошибок
- Общие описания ошибок API
- Символы компаний при неудачной обработке
- AI Agent decision reasoning (при включенном debug режиме)

---

## 8. Производительность и масштабирование

### 8.1 Текущие ограничения

**Batch processing:** Последовательная обработка AI Agent (без параллелизма)
**Rate limits:** Не учитываются в текущей версии (SerpApi, DeepSeek)
**Memory usage:** Загрузка всех 500 сделок в память

### 8.2 Архитектурная готовность

**Возможности добавления:**
- Батчинг компаний для AI Agent обработки
- Паузы между SerpApi вызовами
- Parallel processing нескольких AI Agent instances
- Разделение на sub-workflows для параллелизма

**Индексы MongoDB:** Готовность к росту объема через индексирование

---

## 9. Безопасность

### 9.1 Credentials management
**Все sensitive данные:** Исключительно через n8n Credentials
**Типы credentials:**
- FMP API Key
- DeepSeek API Key  
- SerpApi API Key
- Telegraph Access Token
- Telegram Bot Token
- MongoDB Connection String

### 9.2 Data protection
**Логирование:** Исключение секретов из логов
**API calls:** Передача credentials через защищенные заголовки
**MongoDB:** Подключение через защищенную connection string
**AI Agent:** Обработка sensitive информации о компаниях согласно privacy guidelines

---

*Документ создан согласно New Project Creation Procedure v1.2*  
*AI Agent + SerpApi решение для DeepSeek Web Search Integration*