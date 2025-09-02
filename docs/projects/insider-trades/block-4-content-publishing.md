# Block 4: Content Generation & Publishing (Узлы 18-23)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение AI анализа из surveys коллекции, создание Telegraph статей, публикация в Telegram канал с inline кнопками

**🔗 NAVIGATION:** [← Block 3](block-3-ai-analysis.md) | [Architecture Overview](../architecture.md) | [Next: Block 5 →](block-5-state-management.md)

---

## Узел 18: MongoDB (Survey Results Query)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Выборка AI анализа для компаний со статусом "New" для создания Telegraph статей  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартный MongoDB find с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
  "resource": "document",
  "operation": "find",
  "collection": "surveys",
  "query": "{{ JSON.stringify({ telegraph_url: null }) }}",
  "options": {
    "sort": "{{ JSON.stringify({ polled_at: -1 }) }}",
    "limit": 100
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Filter:** `telegraph_url: null` - только surveys без созданных статей
- **Sort:** `polled_at DESC` - последние AI анализы сначала  

---

## Узел 19: Split In Batches (Content Processing)
**Тип:** `nodes-base.splitInBatches` (v3)  
**📍 НАЗНАЧЕНИЕ:** Поочередная обработка каждого survey для создания Telegraph статьи  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартная конфигурация для sequential content creation

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
- `batchSize: 1` - создаем по одной Telegraph статье (избегание rate limits)

---

## Узел 20: HTTP Request (Telegraph Article Creation)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Создание Telegraph статьи на основе AI анализа компании  
**🔧 СТАТУС КОДА:** TEMPLATE - Telegraph API integration с explicit credential

```json
{
  "method": "POST",
  "url": "https://api.telegra.ph/createPage",
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "httpQueryAuth",
  "sendBody": true,
  "bodyContentType": "json",
  "jsonBody": "={{ JSON.stringify({\n  title: `${$json.symbol} - ${$json.qa[0]?.q || 'Анализ компании'}`,\n  content: $json.qa.map(item => ({\n    tag: 'p',\n    children: [\n      { tag: 'strong', children: [item.q + ':'] },\n      { tag: 'br' },\n      item.a\n    ]\n  })),\n  return_content: false,\n  author_name: 'Insider Trades Bot',\n  author_url: 'https://t.me/insider_trades_channel'\n}) }}",
  "options": {
    "timeout": 10000,
    "retry": {
      "enabled": true,
      "maxAttempts": 2
    },
    "response": {
      "responseFormat": "json",
      "outputPropertyName": "telegraphResponse"
    }
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "httpQueryAuth"` - использует Telegraph API credential (ID: O5WldXH0xHIjyQgD)
- **Method:** POST к Telegraph createPage API
- **Title:** `"SYMBOL - Первый вопрос"` для читаемости

---

## Узел 21: Code (Telegraph Response Processing & Survey Update)
[JavaScript код остается без изменений - no credentials required]

**💡 ПОЯСНЕНИЕ:**
- **No credentials required** - pure JavaScript processing node

---

## Узел 21a: MongoDB (Individual Survey Telegraph Update)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Individual обновление survey с Telegraph URL или error status  
**🔧 СТАТУС КОДА:** TEMPLATE - individual survey update с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
  "resource": "document",
  "operation": "findOneAndUpdate",
  "collection": "surveys",
  "updateKey": "_id",
  "fields": "telegraph_url,updated_at,publishing_status,publishing_error",
  "upsert": false
}
```

## Узел 21b: Code (Update Preparation)
[JavaScript код остается без изменений - no credentials required]

**💡 ПОЯСНЕНИЯ:**
- **21a Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **21b:** No credentials required - pure JavaScript processing node

---

## Узел 22: MongoDB (Company Card Lookup)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Получение данных карточки компании для Telegram сообщения  
**🔧 СТАТУС КОДА:** TEMPLATE - lookup join с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
  "resource": "document",
  "operation": "findOne",
  "collection": "deals",
  "query": "{{ JSON.stringify({ symbol: $json.telegramPayload.symbol, trade_status: { $in: ['New', 'Renew'] } }) }}",
  "options": {
    "sort": "{{ JSON.stringify({ updated_at: -1 }) }}"
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Collection:** `deals` - основная коллекция карточек компаний

---

## Узел 23: HTTP Request (Telegram Publishing)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Публикация сообщения с фото и inline кнопкой в Telegram канал  
**🔧 СТАТУС КОДА:** TEMPLATE - Telegram Bot API с explicit credential

```json
{
  "method": "POST",
  "url": "https://api.telegram.org/bot{{ $credentials.telegramBot.token }}/sendPhoto",
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "telegramApi",
  "sendBody": true,
  "bodyContentType": "json",
  "jsonBody": "[Existing dynamic JSON body code...]",
  "options": {
    "timeout": 15000,
    "retry": {
      "enabled": true,
      "maxAttempts": 3
    },
    "response": {
      "responseFormat": "json",
      "neverError": false
    }
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "telegramApi"` - использует Telegram credential (ID: IPk73kQxS5AUJ1Ni)
- **Method:** sendPhoto для сообщений с изображениями

---

## 📋 Block Connections (UPDATED):
```
18 (Survey Query) → 19 (Split) [Loop] → 20 (Telegraph) → 21 (Process) → 21b (Update Prep) → 21a (Survey Update) → 22 (Card Lookup) → 23 (Telegram) → 19 [Loop]
                         ↑[Done] → Block 5
```

## 🔐 Required Credentials:

**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage patterns.

| Node | Credential Type | Credential Name | ID Reference |
|------|----------------|-----------------|--------------|
| **Узел 18 (MongoDB Query)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узел 20 (Telegraph API)** | `httpQueryAuth` | Telegraph API | `O5WldXH0xHIjyQgD` |
| **Узел 21a (MongoDB Update)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узел 22 (MongoDB Lookup)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узел 23 (Telegram API)** | `telegramApi` | Telegram API | `IPk73kQxS5AUJ1Ni` |
| **Узлы 19,21,21b** | _No credentials_ | N/A | N/A |

**💡 Credential Usage:**
- **MongoDB credentials** handle connection, authentication, database access
- **Telegraph/Telegram credentials** automatically inject API keys/tokens
- **All credential assignments** use predefined credential approach: `"nodeCredentialType": "[type]"`

---

**📝 STATUS:** ✅ FIXED - explicit credential specification added  
**🔧 RED FLAG 4:** ✅ PROGRESS - Block 4 credential selection standardized  
**🔄 NEXT:** [Block 5: State Management & Completion →](block-5-state-management.md)