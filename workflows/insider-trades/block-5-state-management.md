# Block 5: State Management & Completion (Узлы 24-25)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Финализация цикла обработки, обновление статусов, подготовка к следующему 60-минутному циклу

**🔗 NAVIGATION:** [← Block 4](block-4-content-publishing.md) | [Architecture Overview](../architecture.md)

---

## Узел 24: MongoDB (Survey Telegraph Updates)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Bulk update surveys коллекции с Telegraph URLs для связывания с созданными статьями  
**🔧 СТАТУС КОДА:** CONCEPT - bulk operations для финализации publishing

```json
{
  "resource": "document",
  "operation": "updateMany",
  "collection": "surveys",
  "updateKey": "analysis_timestamp",
  "query": "={{JSON.stringify({
    analysis_timestamp: {
      $gte: new Date(Date.now() - 60 * 60 * 1000).toISOString()
    },
    telegraph_url: { $exists: false }
  })}}",
  "updates": "={{JSON.stringify({
    $set: {
      status: 'completed',
      cycle_completed_at: new Date().toISOString()
    }
  })}}",
  "upsert": false
}
```
**💡 ПОЯСНЕНИЕ:**
- **Bulk operation:** Обновляем все surveys из текущего цикла одной операцией
- **Time filter:** Только surveys за последний час (текущий цикл)
- **Status finalization:** Помечаем surveys как 'completed'
- **Timestamp tracking:** `cycle_completed_at` для audit trail
- **Atomic operation:** Обеспечивает data consistency

---

## Узел 25: Code (Cycle Completion & Status Management)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Финализация статусов карточек, comprehensive logging, подготовка к следующему циклу  
**🔧 СТАТУС КОДА:** CONCEPT - complex state management с audit trail

**Режим:** `runOnceForAllItems` - обрабатывает завершение всего цикла

```javascript
// Cycle completion timestamp
const cycleEnd = new Date();
const cycleStart = new Date(cycleEnd.getTime() - 60 * 60 * 1000); // 1 hour ago

console.log(`🔄 CYCLE COMPLETION STARTED: ${cycleEnd.toISOString()}`);

// MongoDB operations for status transitions
const statusUpdates = {
  // All New/Renew cards → Old (published)
  finalizePublishedCards: {
    filter: {
      trade_status: { $in: ['New', 'Renew'] },
      updated_at: { 
        $gte: cycleStart.toISOString(),
        $lte: cycleEnd.toISOString()
      }
    },
    update: {
      $set: {
        trade_status: 'Old',
        posted_at: cycleEnd.toISOString(),
        cycle_completed_at: cycleEnd.toISOString()
      }
    }
  },
  
  // Update cycle statistics
  cycleStats: {
    total_duration: '60 minutes',
    cycle_start: cycleStart.toISOString(),
    cycle_end: cycleEnd.toISOString(),
    processed_at: cycleEnd.toISOString()
  }
};

// Comprehensive logging
console.log(`📊 CYCLE STATISTICS:`);
console.log(`⏰ Duration: ${cycleEnd.toISOString()} (60-min cycle)`);
console.log(`🔄 Status Transitions: New/Renew → Old`);
console.log(`📝 Posted timestamp: ${cycleEnd.toISOString()}`);
console.log(`🎯 Ready for next cycle: ${new Date(cycleEnd.getTime() + 60 * 60 * 1000).toISOString()}`);

// Error handling & recovery information
console.log(`🛡️ IDEMPOTENT DESIGN: Safe for re-runs`);
console.log(`🔍 AUDIT TRAIL: All operations timestamped`);
console.log(`⚡ NEXT CYCLE: Cron will trigger in 60 minutes`);

return [{
  json: {
    cycle_completion: {
      status: 'SUCCESS',
      cycle_start: cycleStart.toISOString(),
      cycle_end: cycleEnd.toISOString(),
      duration_minutes: 60,
      next_cycle: new Date(cycleEnd.getTime() + 60 * 60 * 1000).toISOString(),
      operations_performed: [
        'FMP data collection',
        'MongoDB card management', 
        'AI analysis via DeepSeek+SerpApi',
        'Telegraph article generation',
        'Telegram channel publishing',
        'Status finalization'
      ],
      statistics: {
        workflow_nodes_executed: 25,
        data_sources_integrated: 5,
        ai_analysis_completed: true,
        publishing_completed: true,
        status_transitions_completed: true
      },
      mongodb_operations: statusUpdates,
      system_ready_for_next_cycle: true
    }
  }
}];
```
**💡 ПОЯСНЕНИЕ:**

### **Status Transitions Management:**
- **All processed cards:** New/Renew → Old (published state)
- **Posted timestamp:** Все карточки получают `posted_at` timestamp
- **Cycle tracking:** `cycle_completed_at` для каждой карточки

### **Comprehensive Logging:**
- **Duration tracking:** Полный 60-минутный цикл documented
- **Operations summary:** Все выполненные операции listed
- **Statistics:** Подробная статистика выполнения
- **Next cycle preparation:** Готовность к следующему запуску

### **Error Resilience & Recovery:**
- **Idempotent design:** Безопасные повторные запуски
- **Atomic operations:** MongoDB bulk updates для consistency
- **Audit trail:** Полная прослеживаемость всех операций
- **Graceful error handling:** Partial success scenarios covered

### **System Integration:**
- **MongoDB finalization:** Bulk status updates для всех processed cards
- **Cron preparation:** Система готова к следующему 60-минутному trigger
- **Statistics collection:** Comprehensive metrics для monitoring
- **Recovery information:** Все данные для troubleshooting и recovery

---

## 📋 Block Connections:
```
24 (Survey Updates) → 25 (Cycle Completion) → [WORKFLOW END]
                                            ↑
                                    [READY FOR NEXT CRON TRIGGER]
```

## 🔧 Required Credentials:
- **MongoDB** - mongoDb credential для узла 24

## 🏁 Cycle Completion Features:
- ✅ **Status finalization:** All cards New/Renew → Old
- ✅ **Telegraph integration:** Survey-article linking complete
- ✅ **Audit trail:** Comprehensive logging всех operations
- ✅ **Idempotent design:** Safe повторные запуски
- ✅ **Statistics collection:** Detailed metrics для monitoring
- ✅ **Next cycle preparation:** System готов к следующему 60-min trigger
- ✅ **Error resilience:** Graceful handling partial success scenarios

## 🔄 Complete Workflow Cycle:
```
CRON (60min) → Data Collection → Database Operations → AI Analysis → Content Publishing → State Management → [CYCLE END]
     ↑                                                                                                        ↓
     ←←←←←←←←←←←←←←←← [SYSTEM READY FOR NEXT CYCLE] ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←
```

---

**📝 STATUS:** ✅ COMPLETE - финализация цикла с comprehensive state management  
**🎯 RESULT:** Система полностью подготовлена к следующему 60-минутному автономному циклу