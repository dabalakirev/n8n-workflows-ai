# Insider Trades - Узлы Workflow

**⚠️ СТАТУС ДОКУМЕНТА:** CONCEPT/DRAFT - Концептуальные заготовки для Level 3 архитектуры  
**📋 НАЗНАЧЕНИЕ:** Техническая спецификация узлов n8n согласно Architecture Theses  
**🔧 ВЕРСИЯ:** Расширенная - Блоки 1-3 из 5 (Data Collection + Database Operations + AI Analysis)

---

## 🗃️ Блок 1: Data Collection & Filtering (Узлы 1-4)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение инсайдерских сделок от FMP API, строгая фильтрация согласно Level 2 требованиям, early exit при пустых результатах

### Узел 1: Cron Trigger
**Тип:** `nodes-base.cron` (v1)  
**📍 НАЗНАЧЕНИЕ:** Запуск workflow каждые 60 минут согласно техническому брифу  
**🔧 СТАТУС КОДА:** TEMPLATE - готовая конфигурация расписания

```json
{
  "triggerTimes": {
    "item": [
      {
        "mode": "everyX",
        "value": 60,
        "unit": "minutes"
      }
    ]
  }
}
```
**💡 ПОЯСНЕНИЕ:** Использует `everyX` режим для точного 60-минутного интервала. Альтернативный cron expression `"0 */60 * * * *"` даст аналогичный результат.

---

### Узел 2: HTTP Request (FMP API)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Получение последних 500 инсайдерских сделок от FMP Latest Insider Trading API  
**🔧 СТАТУС КОДА:** CONCEPT - основная структура с credential integration

```json
{
  "method": "GET",
  "url": "https://financialmodelingprep.com/stable/insider-trading/latest",
  "authentication": "genericCredentialType",
  "genericAuthType": "httpQueryAuth",
  "sendQuery": true,
  "specifyQuery": "keypair",
  "queryParameters": {
    "parameters": [
      { "name": "page", "value": "0" },
      { "name": "limit", "value": "500" }
    ]
  },
  "options": {
    "timeout": 30000,
    "response": {
      "response": {
        "responseFormat": "json",
        "neverError": false,
        "fullResponse": false
      }
    }
  },
  "credentials": {
    "httpQueryAuth": {
      "id": "k887gSxTZZEgRYIa",
      "name": "FMP API"
    }
  }
}
```
**💡 ПОЯСНЕНИЕ:** 
- `httpQueryAuth` - передает API key через query parameter (стандарт FMP)
- `limit: 500` - максимальная выборка согласно Level 2 ограничениям
- `timeout: 30000` - 30 секунд для внешнего API call
- `neverError: false` - позволяет workflow остановиться при API failures

---

### Узел 3: Code (Data Filtering)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Строгая фильтрация сделок по типу операции и типу ценных бумаг  
**🔧 СТАТУС КОДА:** CONCEPT - основная логика фильтрации с валидацией данных

**Режим:** `runOnceForAllItems` - обрабатывает весь массив сделок за один раз

```javascript
// Строгая фильтрация согласно Level 2 техническим требованиям
const filteredDeals = $input.all().filter(deal => {
  // Только покупки (P-Purchase)
  const isPurchase = deal.json.transactionType === "P-Purchase";
  
  // Только разрешенные типы ценных бумаг
  const allowedSecurities = ["Common Stock", "Class A Common Stock"];
  const isValidSecurity = allowedSecurities.includes(deal.json.securityName);
  
  // Базовая валидация данных
  const hasRequiredFields = deal.json.symbol && 
                           deal.json.reportingName && 
                           deal.json.securitiesTransacted && 
                           deal.json.price;
  
  return isPurchase && isValidSecurity && hasRequiredFields;
});

console.log(`Original: ${$input.all().length}, Filtered: ${filteredDeals.length}`);
return filteredDeals;
```
**💡 ПОЯСНЕНИЕ:**
- **Фильтр 1:** `transactionType === "P-Purchase"` - только покупки инсайдеров
- **Фильтр 2:** `securityName` проверка против whitelist - исключает опционы/варранты
- **Фильтр 3:** Валидация required fields - предотвращает обработку неполных данных
- **Логирование:** Счетчики до/после фильтрации для мониторинга

---

### Узел 4: If (Early Exit)
**Тип:** `nodes-base.if` (v2.2)  
**📍 НАЗНАЧЕНИЕ:** Early exit optimization - завершение workflow при отсутствии данных после фильтрации  
**🔧 СТАТУС КОДА:** TEMPLATE - готовая conditional логика

