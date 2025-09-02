# Block 1: Data Collection & Filtering (Узлы 1-4)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Получение инсайдерских сделок от FMP API, строгая фильтрация согласно Level 2 требованиям, early exit при пустых результатах

**🔗 NAVIGATION:** [← Architecture Overview](../architecture.md) | [Next: Block 2 →](block-2-database-operations.md)

---

## Узел 1: Cron Trigger
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

## Узел 2: HTTP Request (FMP API)
**Тип:** `nodes-base.httpRequest` (v4.2)  
**📍 НАЗНАЧЕНИЕ:** Получение последних 500 инсайдерских сделок от FMP Latest Insider Trading API  
**🔧 СТАТУС КОДА:** TEMPLATE - ready configuration с explicit credential selection

```json
{
  "method": "GET",
  "url": "https://financialmodelingprep.com/stable/insider-trading/latest",
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "httpQueryAuth",
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
  }
}
```
**💡 ПОЯСНЕНИЕ:** 
- **Credential:** `nodeCredentialType: "httpQueryAuth"` - использует FMP API credential (ID: k887gSxTZZEgRYIa)
- `limit: 500` - максимальная выборка согласно Level 2 ограничениям
- `timeout: 30000` - 30 секунд для внешнего API call
- `neverError: false` - позволяет workflow остановиться при API failures

---

## Узел 3: Code (Data Filtering)
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
- **No credentials required** - pure JavaScript processing node
- **Фильтр 1:** `transactionType === "P-Purchase"` - только покупки инсайдеров
- **Фильтр 2:** `securityName` проверка против whitelist - исключает опционы/варранты
- **Фильтр 3:** Валидация required fields - предотвращает обработку неполных данных

---

## Узел 4: If (Early Exit)
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
- **No credentials required** - logic node
- **Condition:** `array.length > 0` - проверяет наличие отфильтрованных сделок
- **TRUE path** → Block 2 (продолжение обработки)
- **FALSE path** → Workflow end (экономия ресурсов при пустых результатах)

---

## 📋 Block Connections:
```
1 (Cron) → 2 (FMP API) → 3 (Filtering) → 4 (Early Exit)
                                            ↑[TRUE] → Block 2
                                            ↑[FALSE] → END
```

## 🔐 Required Credentials:

**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage patterns.

| Node | Credential Type | Credential Name | ID Reference |
|------|----------------|-----------------|--------------|
| **Узел 2 (FMP API)** | `httpQueryAuth` | FMP API | `k887gSxTZZEgRYIa` |
| **Узел 1,3,4** | _No credentials_ | N/A | N/A |

**💡 Credential Usage:**
- **FMP API credential** automatically injects API key via query parameter
- **Узел 2** uses predefined credential approach: `"nodeCredentialType": "httpQueryAuth"`

---

**📝 STATUS:** ✅ COMPLETE - explicit credential specification added  
**🔧 RED FLAG 4:** ✅ PROGRESS - Block 1 credential selection standardized  
**🔄 NEXT:** [Block 2: Database Operations & Card Management →](block-2-database-operations.md)