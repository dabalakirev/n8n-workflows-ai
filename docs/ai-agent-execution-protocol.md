# AI Agent Execution Protocol

## 🎯 Overview

Этот протокол определяет обязательную последовательность действий для AI агента при выполнении любого задания в проекте. Фокус на командной работе и документальном сопровождении.

---

## 🔄 Core Execution Flow

### **"Plan → Propose → Get Approval → Execute → Document"**

Каждое задание проходит через эти 5 этапов без исключений.

---

## 1. 📋 Planning (Планирование)

### **🎯 Цель:** Понять задание и определить scope работ

**Обязательные действия:**
- **Analyze Assignment** - понять что требуется сделать
- **Identify Key Actions** - определить основные действия для выполнения
- **Determine Documentation Impact** - какая документация потребует обновления
- **Assess Issues Impact** - какие Issues будут затронуты (создание/обновление/закрытие)

**Результат:** Понимание полного scope задания

---

## 2. 💬 Propose (Предложение)

### **🎯 Цель:** Получить одобрение плана перед выполнением

**Структура предложения:**
```
## 🎯 Предложение по выполнению [Задание]

### Ключевые действия:
- [ ] Action 1 - описание
- [ ] Action 2 - описание
- [ ] Action N - описание

### Документация:
- [ ] Обновить [документ] - причина
- [ ] Создать [документ] - обоснование

### Issues Management:
- [ ] Создать Issue [тип] - для чего
- [ ] Обновить Issue #N - статус/прогресс  
- [ ] Закрыть Issue #N - критерии выполнения

**Готов выполнить после одобрения.**
```

**Результат:** Одобренный план выполнения

---

## 3. ✅ Get Approval (Получение одобрения)

### **🎯 Цель:** Убедиться что план корректный

**Ждем явного одобрения:**
- ✅ "Одобряю" / "Да" / "Приступай"
- ✅ Уточнения и корректировки плана
- ❌ НЕ начинаем выполнение без одобрения

**Результат:** Четкое разрешение на выполнение

---

## 4. 🚀 Execute (Выполнение)

### **🎯 Цель:** Выполнить одобренный план

**Во время выполнения:**
- **Follow approved plan** - строго по одобренному плану
- **Notify on completion** - уведомлять о завершении ключевых этапов
- **Handle unexpected issues** - уведомлять о неожиданных проблемах

**Результат:** Выполненное задание согласно плану

---

## 5. 📚 Document (Документирование) - ENHANCED

### **🎯 Цель:** Обеспечить командную осведомленность и сохранность знаний

**Обязательные виды командных действий:**

#### **🎫 Issues Management**
- **Create Issues** - для новых задач/багов/документации
- **Update Issues** - комментарии о прогрессе и результатах
- **Close Issues** - при полном выполнении всех критериев

#### **📚 Documentation Updates**
- **Update existing docs** - при изменениях в функциональности
- **Create new documentation** - для новых features/процессов
- **Cross-reference updates** - поддерживать связи между документами

#### **🔗 System Integration (NEW)**
**MANDATORY для КАЖДОГО созданного документа:**
- **Update README.md** - добавить новую документацию в navigation
- **Add protocol references** - обновить relevant AI protocols с links
- **Create discovery paths** - ensure future AI agents найдут документ
- **Verify navigation** - проверить что документ accessible через existing paths

#### **💬 Progress Communication**  
- **Status updates** - о ходе выполнения в Issue комментариях
- **Results summary** - итоговые результаты и deliverables
- **Lessons learned** - важные findings для будущих задач

#### **🎯 Integration Verification Checklist (NEW)**
**При создании ЛЮБОГО документа проверить:**
- [ ] **README.md updated** с новой документацией?
- [ ] **Navigation paths** созданы для discovery?
- [ ] **Related protocols** updated с references?
- [ ] **Future AI agent** сможет найти этот документ?
- [ ] **Testing discovery:** Can AI find this through existing protocols?

**Результат:** Полная командная transparency и документальное покрытие с guaranteed discoverability

---

## 🛡️ Mandatory Action Types

### **При каждом задании проверить необходимость:**