```json
{
  "conditions": {
    "options": {
      "caseSensitive": true,
      "leftValue": "={{$json.length}}",
      "operation": {
        "type": "number",
        "operation": "gt",
        "rightValue": 0
      }
    }
  },
  "looseTypeValidation": false
}
```
**💡 ПОЯСНЕНИЕ:**
- **Condition:** `array.length > 0` - проверяет наличие отфильтрованных сделок
- **TRUE path** → Блок 2 (продолжение обработки)
- **FALSE path** → Workflow end (экономия ресурсов при пустых результатах)
- `looseTypeValidation: false` - строгая проверка типов

---

## 🗄️ Блок 2: Database Operations & Card Management (Узлы 5-12)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Идемпотентная обработка сделок, управление карточками компаний, дедупликация, статусная модель (New/Renew/Old)

### Узел 5: Split In Batches
**Тип:** `nodes-base.splitInBatches` (v3)  
**📍 НАЗНАЧЕНИЕ:** Поочередная обработка каждой сделки для избежания race conditions в MongoDB  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная конфигурация для item-by-item processing

```json
{
  "batchSize": 1,
  "options": {
    "reset": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- `batchSize: 1` - обрабатываем по одной сделке (критично для дедупликации)
- `reset: false` - сохраняем состояние между итерациями
- **Loop output** → Узел 6 (обработка сделки)
- **Done output** → Блок 3 (переход к следующему блоку)

---

### Узел 6: Code (Deal Processing Logic)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Подготовка данных сделки, создание deduplication key, формирование MongoDB query  
**🔧 СТАТУС КОДА:** CONCEPT - базовая логика обработки и маппинга данных

**Режим:** `runOnceForEachItem` - обрабатывает текущую сделку из Split In Batches

```javascript
const currentDeal = $input.item(0).json;

// Deduplication key
const dedupKey = [
  currentDeal.symbol,
  currentDeal.transactionDate,
  currentDeal.reportingName,
  currentDeal.securitiesTransacted,
  currentDeal.price,
  currentDeal.url
].join('|');

// Find existing card query (30-card window)
const cardQuery = {
  find: {
    query: JSON.stringify({ symbol: currentDeal.symbol }),
    options: {
      sort: JSON.stringify({ created_at: -1 }),
      limit: 30
    }
  }
};

// Map deal data for MongoDB
const mappedDeal = {
  insider_name: currentDeal.reportingName,
  role: currentDeal.typeOfOwner,
  filing_date: currentDeal.filingDate,
  transaction_date: currentDeal.transactionDate,
  price: parseFloat(currentDeal.price) || 0,
  shares: parseInt(currentDeal.securitiesTransacted) || 0,
  value: Math.round((parseFloat(currentDeal.price) || 0) * (parseInt(currentDeal.securitiesTransacted) || 0) * 100) / 100,
  code: 'P',
  ownership_type: currentDeal.directOrIndirect === 'D' ? 'Direct' : 'Indirect',
  sec_url: currentDeal.url
};

