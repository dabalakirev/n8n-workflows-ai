# Block 4: Content Generation & Publishing (Узлы 18-23)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение AI анализа из surveys коллекции, создание Telegraph статей, публикация в Telegram канал с inline кнопками

**🔗 NAVIGATION:** [← Block 3](block-3-ai-analysis.md) | [Architecture Overview](../architecture.md) | [Next: Block 5 →](block-5-state-management.md)

---

## Узел 18: MongoDB (Survey Results Query)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Выборка AI анализа для компаний со статусом "New" для создания Telegraph статей  
**🔧 СТАТУС КОДА:** TEMPLATE - стандартный MongoDB find с join-like логикой

```json
{
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
- **Filter:** `telegraph_url: null` - только surveys без созданных статей
- **Sort:** `polled_at DESC` - последние AI анализы сначала  
- **Limit:** 100 surveys максимум (соответствует Block 3 лимиту)
- **Input:** Done output из Block 3 (Split In Batches завершен)
- **Logic:** Находим surveys созданные в Block 3, но еще не опубликованные

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
- `batchSize: 1` - создаем по одной Telegraph статье (избегание rate limits)
- `reset: false` - сохраняем состояние для перехода к следующему survey
- **Loop output** → Узел 20 (Telegraph создание статьи)
- **Done output** → Block 5 (переход к State Management)

---

## Узел 20: HTTP Request (Telegraph Article Creation)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Создание Telegraph статьи на основе AI анализа компании  
**🔧 СТАТУС КОДА:** CONCEPT - Telegraph API integration с dynamic content

```json
{
  "method": "POST",
  "url": "https://api.telegra.ph/createPage",
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "telegraphApi",
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
- **Method:** POST к Telegraph createPage API
- **Title:** `"SYMBOL - Первый вопрос"` для читаемости
- **Content:** Динамическое форматирование QA pairs как HTML параграфы
- **Author fields:** Branding для Insider Trades
- **Retry logic:** 2 попытки при network failures
- **Response:** Сохранение response в `telegraphResponse` field

---

## Узел 21: Code (Telegraph Response Processing)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Обработка Telegraph API response и подготовка данных для Telegram публикации  
**🔧 СТАТУС КОДА:** CONCEPT - response parsing с fallback logic

**Режим:** `runOnceForEachItem` - обрабатывает Telegraph response для текущего survey

```javascript
const surveyData = $input.first().json;
const telegraphResponse = $input.first().json.telegraphResponse;

let telegraphUrl = null;
let processingError = null;

try {
  // Parse Telegraph API response
  if (telegraphResponse && telegraphResponse.ok && telegraphResponse.result) {
    const pageInfo = telegraphResponse.result;
    if (pageInfo.url) {
      telegraphUrl = pageInfo.url;
    } else if (pageInfo.path) {
      telegraphUrl = `https://telegra.ph/${pageInfo.path}`;
    } else {
      throw new Error('No URL or path in Telegraph response');
    }
  } else {
    throw new Error(`Telegraph API error: ${telegraphResponse?.error || 'Unknown error'}`);
  }
  
} catch (error) {
  processingError = error.message;
  console.log(`Telegraph processing error for ${surveyData.symbol}: ${error.message}`);
  
  // Fallback: skip Telegraph URL (will be handled in Telegram publishing)
  telegraphUrl = null;
}

// Prepare data for Telegram publishing
// Need to fetch the corresponding company card from deals collection
const telegramPayload = {
  symbol: surveyData.symbol,
  telegraphUrl: telegraphUrl,
  qa: surveyData.qa,
  polledAt: surveyData.polled_at,
  processingError: processingError
};

