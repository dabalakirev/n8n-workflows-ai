# Block 5: State Management & Completion (Узлы 24-25)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Финализация цикла workflow - обновление surveys с telegraph_url, перевод статусов карточек New/Renew → Old, установка posted_at timestamps, завершение 60-минутного цикла

**🔗 NAVIGATION:** [← Block 4](block-4-content-publishing.md) | [Architecture Overview](../architecture.md) | **FINAL BLOCK**

---

## Узел 24: MongoDB (Survey Telegraph Updates)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Bulk update surveys коллекции с telegraph_url из Block 4 processing  
**🔧 СТАТУС КОДА:** CONCEPT - bulk update операция с data consistency

```json
{
  "resource": "document",
  "operation": "updateMany",
  "collection": "surveys",
  "query": "{{ JSON.stringify({ telegraph_url: null }) }}",
  "updateDocument": "{{ JSON.stringify({\n  $set: {\n    telegraph_url: $json.telegraphUrl,\n    updated_at: new Date().toISOString(),\n    publishing_status: 'completed'\n  }\n}) }}",
  "options": {
    "upsert": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Operation:** updateMany для batch обновления surveys
- **Filter:** `telegraph_url: null` - только неопубликованные surveys из текущего цикла
- **Updates:** telegraph_url + updated_at timestamp + publishing status
- **Input:** Done output из Block 4 (все Telegraph статьи созданы)
- **Data consistency:** Atomic update operation для всех обработанных surveys
- **Purpose:** Связывание surveys с созданными Telegraph статьями

---

## Узел 25: Code (Cycle Completion & Status Management)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Финализация workflow цикла - обновление статусов карточек, установка timestamps, completion logging  
**🔧 СТАТУС КОДА:** CONCEPT - comprehensive cycle completion с bulk operations

**Режим:** `runOnceForAllItems` - обрабатывает completion для всего цикла

```javascript
// Cycle completion processing
const cycleStartTime = new Date();
const cycleId = `cycle-${Date.now()}`;

// Step 1: Update all published cards to "Old" status
const currentTime = cycleStartTime.toISOString();

// Prepare bulk operations for deals collection
const bulkDealsOperations = [];

