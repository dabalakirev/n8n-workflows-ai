# AI Agent Execution Protocol

## 🚨 **MANDATORY PROTOCOL - NO EXCEPTIONS**

### **⚠️ ПЕРЕД КАЖДЫМ ОТВЕТОМ AI Agent ОБЯЗАН:**

1. **✅ Заявить текущую Phase:** `"Phase 1: Planning"`
2. **✅ Выполнить Context Awareness Check** (даже для "простых" задач)
3. **✅ Никогда не пропускать phases**
4. **✅ НЕТ exceptions** для "quick fixes"

### **🔍 Pre-Response Checklist:**
- [ ] Проверил existing docs/files по теме?
- [ ] Начинаю с "Phase 1: Planning"?
- [ ] Следую 5-step execution flow?
- [ ] Проанализировал context перед solutions?

### **🚩 Warning Signs Protocol Violation:**
- ❌ Начинать с "I suggest..." без Planning phase
- ❌ Не проверять документацию/files
- ❌ Спешить к solutions без context analysis
- ❌ Думать "слишком просто для full protocol"

---

## 🔄 Core Execution Flow: **"Plan → Propose → Get Approval → Execute → Document"**

---

## 1. 📋 Planning

**🎯 Цель:** Понять задание и определить scope работ

### **🔍 MANDATORY Context Awareness Check:**
**ВСЕГДА выполнять (включая "простые" задачи):**
- ✅ **Проверить existing documentation/files** связанные с задачей
- ✅ **Новые комментарии к Issues**
- ✅ **Recent GitHub Actions результаты**
- ✅ **Updates в зависимых задачах**

### **Дополнительные действия:**
- **Analyze Assignment** - понять требования
- **Identify Key Actions** - определить основные действия
- **Determine Documentation Impact** - какие docs обновить
- **Assess Issues Impact** - создание/обновление/закрытие Issues

**Результат:** Понимание полного scope с актуальным контекстом

---

## 2. 💬 Propose

**🎯 Цель:** Получить одобрение плана

**Структура предложения:**
```
## 🎯 Предложение по выполнению [Задание]

### Ключевые действия:
- [ ] Action 1 - описание
- [ ] Action 2 - описание

### Документация:
- [ ] Обновить [документ] - причина
- [ ] Создать [документ] - обоснование

### Issues Management:
- [ ] Создать Issue [тип]
- [ ] Обновить Issue #N
- [ ] Закрыть Issue #N

**Готов выполнить после одобрения.**
```

**Результат:** Одобренный план выполнения

---

## 3. ✅ Get Approval

**🎯 Цель:** Убедиться что план корректный

**Ждем явного одобрения:**
- ✅ "Одобряю" / "Да" / "Приступай"
- ❌ НЕ начинаем без одобрения

**Результат:** Четкое разрешение на выполнение

---

## 4. 🚀 Execute

**🎯 Цель:** Выполнить одобренный план

**Во время выполнения:**
- **Follow approved plan** - строго по плану
- **Notify on completion** - уведомлять о завершении этапов
- **Handle unexpected issues** - уведомлять о проблемах

**Результат:** Выполненное задание согласно плану

---

## 5. 📚 Document

**🎯 Цель:** Обеспечить командную осведомленность

### **Обязательные командные действия:**

#### **🎫 Issues Management**
- **Create/Update/Close Issues** для задач/багов/документации

#### **📚 Documentation Updates**
- **Update existing docs** при изменениях функциональности
- **Create new documentation** для новых features/процессов

#### **🔗 System Integration** - MANDATORY для каждого документа:
- **Update README.md** - добавить в navigation
- **Add protocol references** - обновить relevant protocols
- **Create discovery paths** - ensure future AI agents найдут документ
- **Verify navigation** - проверить accessibility

#### **💬 Progress Communication**
- **Status updates** в Issue комментариях
- **Results summary** - итоговые результаты
- **Lessons learned** - важные findings

### **🎯 Integration Checklist при создании документа:**
- [ ] **README.md updated** с новой документацией?
- [ ] **Navigation paths** созданы?
- [ ] **Related protocols** updated с references?
- [ ] **Future AI agent** сможет найти документ?

**Результат:** Полная transparency с guaranteed discoverability

---

## 🛡️ Action Types

| Action Type | When | Example |
|------------|------|---------|
| **Context Awareness** | **ВСЕГДА в Planning** | **Check docs, recent changes** |
| **Issues Management** | Always | Create/Update/Close Issues |
| **Documentation** | При функциональных изменениях | Update guides, specs |
| **System Integration** | **ВСЕГДА при создании docs** | **README updates, links** |
| **Progress Communication** | Always | Comment статус в Issues |

### **✅ MUST be planned:**
- **Context awareness activities**
- Командные коммуникации
- Документальные изменения
- **System integration requirements**
- Issues lifecycle management

---

## 🎯 Success Criteria

**✅ Задание выполнено когда:**
- ✅ **Context проверен и актуален**
- ✅ Все planned actions завершены
- ✅ Issues обновлены/закрыты
- ✅ Документация актуализирована
- ✅ **README.md updated с новой документацией**
- ✅ **System integration completed**
- ✅ Команда informative о результатах

**❌ Задание НЕ завершено если:**
- ❌ **Context не проверен**
- ❌ **Новые документы изолированы**
- ❌ Issues без обновления
- ❌ Нет communication о результатах

---

## 🔄 Integration с Project Protocols

- **AI Agent Roles Protocol** - определяет роли, этот протокол - execution process
- **GitHub Issues Protocol** - обеспечивает Issues management
- **Context Handoff Protocol** - этот протокол создает context для handoff

### **При смене AI agents:**
- Current agent завершает Document phase (INCLUDING system integration)
- New agent начинает с Planning phase (INCLUDING context awareness)

---

## 🚨 Critical Requirements

### **For Documentation Creation:**
**NEVER create isolated documents.** Every document MUST have:
- **README.md entry** for navigation
- **Protocol references** где relevant
- **Discovery paths** for future AI agents

### **Integration Questions:**
1. **Context:** "Что изменилось с последнего обновления?"
2. **Discovery:** "Как future AI agent найдет документацию?"
3. **Navigation:** "Где создать links?"

### **Enforcement:**
- **Context awareness НЕ optional** - обязательно в Planning
- **Documentation НЕ complete** пока document isolated

---

## 📚 **Protocol Discipline**

### **🎯 Key Mindset:**
- **Protocol = Discipline, не Guideline**
- **NO shortcuts** даже для "obvious" tasks
- **Context First, Solutions Second ALWAYS**

### **🚫 Avoid:**
- "Too simple for full protocol"
- "Skip Context Awareness, it's obvious"
- "Rush to solution без planning"

### **✅ Proper Mindset:**
- "Even simple tasks benefit от systematic approach"
- "Context Awareness reveals unexpected information"
- "Protocol compliance builds team trust"

---

**Key Principle:** **"Context First, Solutions Second"** - даже для obvious задач, Context Awareness Check предотвращает ошибки и duplicate work.

*Protocol applies to ALL AI agent activities - NO EXCEPTIONS.*