# Block 2: Database Operations & Card Management (Узлы 5-12)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Идемпотентная обработка сделок, управление карточками компаний, дедупликация, статусная модель (New/Renew/Old)

**🔗 NAVIGATION:** [← Block 1](block-1-data-collection.md) | [Architecture Overview](../architecture.md) | [Next: Block 3 →](block-3-ai-analysis.md)

---

## Узел 5: Split In Batches
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
- **No credentials required** - logic node
- `batchSize: 1` - обрабатываем по одной сделке (критично для дедупликации)
- `reset: false` - сохраняем состояние между итерациями

---

## Узел 6: Code (Deal Processing Logic)
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
- **No credentials required** - pure JavaScript processing node
- **Dedup key:** Композитный ключ из 6 полей для уникальности сделок
- **30-card window:** Оптимизация поиска - только последние 30 карточек по дате
- **Data mapping:** FMP формат → MongoDB schema согласно Level 2 спецификации

---

## Узел 7: MongoDB (Card Lookup)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Поиск существующих карточек компании в базе данных (30-карточное окно)  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная конфигурация MongoDB find с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
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
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Dynamic query:** Использует подготовленный query из предыдущего узла
- **Collection:** `deals` - основная коллекция карточек компаний

---

## Узел 8: Code (Card Status Logic)
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
- **No credentials required** - pure JavaScript processing node
- **Дедупликация:** Проверка против всех существующих сделок в карточках
- **Current session логика:** Карточки созданные сегодня со статусом 'New'
- **Статусная модель:** New (текущая сессия) → Renew (следующие сессии) → Old (опубликовано)

---

## Узел 9: If (Skip Duplicate Check)
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
- **No credentials required** - logic node
- **Condition:** `skipProcessing === false` - обрабатывать только non-duplicate сделки
- **TRUE path** → Узел 10 (продолжение обработки)
- **FALSE path** → Обратно к Узел 5 (следующая итерация без обработки)

---

## Узел 10: HTTP Request (Company Profile)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Получение профиля компании от FMP для новых карточек  
**🔧 СТАТУС КОДА:** TEMPLATE - conditional API call с explicit credential selection

```json
{
  "method": "GET",
  "url": "={{`https://financialmodelingprep.com/api/v3/profile/${$json.symbol}`}}",
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "httpQueryAuth",
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
- **Credential:** `nodeCredentialType: "httpQueryAuth"` - использует FMP API credential (ID: k887gSxTZZEgRYIa)
- **Dynamic URL:** Использует symbol из текущей сделки
- **neverError: true** - продолжает работу даже если профиль недоступен

---

## Узел 11: Code (MongoDB Operations Preparation)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Формирование MongoDB операций (INSERT/UPDATE) на основе cardAction  
**🔧 СТАТУС КОДА:** TEMPLATE - n8n-compatible operation preparation

**Режим:** `runOnceForEachItem` - подготавливает операцию для текущей сделки

```javascript
const processedData = $input.item(0).json;
const companyProfile = $input.item(1).json?.[0] || {};

const timestamp = new Date().toISOString();

switch (processedData.cardAction) {
  case 'CREATE_NEW_CARD':
    return [{
      json: {
        operation: 'insert',
        symbol: processedData.symbol,
        action: processedData.cardAction,
        // Document data for INSERT
        trade_status: 'New',
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
    }];
    
  case 'UPDATE_CURRENT_SESSION':
  case 'UPDATE_PREVIOUS_CARD':
    return [{
      json: {
        operation: 'findOneAndUpdate',
        updateTargetId: processedData.cardId,
        symbol: processedData.symbol,
        action: processedData.cardAction,
        // Update data for findOneAndUpdate
        trade_status: processedData.cardStatus,
        updated_at: timestamp,
        newTrade: processedData.mappedDeal
      }
    }];
    
  default:
    return [{ json: { skipped: true, action: processedData.cardAction } }];
}
```
**💡 ПОЯСНЕНИЕ:**
- **No credentials required** - pure JavaScript processing node
- **n8n Compatible:** Данные подготовлены в формате, который понимает MongoDB node
- **Separate data structures:** INSERT использует прямые поля, UPDATE использует updateTargetId

---

## Узел 12: MongoDB (Execute Operation)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Выполнение подготовленной MongoDB операции (INSERT или findOneAndUpdate)  
**🔧 СТАТУС КОДА:** TEMPLATE - dynamic operation execution с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
  "resource": "document",
  "operation": "={{$json.operation}}",
  "collection": "deals",
  "updateKey": "_id",
  "fields": "={{$json.operation === 'insert' ? 'trade_status,symbol,company_name,company_marketcap,industry,chart_url,company_about,created_at,updated_at,posted_at,trades' : 'trade_status,updated_at'}}",
  "upsert": false
}
```

**🔧 ADDITIONAL CODE for findOneAndUpdate ($push operation):**
**Добавить отдельный Code node (12a) перед MongoDB node для UPDATE операций:**

```javascript
// For UPDATE operations - prepare $push for trades array
if ($json.operation === 'findOneAndUpdate') {
  return [{
    json: {
      ...$json,
      // Set the document ID that updateKey will match against
      _id: $json.updateTargetId,
      // Prepare $push update for trades
      '$push': {
        trades: $json.newTrade
      }
    }
  }];
} else {
  // For INSERT operations - pass through
  return [$input.all()];
}
```

**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Dynamic operation:** INSERT или findOneAndUpdate определяется из input data
- **updateKey="_id":** Поиск документа по _id поля (стандартный MongoDB подход)

---

## 📋 Block Connections (UPDATED):
```
5 (Split) [Loop] → 6 (Process) → 7 (Lookup) → 8 (Status) → 9 (Skip Check)
    ↑                                                            ↑[TRUE] → 10 (Profile) → 11 (Prepare) → 12a (Update Logic) → 12 (Execute) → 5 [Loop]
    ↑[Done] → Block 3                                            ↑[FALSE] → 5 [Loop]
```

## 🔐 Required Credentials:

**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage patterns.

| Node | Credential Type | Credential Name | ID Reference |
|------|----------------|-----------------|--------------|
| **Узел 7 (MongoDB Lookup)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узел 10 (FMP Profile)** | `httpQueryAuth` | FMP API | `k887gSxTZZEgRYIa` |
| **Узел 12 (MongoDB Execute)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узлы 5,6,8,9,11,12a** | _No credentials_ | N/A | N/A |

**💡 Credential Usage:**
- **MongoDB credentials** automatically handle connection, authentication, and database selection
- **FMP API credential** automatically injects API key via query parameter
- **All credential assignments** use predefined credential approach: `"nodeCredentialType": "[type]"`

---

**📝 STATUS:** ✅ FIXED - explicit credential specification added  
**🔧 RED FLAG 4:** ✅ PROGRESS - Block 2 credential selection standardized  
**🔄 NEXT:** [Block 3: AI Analysis & Intelligence →](block-3-ai-analysis.md)