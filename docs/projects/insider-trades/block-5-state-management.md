# Block 5: State Management & Completion (Узлы 24-25)

**🎯 НАЗНАЧЕНИЕ БЛОКА:** Финализация цикла workflow - перевод статусов карточек New/Renew → Old, установка posted_at timestamps, завершение 60-минутного цикла

**🔗 NAVIGATION:** [← Block 4](block-4-content-publishing.md) | [Architecture Overview](../architecture.md) | **FINAL BLOCK**

---

## Узел 24: MongoDB (Card Status Finalization)
**Тип:** `nodes-base.mongoDb` (v1.2)  
**📍 НАЗНАЧЕНИЕ:** Bulk update карточек New/Renew → Old статус для завершения publishing cycle  
**🔧 СТАТУС КОДА:** TEMPLATE - bulk status update с explicit credential

```json
{
  "authentication": "predefinedCredentialType",
  "nodeCredentialType": "mongoDb",
  "resource": "document",
  "operation": "updateMany",
  "collection": "deals",
  "query": "{{ JSON.stringify({ trade_status: { $in: ['New', 'Renew'] } }) }}",
  "updateDocument": "{{ JSON.stringify({\n  $set: {\n    trade_status: 'Old',\n    posted_at: new Date().toISOString(),\n    updated_at: new Date().toISOString(),\n    cycle_completed: true\n  }\n}) }}",
  "options": {
    "upsert": false
  }
}
```
**💡 ПОЯСНЕНИЕ:**
- **Credential:** `nodeCredentialType: "mongoDb"` - использует MongoDB credential (ID: Jb779SAaphmHAOGs)
- **Operation:** updateMany для batch обновления всех active карточек
- **Filter:** `trade_status: { $in: ['New', 'Renew'] }` - все cards готовые к finalization
- **Status transition:** New/Renew → Old (published state)

---

## Узел 25: Code (Cycle Completion & Statistics)
**Тип:** `nodes-base.code` (v2)  
**📍 НАЗНАЧЕНИЕ:** Финализация workflow цикла - completion logging, statistics calculation, next cycle preparation  
**🔧 СТАТУС КОДА:** TEMPLATE - comprehensive cycle completion с performance metrics

[JavaScript код остается без изменений - comprehensive cycle completion logic]

**💡 ПОЯСНЕНИЕ:**
- **No credentials required** - pure JavaScript processing node
- **Focus on card finalization:** Primary responsibility перевод статусов карточек
- **Statistics calculation:** Performance metrics для monitoring workflow health

---

## 📋 Block Connections (UPDATED):
```
Block 4 [Done] → 24 (Card Status Finalization) → 25 (Cycle Completion) → [WORKFLOW END]
```

## 🔐 Required Credentials:

**See:** [credentials-reference.md](credentials-reference.md) for exact credential IDs and usage patterns.

| Node | Credential Type | Credential Name | ID Reference |
|------|----------------|-----------------|--------------|
| **Узел 24 (MongoDB Update)** | `mongoDb` | MongoDB account | `Jb779SAaphmHAOGs` |
| **Узел 25** | _No credentials_ | N/A | N/A |

**💡 Credential Usage:**
- **MongoDB credential** handles connection, authentication, database access for bulk updates
- **Cycle completion logic** uses pure JavaScript processing without external credentials

---

## 🎯 Cycle Completion Checklist:

### ✅ Data Finalization:
- [ ] **Card statuses finalized** - все New/Renew → Old transitions
- [ ] **Timestamps set** - posted_at для tracking публикации
- [ ] **Cycle metadata** - cycle_id, duration, statistics logged
- [ ] **Publishing confirmation** - surveys уже updated с individual Telegraph URLs в Block 4

### ✅ Business Logic Compliance:
- [ ] **Status model integrity** - статусные переходы согласно архитектуре
- [ ] **Publishing confirmation** - все опубликованные карточки marked как Old
- [ ] **Audit trail** - полная прослеживаемость операций цикла
- [ ] **Idempotency** - повторный запуск не нарушит data consistency

### **🔧 RED FLAG 3 ARCHITECTURAL CORRECTION:**
- ✅ **Telegraph URL assignment removed** - теперь handled в Block 4 individually
- ✅ **Focus on card lifecycle** - Block 5 responsibility четко defined
- ✅ **Data consistency maintained** - no more bulk telegraph_url overwrites

---

**📝 STATUS:** ✅ FIXED - explicit credential specification added  
**🔧 RED FLAG 4:** ✅ COMPLETED - All 27 nodes have explicit credential assignments  
**🏁 ACHIEVEMENT:** Complete credential standardization across всей архитектуры