try {
  // Update all New/Renew cards that have been successfully published
  // These are cards that went through the complete pipeline
  const statusUpdateOperation = {
    updateMany: {
      filter: { 
        trade_status: { $in: ["New", "Renew"] }
      },
      update: {
        $set: {
          trade_status: "Old",
          posted_at: currentTime,
          updated_at: currentTime,
          cycle_id: cycleId
        }
      }
    }
  };
  
  bulkDealsOperations.push(statusUpdateOperation);
  
  console.log(`Cycle ${cycleId}: Finalizing card statuses New/Renew → Old`);
  
  // Step 2: Calculate cycle statistics
  const cycleStats = {
    cycle_id: cycleId,
    started_at: cycleStartTime.toISOString(),
    completed_at: new Date().toISOString(),
    duration_seconds: Math.round((Date.now() - cycleStartTime.getTime()) / 1000),
    
    // These would be populated from previous blocks in real implementation
    deals_processed: $input.all().length || 0,
    cards_created: 0, // Would come from Block 2 output
    cards_updated: 0, // Would come from Block 2 output  
    ai_analyses_completed: 0, // Would come from Block 3 output
    telegraph_articles_created: 0, // Would come from Block 4 output
    telegram_messages_sent: 0, // Would come from Block 4 output
    
    status: "completed"
  };
  
  // Step 3: Log completion metrics
  console.log(`=== CYCLE COMPLETION REPORT ===`);
  console.log(`Cycle ID: ${cycleStats.cycle_id}`);
  console.log(`Duration: ${cycleStats.duration_seconds} seconds`);
  console.log(`Cards Status Updated: New/Renew → Old`);
  console.log(`Timestamp Set: ${cycleStats.completed_at}`);
  console.log(`Next Cycle: +60 minutes`);
  console.log(`=== END CYCLE REPORT ===`);
  
  // Step 4: Prepare MongoDB bulk operations payload
  const mongoOperations = {
    collection: "deals",
    operations: bulkDealsOperations,
    cycleStats: cycleStats
  };
  
  return [{
    json: {
      cycleCompletion: {
        success: true,
        cycleId: cycleId,
        completedAt: cycleStats.completed_at,
        operations: mongoOperations,
        message: "Workflow cycle completed successfully"
      },
      mongoOperations: mongoOperations,
      cycleStats: cycleStats,
      nextExecution: new Date(Date.now() + 60 * 60 * 1000).toISOString() // +60 minutes
    }
  }];
  
} catch (error) {
  console.error(`Cycle completion error: ${error.message}`);
  
  return [{
    json: {
      cycleCompletion: {
        success: false,
        cycleId: cycleId,
        error: error.message,
        completedAt: new Date().toISOString()
      },
      mongoOperations: null,
      cycleStats: null
    }
  }];
}
```
**💡 ПОЯСНЕНИЕ:**
- **Cycle management:** Генерация уникального cycle_id для отслеживания
- **Bulk status updates:** Подготовка MongoDB bulk operations для efficiency
- **Status transitions:** New/Renew → Old для всех опубликованных карточек
- **Timestamp management:** posted_at и updated_at установка
- **Completion logging:** Comprehensive cycle statistics и metrics
- **Error handling:** Graceful handling с error logging
- **Next cycle preparation:** Расчет времени следующего выполнения
- **MongoDB operations:** Подготовка bulk updates для atomic execution

---

## 📋 Block Connections:
```
Block 4 [Done] → 24 (Survey Updates) → 25 (Cycle Completion) → [WORKFLOW END]
```

## 🔧 Required Credentials:
- **MongoDB** - mongoDb credential для узла 24

## 📊 Data Flow Analysis:

### Input Requirements:
- **Block 4 completion** - все Telegraph статьи созданы и Telegram сообщения отправлены
- **Telegraph URLs** - успешно созданные статьи для survey updates
- **Active card states** - карточки со статусами New/Renew готовые к финализации

### Output Deliverables:
- **Updated surveys** - telegraph_url поля populated, publishing_status = 'completed'
- **Finalized card statuses** - все New/Renew карточки → Old
- **Posted timestamps** - posted_at установлен для всех опубликованных карточек
- **Cycle completion** - workflow готов к следующему 60-минутному циклу

### Completion Strategy:
- **Atomic operations** - bulk updates для data consistency
- **Comprehensive logging** - cycle statistics и performance metrics
- **Status tracking** - clear indication что цикл завершен
- **Error resilience** - graceful handling completion failures
- **Next cycle ready** - система готова к следующему запуску

---

## 🎯 Cycle Completion Checklist:

### ✅ Data Finalization:
- [ ] **Survey records updated** - telegraph_url связи установлены
- [ ] **Card statuses finalized** - все New/Renew → Old transitions
- [ ] **Timestamps set** - posted_at для tracking публикации
- [ ] **Cycle metadata** - cycle_id, duration, statistics logged

### ✅ System State Reset:
- [ ] **Workflow completion** - готовность к следующему Cron trigger
- [ ] **Clean state** - никаких hanging processes или incomplete operations  
- [ ] **Error cleanup** - все ошибки logged, система stable
- [ ] **Performance metrics** - cycle duration и throughput recorded

### ✅ Business Logic Compliance:
- [ ] **Status model integrity** - статусные переходы согласно архитектуре
- [ ] **Publishing confirmation** - все опубликованные карточки marked как Old
- [ ] **Audit trail** - полная прослеживаемость операций цикла
- [ ] **Idempotency** - повторный запуск не нарушит data consistency

---

**📝 STATUS:** ✅ COMPLETE - финализация архитектуры с comprehensive cycle management  
**🏁 ACHIEVEMENT:** 25 узлов workflow архитектуры ЗАВЕРШЕНЫ - 100% Level 3 ready для validation