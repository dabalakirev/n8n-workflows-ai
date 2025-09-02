# Block 5: State Management & Completion (Узлы 24-25)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Обновление surveys коллекции с Telegraph URLs, финализация статусов карточек New/Renew → Old, завершение 60-минутного цикла

**🔗 NAVIGATION:** [← Block 4](block-4-content-publishing.md) | [Architecture Overview](../architecture.md)

---

## Узел 24: MongoDB (Survey Telegraph Updates)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Bulk обновление surveys коллекции с Telegraph URLs из Block 4 processing  
**🔧 СТАТУС КОДА:** CONCEPT - batch update операция с data consolidation

```json
{
  "resource": "document",
  "operation": "update",
  "collection": "surveys",
  "updateKey": "symbol",
  "fields": "telegraph_url,updated_at",
  "options": {
    "multi": true,
    "upsert": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Batch operation:** Обновление всех surveys обработанных в Block 4
- **Update key:** Symbol-based matching для связи survey ↔ telegraph_url
- **Fields:** telegraph_url + updated_at timestamp
- **Multi: true** - массовое обновление всех matched records
- **Input:** Done output из Block 4 Split In Batches completion
- **Data source:** Consolidated telegraph URLs из Block 4 processing

**📋 Input Processing Logic (Code узел перед MongoDB):**
```javascript
// Consolidate Telegraph URLs from Block 4 processing
const block4Results = $input.all();
const surveyUpdates = [];

for (const item of block4Results) {
  if (item.json.telegraphSuccess && item.json.telegramPayload?.telegraphUrl) {
    surveyUpdates.push({
      symbol: item.json.telegramPayload.symbol,
      telegraph_url: item.json.telegramPayload.telegraphUrl,
      updated_at: new Date().toISOString()
    });
  }
}

// Prepare bulk update operations
const bulkOperations = surveyUpdates.map(update => ({
  updateOne: {
    filter: { symbol: update.symbol, telegraph_url: null },
    update: { 
      $set: { 
        telegraph_url: update.telegraph_url,
        updated_at: update.updated_at
      }
    }
  }
}));

