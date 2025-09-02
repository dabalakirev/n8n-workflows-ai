# Block 3: AI Analysis & Intelligence (Узлы 13-17)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение карточек со статусом "New", AI анализ компаний через DeepSeek + web search, создание surveys записей в MongoDB

**🔗 NAVIGATION:** [← Block 2](block-2-database-operations.md) | [Architecture Overview](../architecture.md) | [Next: Block 4 →](block-4-content-publishing.md)

---

## Узел 13: MongoDB (New Cards Query)
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
- **Input:** Данные из завершенного Block 2 (Split In Batches Done output)

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
- `batchSize: 1` - обрабатываем по одной компании (критично для AI Agent rate limits)
- `reset: false` - сохраняем состояние между итерациями AI анализа
- **Loop output** → Узел 15 (AI Agent анализ)
- **Done output** → Block 4 (переход к Content Generation)

---

## Узел 15: AI Agent (Company Analysis)
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

## Узел 15a: DeepSeek Chat Model (Connected to AI Agent)
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

## Узел 15b: SerpApi Tool (Connected to AI Agent)
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

## Узел 16: Code (AI Response Processing)
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

## Узел 17: MongoDB (Survey Insert)
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

## 📋 Block Connections:
```
13 (Query New) → 14 (Split) [Loop] → 15 (AI Agent) → 16 (Process) → 17 (Insert) → 14 [Loop]
                     ↑[Done] → Block 4

AI Agent Ecosystem:
15 (AI Agent) ←→ 15a (DeepSeek Chat Model)
15 (AI Agent) ←→ 15b (SerpApi Tool)
```

## 🔧 Required Credentials:
**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage

---

**📝 STATUS:** ✅ COMPLETE - концептуальная спецификация с AI Agent ecosystem  
**🔄 NEXT:** [Block 4: Content Generation & Publishing →](block-4-content-publishing.md)