return [{
  json: {
    telegramPayload: telegramPayload,
    surveyData: surveyData,
    telegraphSuccess: !!telegraphUrl
  }
}];
```
**💡 ПОЯСНЕНИЕ:**
- **Response parsing:** Извлечение Telegraph URL из API response
- **URL construction:** Обработка как полных URLs так и path references
- **Error handling:** Graceful fallback при Telegraph API ошибках
- **Data preparation:** Подготовка payload для Telegram publishing
- **Status tracking:** Boolean flag успешности Telegraph создания

---

## Узел 22: MongoDB (Company Card Lookup)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Получение данных карточки компании для Telegram сообщения  
**🔧 СТАТУС КОДА:** CONCEPT - lookup join между surveys и deals коллекциями

```json
{
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
- **Collection:** `deals` - основная коллекция карточек компаний
- **Filter:** Symbol match + статусы New/Renew для current/pending карточек
- **Sort:** `updated_at DESC` - последняя версия карточки
- **Operation:** findOne - expecting single result per symbol
- **Purpose:** Получение company data (chart_url, industry, trades) для Telegram

---

## Узел 23: HTTP Request (Telegram Publishing)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Публикация сообщения с фото и inline кнопкой в Telegram канал  
**🔧 СТАТУС КОДА:** CONCEPT - Telegram Bot API с dynamic content и error handling

```json
{
  "method": "POST",
  "url": "https://api.telegram.org/bot{{ $credentials.telegramBot.token }}/sendPhoto",
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "telegramBot",
  "sendBody": true,
  "bodyContentType": "json",
  "jsonBody": "={{ \n  const companyCard = $input.item(1).json; // From MongoDB lookup\n  const telegramData = $input.item(0).json.telegramPayload;\n  \n  // Format market cap\n  const formatMarketCap = (cap) => {\n    if (cap >= 1e12) return `${(cap / 1e12).toFixed(1)}T`;\n    if (cap >= 1e9) return `${(cap / 1e9).toFixed(1)}B`;\n    if (cap >= 1e6) return `${(cap / 1e6).toFixed(1)}M`;\n    return cap?.toString() || 'N/A';\n  };\n  \n  // Build trades text\n  const tradesText = companyCard.trades?.slice(0, 5).map(trade => \n    `👤 ${trade.insider_name} (${trade.role})\\n` +\n    `📅 ${new Date(trade.transaction_date).toLocaleDateString('ru-RU')}\\n` +\n    `💰 ${trade.shares?.toLocaleString('ru-RU')} акций по $${trade.price}\\n` +\n    `💵 Сумма: $${trade.value?.toLocaleString('ru-RU')}`\n  ).join('\\n\\n---\\n\\n') || 'Нет данных по сделкам';\n  \n  // Build caption\n  const caption = \n    `<b>${companyCard.company_name || telegramData.symbol}</b>\\n` +\n    `📊 ${companyCard.symbol} • ${companyCard.industry || 'N/A'}\\n` +\n    `💎 Капитализация: $${formatMarketCap(companyCard.company_marketcap)}\\n\\n` +\n    `<b>🔥 Недавние инсайдерские покупки:</b>\\n\\n` +\n    `${tradesText}`;\n  \n  // Build inline keyboard\n  const replyMarkup = {\n    inline_keyboard: [[\n      {\n        text: '📖 ПОДРОБНЕЕ',\n        url: telegramData.telegraphUrl || 'https://t.me/insider_trades_channel'\n      }\n    ]]\n  };\n  \n  return JSON.stringify({\n    chat_id: '3049635154',\n    photo: companyCard.chart_url || undefined,\n    caption: caption,\n    parse_mode: 'HTML',\n    reply_markup: replyMarkup\n  });\n}}",
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
- **Method:** sendPhoto для сообщений с изображениями
- **Photo:** chart_url из company card (fallback если недоступен)
- **Caption formatting:** HTML markup с company info и trades список
- **Market cap:** Человекочитаемый формат (3.5T, 950B, 12.3B)
- **Trades display:** Максимум 5 recent сделок с форматированием
- **Inline keyboard:** "ПОДРОБНЕЕ" кнопка → Telegraph URL
- **Error handling:** 3 retry attempts для network reliability
- **Fallback URL:** Channel link если Telegraph недоступен

---

## 📋 Block Connections:
```
18 (Survey Query) → 19 (Split) [Loop] → 20 (Telegraph) → 21 (Process) → 22 (Card Lookup) → 23 (Telegram) → 19 [Loop]
                         ↑[Done] → Block 5
```

## 🔧 Required Credentials:
**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage

## 📊 Data Flow Analysis:

### Input Requirements:
- **Block 3 completion** - surveys коллекция populated с AI анализом
- **Active company cards** - deals коллекция с New/Renew статусами

### Output Deliverables:
- **Telegraph articles** - published статьи с QA content
- **Telegram messages** - канальные сообщения с photos и inline кнопками
- **Survey updates** - telegraph_url поля populated

### Error Handling Strategy:
- **Telegraph failures** → skip article creation, log error, continue
- **Telegram failures** → retry 3 times, maintain card status для re-processing
- **Missing company data** → fallback values, simplified message format
- **Chart URL failures** → text-only Telegram message

---

**📝 STATUS:** ✅ COMPLETE - детальная спецификация с Telegraph + Telegram integration  
**🔄 NEXT:** [Block 5: State Management & Completion →](block-5-state-management.md)