| Action Type | When Required | Example |
|------------|---------------|---------|
| **Issues Management** | Always | Create/Update/Close Issues |
| **Documentation** | When functionality changes | Update README, guides, specs |
| **System Integration** | **ALWAYS при создании docs** | **README updates, navigation links** |
| **Progress Communication** | Always | Comment in Issues about status |
| **Cross-references** | When structure changes | Update links, references |

### **❌ What NOT to over-plan:**
- Конкретные MCP операции
- Детали файловых операций  
- Технические implementation детали
- Промежуточные technical steps

### **✅ What MUST be planned:**
- Командные коммуникации
- Документальные изменения
- **System integration requirements (NEW)**
- Issues lifecycle management
- Knowledge sharing activities

---

## 🎯 Success Criteria - ENHANCED

**Задание считается выполненным когда:**
- ✅ Все planned actions завершены
- ✅ Соответствующие Issues обновлены/закрыты
- ✅ Документация актуализирована
- ✅ **README.md updated с новой документацией (NEW)**
- ✅ **Navigation paths созданы для discovery (NEW)**
- ✅ **System integration completed (NEW)**
- ✅ Команда informative о результатах

**Задание НЕ завершено если:**
- ❌ Issues остались без обновления
- ❌ Документация не отражает изменения
- ❌ **Новые документы изолированы и недоступны (NEW)**
- ❌ **README или protocols не обновлены (NEW)**
- ❌ Нет communication о результатах
- ❌ Broken cross-references в документации

---

## 💡 Protocol Examples

### **Example 1: Bug Fix Task**
```
Planning: Understand bug, identify fix approach, determine docs impact
Propose: Fix steps + Issue closure + documentation updates
Execute: Implement fix, test, document
Document: Close Issue, update troubleshooting docs, UPDATE README navigation, communicate fix
```

### **Example 2: New Feature Task**  
```
Planning: Feature requirements, design approach, documentation needs
Propose: Implementation plan + new Issues + comprehensive docs + system integration
Execute: Build feature, test, integrate
Document: Update Issues, create user guides, ADD TO README navigation, UPDATE protocols, announce feature
```

### **Example 3: Documentation Task** - ENHANCED
```
Planning: Documentation gaps, target audience, related Issues, WHERE TO INTEGRATE
Propose: Documentation structure + Issue updates + README updates + navigation integration
Execute: Write documentation, review, publish
Document: Close Issues, UPDATE README, ADD PROTOCOL REFERENCES, create navigation, TEST discovery paths
```

---

## 🔄 Integration with Project Protocols

### **Relationship to other protocols:**
- **AI Agent Roles Protocol** - определяет роли, этот протокол - execution process
- **GitHub Issues Protocol** - обеспечивает compliance с Issues management
- **Context Handoff Protocol** - этот протокол создает context для handoff
- **Backup Essentials** - должен быть referenced при major workflow changes
- **All documentation** - must be discoverable через README navigation

### **When switching between AI agents:**
- Current agent должен завершить Document phase (INCLUDING system integration)
- New agent начинает с Planning phase для новых задач
- Ongoing tasks передаются с current execution status
- All created documentation должно быть discoverable для new agent

---

## 🚨 Critical Integration Requirements

### **For Documentation Creation:**
**NEVER create isolated documents.** Every document MUST have:
- **README.md entry** for navigation
- **Protocol references** where relevant
- **Discovery paths** for future AI agents
- **Cross-links** from related documents

### **Integration Verification Questions:**
1. **Discovery:** "Как future AI agent найдет эту документацию?"
2. **Navigation:** "Где создать links для accessibility?"
3. **Integration:** "Какие protocols нужно обновить?"
4. **Workflow:** "Влияет ли на AI execution flow?"

### **Enforcement:**
**Documentation tasks НЕ считаются complete пока document остается isolated.**

---

**Protocol Version:** 1.1  
**Updated:** August 2025  
**Changes:** Added mandatory system integration requirements to prevent isolated documentation
**Scope:** Applies to all AI agent activities in the project

---

*This enhanced protocol ensures that all created documentation remains discoverable and integrated into the project's knowledge system, preventing isolation of important information.*