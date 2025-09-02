# Архитектурные тезисы - Insider Trades

## 🏗️ Архитектурные контуры системы Insider Trades

### 1. Фундаментальное решение: Единый монолитный workflow

**Решение:** Вся система Insider Trades реализуется как **единый main workflow** без разделения на sub-workflows.

**Обоснование:**
- **Последовательная обработка:** 7-этапный цикл требует строгой последовательности без параллелизма
- **Состояние сессии:** Все операции в рамках одного 60-минутного цикла должны работать с единой сессией данных
- **Простота отладки:** Один workflow = одно место для логирования, мониторинга и troubleshooting
- **Статусная модель:** Переходы карточек (New → Renew → Old) требуют единого контроля состояния
- **Идемпотентность:** Логика дедупликации и поиска карточек проще в рамках единого execution context

**Key Principle соблюдение:** Nothing Forgotten - весь цикл в одном месте, Nothing Redundant - никакой дублированной логики между workflows.

### 2. Архитектурное разделение на логические блоки

Единый workflow структурируется в **5 основных архитектурных блоков:**

#### **Блок 1: Data Collection & Filtering**
- **Компоненты:** Cron Trigger → FMP API calls → Data filtering
- **Функции:** Получение сделок, строгая фильтрация, early exit при пустых результатах
- **Узлы:** Cron, HTTP Request (FMP), Code (фильтрация), If (early exit)

#### **Блок 2: Database Operations & Card Management** 
- **Компоненты:** MongoDB queries → Card lookup → Deduplication → Card creation/update
- **Функции:** Идемпотентная обработка, статусная модель, 30-карточное окно
- **Узлы:** MongoDB (queries), Code (деdup логика), Split in Batches, Set

#### **Блок 3: AI Analysis & Intelligence**
- **Компоненты:** AI Agent → DeepSeek Chat Model → SerpApi Tool → Results processing
- **Функции:** Автономный web search, анализ компаний, JSON response обработка
- **Узлы:** AI Agent, DeepSeek Chat Model, SerpApi Tool, Code (JSON parsing)

#### **Блок 4: Content Generation & Publishing**
- **Компоненты:** Telegraph article creation → Telegram message formatting → Publishing
- **Функции:** Создание статей, форматирование сообщений, Inline buttons
- **Узлы:** HTTP Request (Telegraph), HTTP Request (Telegram), Code (formatting)

#### **Блок 5: State Management & Completion**
- **Компоненты:** Status updates → Final logging → Cycle completion
- **Функции:** Перевод в статус "Old", timestamp установка, цикл завершения
- **Узлы:** MongoDB (updates), Code (logging), NoOp (completion)

### 3. Принципы узловой архитектуры

#### **Минимализм узлов:**
- **HTTP Request узлы:** Только для API calls (FMP, Telegraph, Telegram)
- **MongoDB узлы:** Только для database operations
- **Code узлы:** Для всей бизнес-логики (фильтрация, деdup, форматирование)
- **AI Agent комплекс:** Один AI Agent + один Chat Model + один Tool

#### **Обработка данных:**
- **Split in Batches:** Только для обработки массивов (сделки, карточки, компании)
- **Set узлы:** Для data transformation между блоками
- **If узлы:** Только для критических условий (early exit, status checks)

#### **Error Handling стратегия:**
- **Встроенная обработка:** В Code узлах через try/catch
- **Continue On Fail:** Для HTTP Request узлов с retry логикой
- **Fallback узлы:** Только для критических API failures

### 4. Оптимальность решения

**Производительность:**
- Последовательная обработка без overhead sub-workflow calls
- Минимум узлов для каждой операции
- Batch processing только там где необходимо

**Надежность:**
- Единое состояние исключает race conditions
- Простая retry логика в рамках одного workflow
- Все credentials в одном месте

**Масштабируемость:**
- Готовность к добавлению новых блоков (например, notification расширения)
- Модульная структура позволяет оптимизировать отдельные блоки
- AI Agent архитектура готова к добавлению новых tools

**Обслуживаемость:**
- Один workflow = одна точка мониторинга
- Линейная логика легка для понимания и дебага
- Все конфигурации в одном месте

### 5. Обоснование против альтернатив

**Почему НЕ разделение на sub-workflows:**
- **Сессионность:** Нарушается единство 60-минутного цикла
- **Сложность:** Передача состояния между workflows через Execute Workflow
- **Debugging:** Сложнее отслеживать end-to-end execution
- **Избыточность:** Дублирование error handling и logging логики

**Почему НЕ microservice архитектура:**
- **Latency:** Дополнительные HTTP calls между services
- **Consistency:** Сложнее поддерживать ACID semantics
- **Deployment:** Усложнение без реальных benefits для данного scale

**Почему монолитный подход оптимален:**
- **Current Scale:** 500 deals/hour максимум, простые операции
- **Data Flow:** Строго последовательный pipeline
- **Business Logic:** Тесно связанные операции с shared state
- **Maintenance:** Один deployment unit, простая операционная модель

---

**Заключение:** Единый монолитный workflow с 5 логическими блоками представляет оптимальное архитектурное решение для системы Insider Trades, соответствующее принципам "Nothing Forgotten, Nothing Redundant" и лучшим практикам n8n для последовательных data processing pipelines.

---

*Создано как часть Level 3 архитектурного планирования*  
*Date: September 2, 2025*