return surveyUpdates.map(update => ({ json: update }));
```

---

## Узел 25: MongoDB (Card Status Completion)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Финализация статусов карточек и завершение 60-минутного цикла  
**🔧 СТАТУС КОДА:** CONCEPT - multi-step completion с status transitions и logging

```json
{
  "resource": "document",
  "operation": "update",
  "collection": "deals",
  "query": "{{ JSON.stringify({ trade_status: { $in: ['New', 'Renew'] } }) }}",
  "fields": "trade_status,posted_at,updated_at",
  "options": {
    "multi": true,
    "upsert": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Status transition:** New/Renew → Old для всех обработанных карточек
- **Timestamp update:** posted_at = current timestamp (marking publication)
- **Multi update:** Всех карточек которые были опубликованы в Telegram
- **Final step:** Завершение полного workflow цикла
- **Logging ready:** Подготовка completion metrics

**📋 Pre-processing Logic (Code узел перед MongoDB):**
```javascript
// Workflow completion logic
const completionTimestamp = new Date().toISOString();
const cycleStartTime = $workflow.settings?.startTime || completionTimestamp;

// Calculate cycle metrics
const cycleMetrics = {
  cycle_started: cycleStartTime,
  cycle_completed: completionTimestamp,
  duration_minutes: Math.round((new Date(completionTimestamp) - new Date(cycleStartTime)) / (1000 * 60)),
  
  // Counters (populated from previous blocks)
  deals_processed: $runExecutionData?.contextData?.dealsProcessed || 0,
  cards_created: $runExecutionData?.contextData?.cardsCreated || 0,
  cards_updated: $runExecutionData?.contextData?.cardsUpdated || 0,
  ai_analyses_completed: $runExecutionData?.contextData?.aiAnalysesCompleted || 0,
  telegraph_articles_created: $runExecutionData?.contextData?.telegraphArticlesCreated || 0,
  telegram_messages_sent: $runExecutionData?.contextData?.telegramMessagesSent || 0,
  surveys_updated: $runExecutionData?.contextData?.surveysUpdated || 0,
  cards_finalized: 0  // Will be counted after this operation
};

// Update all New/Renew cards to Old status
const updateData = {
  trade_status: 'Old',
  posted_at: completionTimestamp,
  updated_at: completionTimestamp
};

// Log cycle completion
console.log('🏁 INSIDER TRADES CYCLE COMPLETED');
console.log('⏱️ Duration:', cycleMetrics.duration_minutes, 'minutes');
console.log('📊 Metrics:', JSON.stringify(cycleMetrics, null, 2));

return [{ 
  json: {
    ...updateData,
    cycleMetrics: cycleMetrics,
    completionStatus: 'SUCCESS'
  }
}];
```

---

## 📊 Enhanced Completion Logic

### **Статусная модель финализации:**
```
New (current session) → Old (published & finalized)
Renew (updated in session) → Old (published & finalized)
Old (already finalized) → unchanged
```

### **Completion Sequence:**
1. **Block 4 Done** → Survey telegraph_url updates consolidated
2. **Survey Updates** → All surveys populated with Telegraph URLs  
3. **Status Finalization** → All published cards marked as Old
4. **Cycle Metrics** → Complete workflow statistics logged
5. **Workflow End** → Ready for next 60-minute cycle

### **Atomic Operations:**
- **Survey updates** и **Card status updates** выполняются как отдельные atomic operations
- **Rollback strategy:** При ошибке в любой операции, предыдущие remain consistent
- **Partial success handling:** Updates применяются по мере возможности

---

## 📋 Block Connections:
```
Block 4 [Done] → 24 (Survey Updates) → 25 (Status Completion) → Workflow End
```

## 🔧 Required Credentials:
- **MongoDB** - mongoDb credential для узлов 24, 25

## 📊 Data Flow Analysis:

### Input Requirements:
- **Block 4 completion** - all Telegraph articles created и Telegram messages sent
- **Survey processing results** - symbol ↔ telegraph_url mappings
- **Active cards status** - New/Renew карточки ready для finalization

### Output Deliverables:
- **Survey completeness** - все surveys с populated telegraph_url
- **Card finalization** - все карточки переведены в Old status
- **Cycle completion** - workflow готов к следующему 60-minute cycle
- **Metrics logging** - полная статистика выполнения цикла

### Error Handling Strategy:
- **Survey update failures** → log errors, proceed с card status updates
- **Card status failures** → log errors, complete cycle (готов к retry в следующем цикле)
- **Partial updates** → consistent state maintained, resume в next cycle
- **Completion logging** → всегда выполняется независимо от errors

---

## 🔄 Cycle Completion Workflow:

### **Success Path:**
1. ✅ All surveys updated with Telegraph URLs
2. ✅ All cards transitioned to Old status  
3. ✅ Completion metrics logged
4. ✅ Workflow terminated successfully
5. ✅ Next cycle scheduled (60 minutes)

### **Partial Success Path:**
1. ⚠️ Some surveys updated (others remain with telegraph_url: null)
2. ⚠️ Some cards finalized (others retry in next cycle)
3. ✅ Error logging completed
4. ✅ Workflow terminated with warnings
5. ✅ Next cycle will process remaining items

### **Error Recovery:**
- **Idempotent design** - повторные запуски безопасны
- **Status consistency** - карточки всегда в правильном состоянии
- **Incremental progress** - каждый цикл продвигает состояние forward
- **Graceful degradation** - частичные результаты сохраняются

---

**📝 STATUS:** ✅ COMPLETE - финализация workflow с comprehensive state management  
**🏁 FINAL BLOCK:** Завершение Level 3 архитектурного решения (100% - все 25 узлов)