return [{
  json: {
    originalDeal: currentDeal,
    mappedDeal: mappedDeal,
    dedupKey: dedupKey,
    symbol: currentDeal.symbol,
    mongoQuery: cardQuery,
    processingTimestamp: new Date().toISOString()
  }
}];
```
**💡 ПОЯСНЕНИЕ:**
- **Dedup key:** Композитный ключ из 6 полей для уникальности сделок
- **30-card window:** Оптимизация поиска - только последние 30 карточек по дате
- **Data mapping:** FMP формат → MongoDB schema согласно Level 2 спецификации
- **Value calculation:** Автоматический расчет стоимости сделки (price × shares)
- **Type conversion:** Безопасное преобразование строк в числа с fallback

---

### Узел 7: MongoDB (Card Lookup)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Поиск существующих карточек компании в базе данных (30-карточное окно)  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная конфигурация MongoDB find operation

```json
{
  "resource": "document",
  "operation": "find",
  "collection": "deals",
  "query": "={{JSON.parse($json.mongoQuery.find.query)}}",
  "options": {
    "sort": "={{JSON.parse($json.mongoQuery.find.options.sort)}}",
    "limit": "={{$json.mongoQuery.find.options.limit}}"
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Dynamic query:** Использует подготовленный query из предыдущего узла
- **Collection:** `deals` - основная коллекция карточек компаний
- **Sort:** `created_at DESC` - новейшие карточки первыми
- **Limit:** 30 карточек для оптимизации (согласно Level 2)
- **Credential:** Использует существующий `mongoDb` credential

---

### Узел 8: Code (Card Status Logic)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Логика статусной модели карточек, определение действия (CREATE/UPDATE/SKIP)  
**🔧 СТАТУС КОДА:** CONCEPT - сложная бизнес-логика статусов и дедупликации

**Режим:** `runOnceForEachItem` - анализирует текущую сделку против найденных карточек

```javascript
const dealData = $input.item(0).json;
const existingCards = $input.item(1).json || [];

// Deduplication check
let isDuplicate = false;
let targetCard = null;
let currentSessionCard = null;

for (const card of existingCards) {
  // Check existing deals
  for (const existingDeal of (card.trades || [])) {
    const existingDedupKey = [
      card.symbol,
      existingDeal.transaction_date,
      existingDeal.insider_name,
      existingDeal.shares,
      existingDeal.price,
      existingDeal.sec_url
    ].join('|');
    
    if (existingDedupKey === dealData.dedupKey) {
      isDuplicate = true;
      break;
    }
  }
  
  // Find current session card
  const cardDate = new Date(card.created_at);
  const today = new Date();
  const isToday = cardDate.toDateString() === today.toDateString();
  
  if (isToday && card.trade_status === 'New') {
    currentSessionCard = card;
  }
  
  if (!targetCard && (card.trade_status === 'New' || card.trade_status === 'Renew')) {
    targetCard = card;
  }
}

// Determine action
let action, cardStatus, cardId;

if (isDuplicate) {
  action = 'SKIP';
} else if (currentSessionCard) {
  action = 'UPDATE_CURRENT_SESSION';
  cardStatus = 'New';
  cardId = currentSessionCard._id;
} else if (targetCard) {
  action = 'UPDATE_PREVIOUS_CARD';
  cardStatus = 'Renew';
  cardId = targetCard._id;
} else {
  action = 'CREATE_NEW_CARD';
  cardStatus = 'New';
}

return [{
  json: {
    ...dealData,
    cardAction: action,
    cardStatus: cardStatus,
    cardId: cardId,
    skipProcessing: action === 'SKIP'
  }
}];
```
**💡 ПОЯСНЕНИЕ:**
- **Дедупликация:** Проверка против всех существующих сделок в карточках
- **Current session логика:** Карточки созданные сегодня со статусом 'New'
- **Статусная модель:** New (текущая сессия) → Renew (следующие сессии) → Old (опубликовано)
- **Action determination:** 4 возможных действия на основе состояния карточек
- **Data preservation:** Передает все данные + решение о действии

---

### Узел 9: If (Skip Duplicate Check)
**Тип:** `nodes-base.if` (v2.2)  
**📍 НАЗНАЧЕНИЕ:** Пропуск дублированных сделок, оптимизация обработки  
**🔧 СТАТУС КОДА:** TEMPLATE - conditional логика для skip optimization

```json
{
  "conditions": {
    "options": {
      "caseSensitive": true,
      "leftValue": "={{$json.skipProcessing}}",
      "operation": {
        "type": "boolean", 
        "operation": "false"
      }
    }
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Condition:** `skipProcessing === false` - обрабатывать только non-duplicate сделки
- **TRUE path** → Узел 10 (продолжение обработки)
- **FALSE path** → Обратно к Узел 5 (следующая итерация без обработки)
- Оптимизация: избегает ненужных API calls для дубликатов

---

### Узел 10: HTTP Request (Company Profile)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Получение профиля компании от FMP для новых карточек  
**🔧 СТАТУС КОДА:** CONCEPT - conditional API call с dynamic URL

```json
{
  "method": "GET",
  "url": "={{`https://financialmodelingprep.com/api/v3/profile/${$json.symbol}`}}",
  "authentication": "genericCredentialType",
  "genericAuthType": "httpQueryAuth",
  "options": {
    "timeout": 30000,
    "response": {
      "response": {
        "responseFormat": "json",
        "neverError": true
      }
    }
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Dynamic URL:** Использует symbol из текущей сделки
- **Same authentication:** Переиспользует FMP API credential
- **neverError: true** - продолжает работу даже если профиль недоступен
- **Timeout:** 30 секунд для внешнего API
- Выполняется только для non-duplicate сделок

---

### Узел 11: Code (MongoDB Operations)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Формирование MongoDB операций (INSERT/UPDATE) на основе cardAction  
**🔧 СТАТУС КОДА:** CONCEPT - подготовка операций для различных сценариев

**Режим:** `runOnceForEachItem` - подготавливает операцию для текущей сделки

```javascript
const processedData = $input.item(0).json;
const companyProfile = $input.item(1).json?.[0] || {};

const timestamp = new Date().toISOString();
let mongoOperation;

switch (processedData.cardAction) {
  case 'CREATE_NEW_CARD':
    mongoOperation = {
      operation: 'insert',
      document: {
        trade_status: 'New',
        symbol: processedData.symbol,
        company_name: companyProfile.companyName || processedData.symbol,
        company_marketcap: companyProfile.marketCap || 0,
        industry: companyProfile.industry || 'Unknown',
        chart_url: `https://images.weserv.nl/?url=finviz.com/chart.ashx%3Ft%3D${processedData.symbol}`,
        company_about: companyProfile.description || '',
        created_at: timestamp,
        updated_at: timestamp,
        posted_at: null,
        trades: [processedData.mappedDeal]
      }
    };
    break;
    
  case 'UPDATE_CURRENT_SESSION':
  case 'UPDATE_PREVIOUS_CARD':
    mongoOperation = {
      operation: 'findOneAndUpdate',
      updateKey: '_id',
      updateValue: processedData.cardId,
      updates: {
        trade_status: processedData.cardStatus,
        updated_at: timestamp,
        '$push': {
          trades: processedData.mappedDeal
        }
      }
    };
    break;
    
  default:
    return [{ json: { skipped: true, action: processedData.cardAction } }];
}

return [{ 
  json: { 
    mongoOperation: mongoOperation,
    symbol: processedData.symbol,
    action: processedData.cardAction
  }
}];
```
**💡 ПОЯСНЕНИЕ:**
- **Switch логика:** 3 различных типа операций на основе cardAction
- **CREATE_NEW_CARD:** Полная карточка с company profile + первой сделкой
- **UPDATE operations:** Добавление сделки в существующую карточку + статус update
- **Fallback data:** Использует symbol как company_name если профиль недоступен
- **Chart URL generation:** Автоматическая генерация ссылки на график Finviz

---

### Узел 12: MongoDB (Execute Operation)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Выполнение подготовленной MongoDB операции (INSERT или UPDATE)  
**🔧 СТАТУС КОДА:** CONCEPT - dynamic operation execution с universal configuration

```json
{
  "resource": "document",
  "operation": "={{$json.mongoOperation.operation}}",
  "collection": "deals",
  "query": "={{$json.mongoOperation.query || '{}'}}",
  "updateKey": "={{$json.mongoOperation.updateKey || 'id'}}",
  "fields": "={{Object.keys($json.mongoOperation.document || $json.mongoOperation.updates || {}).join(',')}}",
  "upsert": false
}
```
**💡 ПОЯСНЕНИЕ:**
- **Dynamic operation:** INSERT или findOneAndUpdate в зависимости от подготовленной операции
- **Universal config:** Работает для всех типов операций через conditional properties
- **Collection:** `deals` - основная коллекция карточек
- **No upsert:** Строгий контроль операций без автоматического создания
- **После выполнения** → возврат к Узел 5 для следующей итерации

---

## 🤖 Блок 3: AI Analysis & Intelligence (Узлы 13-17)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение карточек со статусом "New", AI анализ компаний через DeepSeek + web search, создание surveys записей в MongoDB

### Узел 13: MongoDB (New Cards Query)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Выборка карточек со статусом "New" для отправки на AI анализ  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартный MongoDB find для статусной фильтрации

```json
{
  "resource": "document",
  "operation": "find",
  "collection": "deals",
  "query": "{{ JSON.stringify({ trade_status: 'New' }) }}",
  "options": {
    "sort": "{{ JSON.stringify({ created_at: 1 }) }}",
    "limit": 100
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Filter:** `trade_status: "New"` - только карточки текущей сессии для AI анализа
- **Sort:** `created_at ASC` - обработка в порядке создания карточек
- **Limit:** 100 карточек максимум (защита от перегрузки AI Agent)
- **Input:** Данные из завершенного Блока 2 (Split In Batches Done output)

---

### Узел 14: Split In Batches (AI Processing)
**Тип:** `nodes-base.splitInBatches` (v3)  
**📍 НАЗНАЧЕНИЕ:** Поочередная обработка каждой компании через AI Agent для избежания rate limits  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная конфигурация для sequential AI processing

```json
{
  "batchSize": 1,
  "options": {
    "reset": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- `batchSize: 1` - обрабатываем по одной компании (критично для AI Agent rate limits)
- `reset: false` - сохраняем состояние между итерациями AI анализа
- **Loop output** → Узел 15 (AI Agent анализ)
- **Done output** → Блок 4 (переход к Content Generation)

---

### Узел 15: AI Agent (Company Analysis)
**Тип:** `nodes-langchain.agent` (v2.2)  
**📍 НАЗНАЧЕНИЕ:** Автономный анализ компании с web search через DeepSeek + SerpApi  
**🔧 СТАТУС КОДА:** CONCEPT - основная AI Agent конфигурация с dynamic prompt

```json
{
  "promptType": "define",
  "text": "={{`Проанализируй компанию ${$json.company_name} (${$json.symbol}) и ответь на вопросы в JSON формате.\n\nВопросы:\n1. Каково текущее состояние финансового здоровья компании?\n2. Каковы катализаторы роста этой компании?\n3. Каковы основные риски для инвестирования в эту компанию на данный момент?\n4. Что конкретно производит компания и какова динамика продаж продукции за последние два года по кварталам?\n\nИспользуй актуальную информацию из интернета для ответов. Каждый ответ должен быть до 1000 символов на русском языке.\n\nФормат ответа: [{"q": "вопрос 1", "a": "ответ 1"}, {"q": "вопрос 2", "a": "ответ 2"}, ...]\n\nТолько JSON, без дополнительного текста.`}}",
  "hasOutputParser": false,
  "options": {
    "systemMessage": "Ты финансовый аналитик. Используй web search для получения актуальной информации о компаниях. Отвечай точно и лаконично на русском языке.",
    "maxIterations": 5,
    "returnIntermediateSteps": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Dynamic prompt:** Использует данные компании из текущей карточки
- **JSON format:** Четко определенная структура ответа для parsing
- **System message:** Контекст финансового аналитика с web search инструкциями
- **Max iterations:** 5 попыток для получения качественного ответа
- **Connections:** DeepSeek Chat Model (language model) + SerpApi Tool (web search)

---

### Узел 15a: DeepSeek Chat Model (Connected to AI Agent)
**Тип:** `nodes-langchain.lmChatDeepSeek` (v1)  
**📍 НАЗНАЧЕНИЕ:** Языковая модель для AI Agent с поддержкой JSON output  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная DeepSeek конфигурация для structured output

```json
{
  "model": "deepseek-chat",
  "options": {
    "temperature": 0.3,
    "maxTokens": 2000,
    "responseFormat": "json_object"
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Model:** `deepseek-chat` - основная модель для conversation и reasoning
- **Temperature:** 0.3 - баланс между креативностью и точностью для финанализа
- **Max tokens:** 2000 - достаточно для 4 ответов по 1000 символов
- **JSON format:** Структурированный выход для автоматической обработки
- **Connection:** AI Agent ←→ DeepSeek Chat Model

---

### Узел 15b: SerpApi Tool (Connected to AI Agent)
**Тип:** `nodes-langchain.toolSerpApi` (v1)  
**📍 НАЗНАЧЕНИЕ:** Google Search интеграция для получения актуальной информации о компаниях  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная SerpApi конфигурация

```json
{
  "connectionParameters": {
    "device": "desktop",
    "googleDomain": "google.com",
    "country": "us",
    "language": "en"
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Device:** desktop - полные результаты поиска
- **Domain:** google.com - международная версия для лучшего coverage
- **Country/Language:** US/EN для финансовой информации (переводится в ответах)
- **Auto-activation:** AI Agent сам определяет когда использовать web search
- **Connection:** AI Agent ←→ SerpApi Tool

---

### Узел 16: Code (AI Response Processing)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Обработка JSON ответа от AI Agent, валидация и подготовка для surveys коллекции  
**🔧 СТАТУС КОДА:** CONCEPT - обработка AI output с error handling

**Режим:** `runOnceForEachItem` - обрабатывает AI ответ для текущей компании

```javascript
const companyCard = $input.item(0).json; // From Split In Batches
const aiResponse = $input.item(1).json; // From AI Agent

let parsedQA;
let processingError = null;

try {
  // Parse AI Agent response
  const responseText = aiResponse.text || aiResponse.response || aiResponse.output || '';
  
  // Try to parse JSON from AI response
  if (responseText.includes('[') && responseText.includes(']')) {
    const jsonStart = responseText.indexOf('[');
    const jsonEnd = responseText.lastIndexOf(']') + 1;
    const jsonString = responseText.slice(jsonStart, jsonEnd);
    parsedQA = JSON.parse(jsonString);
  } else {
    throw new Error('No valid JSON array found in AI response');
  }
  
  // Validate structure
  if (!Array.isArray(parsedQA) || parsedQA.length === 0) {
    throw new Error('Invalid QA structure from AI');
  }
  
  // Ensure all items have q and a properties
  parsedQA = parsedQA.map(item => ({
    q: String(item.q || 'Unknown question').substring(0, 500),
    a: String(item.a || 'No answer provided').substring(0, 1000)
  }));
  
} catch (error) {
  processingError = error.message;
  console.log(`AI Response processing error for ${companyCard.symbol}: ${error.message}`);
  
  // Fallback QA structure
  parsedQA = [
    { q: "AI анализ недоступен", a: "Произошла ошибка при обработке ответа AI Agent" }
  ];
}

// Calculate token usage (estimation)
const responseText = aiResponse.text || '';
const estimatedInputTokens = Math.ceil(800); // Approximate prompt length
const estimatedOutputTokens = Math.ceil(responseText.length / 4); // ~4 chars per token
const estimatedCost = (estimatedInputTokens * 0.56e-6) + (estimatedOutputTokens * 1.68e-6);

// Prepare surveys document
const surveyDocument = {
  symbol: companyCard.symbol,
  polled_at: new Date().toISOString(),
  qa: parsedQA,
  tokens_used: {
    input: estimatedInputTokens,
    output: estimatedOutputTokens,
    total: estimatedInputTokens + estimatedOutputTokens
  },
  cost_usd: Math.round(estimatedCost * 100) / 100, // Round to cents
  telegraph_url: null, // Will be updated in Block 4
  processing_error: processingError
};

return [{
  json: {
    surveyDocument: surveyDocument,
    companyCard: companyCard,
    originalAiResponse: aiResponse,
    processingSuccess: !processingError
  }
}];
```
**💡 ПОЯСНЕНИЕ:**
- **JSON parsing:** Извлечение структурированного ответа из AI Agent output
- **Error handling:** Fallback на default QA при parsing ошибках
- **Data validation:** Проверка структуры и ограничение длины ответов
- **Token calculation:** Оценка стоимости AI Agent вызова
- **Survey preparation:** Подготовка документа для MongoDB surveys коллекции

---

### Узел 17: MongoDB (Survey Insert)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Сохранение результатов AI анализа в surveys коллекцию  
**🔧 СТАТУС КОДА:** CONCEPT - dynamic insert с prepared document

```json
{
  "resource": "document",
  "operation": "insert",
  "collection": "surveys",
  "fields": "symbol,polled_at,qa,tokens_used,cost_usd,telegraph_url,processing_error"
}
```
**💡 ПОЯСНЕНИЕ:**
- **Collection:** `surveys` - отдельная коллекция для AI анализа
- **Operation:** INSERT - всегда новая запись для каждого анализа
- **Document source:** Использует подготовленный surveyDocument из предыдущего узла
- **Fields:** Все поля surveys schema согласно Level 2 спецификации
- **После выполнения** → возврат к Узел 14 для следующей компании

---

## 📋 Updated Connections Flow:
```
1 → 2 → 3 → 4[TRUE] → 5[Loop] → 6 → 7 → 8 → 9[TRUE] → 10 → 11 → 12 → 5[Loop]
                  ↑[FALSE] → END
                                                    ↑[FALSE] → 5[Loop] 
                      ↑[Done] → 13 → 14[Loop] → 15 → 16 → 17 → 14[Loop]
                                         ↑[Done] → Блок 4 (следующие блоки)
```

**AI Agent Connections:**
```
15 (AI Agent) ←→ 15a (DeepSeek Chat Model)
15 (AI Agent) ←→ 15b (SerpApi Tool)
```

## 🔧 Required Credentials:
- **FMP API** (ID: k887gSxTZZEgRYIa) - httpQueryAuth для узлов 2, 10
- **MongoDB** - mongoDb credential для узлов 7, 12, 13, 17
- **DeepSeek API** - deepSeekApi credential для узла 15a
- **SerpApi** - serpApi credential для узла 15b

---

**📝 СТАТУС ЗАВЕРШЕНИЯ БЛОКОВ 1-3:** CONCEPT с улучшенными пояснениями  
**🔄 СЛЕДУЮЩИЕ ЭТАПЫ:** Блоки 4-5 требуют детализации (Content Publishing, State Management)