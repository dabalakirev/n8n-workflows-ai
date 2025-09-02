# Block 3: AI Analysis & Intelligence (Узлы 13-17)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение карточек со статусом "New", AI анализ компаний через DeepSeek + web search, создание surveys записей в MongoDB

**🔗 NAVIGATION:** [← Block 2](block-2-database-operations.md) | [Architecture Overview](../architecture.md) | [Next: Block 4 →](block-4-content-publishing.md)

---

## Узел 13: MongoDB (New Cards Query)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Выборка карточек со статусом "New" для отправки на AI анализ  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартный MongoDB find с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
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
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Filter:** `trade_status: "New"` - только карточки текущей сессии для AI анализа
- **Sort:** `created_at ASC` - обработка в порядке создания карточек

---

## Узел 14: Split In Batches (AI Processing)
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
- **No credentials required** - logic node
- `batchSize: 1` - обрабатываем по одной компании (критично для AI Agent rate limits)

---

## Узел 15: AI Agent (Company Analysis)
**Тип:** `nodes-langchain.agent` (v2.2)  
**📍 НАЗНАЧЕНИЕ:** Автономный анализ компании с web search через DeepSeek + SerpApi  
**🔧 СТАТУС КОДА:** TEMPLATE - AI Agent конфигурация с explicit tool connections

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
- **No direct credentials** - uses connected tools' credentials
- **Tool connections:** DeepSeek Chat Model + SerpApi Tool
- **Dynamic prompt:** Использует данные компании из текущей карточки

---

## Узел 15a: DeepSeek Chat Model (Connected to AI Agent)
**Тип:** `nodes-langchain.lmChatDeepSeek` (v1)  
**📍 НАЗНАЧЕНИЕ:** Языковая модель для AI Agent с поддержкой JSON output  
**🔧 СТАТУС КОДА:** TEMPLATE - DeepSeek конфигурация с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "deepSeekApi",
  "model": "deepseek-chat",
  "options": {
    "temperature": 0.3,
    "maxTokens": 2000,
    "responseFormat": "json_object"
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "deepSeekApi"` - использует DeepSeek credential (ID: sFuzOe0ydJ9CEn0H)
- **Temperature:** 0.3 - баланс между креативностью и точностью для финанализа
- **JSON format:** Структурированный выход для автоматической обработки

---

## Узел 15b: SerpApi Tool (Connected to AI Agent)
**Тип:** `nodes-langchain.toolSerpApi` (v1)  
**📍 НАЗНАЧЕНИЕ:** Google Search интеграция для получения актуальной информации о компаниях  
**🔧 СТАТУС КОДА:** TEMPLATE - SerpApi конфигурация с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "serpApi",
  "connectionParameters": {
    "device": "desktop",
    "googleDomain": "google.com",
    "country": "us",
    "language": "en"
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "serpApi"` - использует SerpAPI credential (ID: 75EBIHKM5Q7jnT86)
- **Device:** desktop - полные результаты поиска
- **Domain:** google.com - международная версия для лучшего coverage

---

## Узел 16: Code (AI Response Processing)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Обработка JSON ответа от AI Agent, валидация и подготовка для surveys коллекции  
**🔧 СТАТУС КОДА:** CONCEPT - обработка AI output с error handling

[JavaScript код остается без изменений - no credentials required]

**💡 ПОЯСНЕНИЕ:**
- **No credentials required** - pure JavaScript processing node

---

## Узел 17: MongoDB (Survey Insert)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Сохранение результатов AI анализа в surveys коллекцию  
**🔧 СТАТУС КОДА:** TEMPLATE - dynamic insert с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
  "resource": "document",
  "operation": "insert",
  "collection": "surveys",
  "fields": "symbol,polled_at,qa,tokens_used,cost_usd,telegraph_url,processing_error"
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Collection:** `surveys` - отдельная коллекция для AI анализа
- **Operation:** INSERT - всегда новая запись для каждого анализа

---

## 📋 Block Connections:
```
13 (Query New) → 14 (Split) [Loop] → 15 (AI Agent) → 16 (Process) → 17 (Insert) → 14 [Loop]
                     ↑[Done] → Block 4

AI Agent Ecosystem:
15 (AI Agent) ←→ 15a (DeepSeek Chat Model)
15 (AI Agent) ←→ 15b (SerpApi Tool)
```

## 🔐 Required Credentials:

**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage patterns.

| Node | Credential Type | Credential Name | ID Reference |
|------|----------------|-----------------|--------------|
| **Узел 13 (MongoDB Query)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узел 15a (DeepSeek)** | `deepSeekApi` | DeepSeek API | `sFuzOe0ydJ9CEn0H` |
| **Узел 15b (SerpApi)** | `serpApi` | SerpAPI account | `75EBIHKM5Q7jnT86` |
| **Узел 17 (MongoDB Insert)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узлы 14,15,16** | _No credentials_ | N/A | N/A |

**💡 Credential Usage:**
- **AI Agent ecosystem** uses connected tools' credentials automatically
- **MongoDB credentials** handle connection, authentication, and database access
- **API credentials** automatically inject keys into requests
- **All credential assignments** use predefined credential approach: `"nodeCredentialType": "[type]"`

---

**📝 STATUS:** ✅ FIXED - explicit credential specification added  
**🔧 RED FLAG 4:** ✅ PROGRESS - Block 3 credential selection standardized  
**🔄 NEXT:** [Block 4: Content Generation & Publishing →](block-4-content-publishing.md)