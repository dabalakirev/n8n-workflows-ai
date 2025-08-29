# AI Agent Execution Protocol

## 🚨 **MANDATORY PROTOCOL ENFORCEMENT**

### **⚠️ ПЕРЕД КАЖДЫМ ОТВЕТОМ AI Agent ОБЯЗАН:**

1. **✅ Explicitly заявить текущую Phase:** `"Phase 1: Planning"` 
2. **✅ Выполнить Context Awareness Check** (даже для "простых" задач)
3. **✅ Никогда не пропускать phases** независимо от сложности задачи
4. **✅ Помнить: НЕТ exceptions** для "quick fixes" или "obvious solutions"

### **🔍 Pre-Response Self-Check Checklist:**
```markdown
Перед каждым ответом проверить:
- [ ] Проверил ли я existing docs/files связанные с этой темой?
- [ ] Начинаю ли я с "Phase 1: Planning"?
- [ ] Следую ли я 5-step execution flow?
- [ ] Проанализировал ли context перед предложением solutions?
- [ ] Это действительно "простая" задача или я пропускаю важные детали?
```

### **🚩 Warning Signs Protocol Violation:**
- **❌ Начинать с "I suggest..." без Planning phase**
- **❌ Не проверять существующую documentation/files**  
- **❌ Спешить к solutions без context analysis**
- **❌ Думать "это слишком просто для full protocol"**
- **❌ Пропускать Context Awareness из-за "очевидности" задачи**

### **💡 Fundamental Principle:**
> **"Context First, Solutions Second"** - Даже для seemingly obvious задач, Context Awareness Check reveals critical information that prevents errors и duplicate work.

---

## 🎯 Overview

Этот протокол определяет обязательную последовательность действий для AI агента при выполнении любого задания в проекте. Фокус на командной работе и документальном сопровождении.

---

## 🔄 Core Execution Flow

### **"Plan → Propose → Get Approval → Execute → Document"**

Каждое задание проходит через эти 5 этапов без исключений.

---

## 1. 📋 Planning (Планирование)

### **🎯 Цель:** Понять задание и определить scope работ

### **🔍 MANDATORY Context Awareness Check:**
**ВСЕГДА выполнять перед любым заданием (включая "простые"):**
- **✅ Проверить existing documentation/files** связанные с задачей
- **✅ Новые комментарии к связанным Issues**
- **✅ Recent GitHub Actions результаты**  
- **✅ Updates в зависимых задачах**
- **✅ Changes в related protocols/files**

**⚠️ НИКОГДА не пропускать этот шаг из-за "простоты" задачи!**

### **Дополнительные обязательные действия:**
- **Analyze Assignment** - понять что требуется сделать
- **Identify Key Actions** - определить основные действия для выполнения
- **Determine Documentation Impact** - какая документация потребует обновления
- **Assess Issues Impact** - какие Issues будут затронуты (создание/обновление/закрытие)

**Результат:** Понимание полного scope задания с актуальным контекстом

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

#### **🔗 System Integration**
**MANDATORY для КАЖДОГО созданного документа:**
- **Update README.md** - добавить новую документацию в navigation
- **Add protocol references** - обновить relevant AI protocols с links
- **Create discovery paths** - ensure future AI agents найдут документ
- **Verify navigation** - проверить что документ accessible через existing paths

#### **💬 Progress Communication**  
- **Status updates** - о ходе выполнения в Issue комментариях
- **Results summary** - итоговые результаты и deliverables
- **Lessons learned** - важные findings для будущих задач

#### **🎯 Integration Verification Checklist**
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
| **Context Awareness** | **ВСЕГДА в Planning** | **Check existing docs, recent changes** |
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
- **Context awareness activities**
- Командные коммуникации
- Документальные изменения
- **System integration requirements**
- Issues lifecycle management
- Knowledge sharing activities

---

## 🎯 Success Criteria - ENHANCED

**Задание считается выполненным когда:**
- ✅ **Context проверен и актуален**
- ✅ Все planned actions завершены
- ✅ Соответствующие Issues обновлены/закрыты
- ✅ Документация актуализирована
- ✅ **README.md updated с новой документацией**
- ✅ **Navigation paths созданы для discovery**
- ✅ **System integration completed**
- ✅ Команда informative о результатах

**Задание НЕ завершено если:**
- ❌ **Context не проверен перед началом**
- ❌ Issues остались без обновления
- ❌ Документация не отражает изменения
- ❌ **Новые документы изолированы и недоступны**
- ❌ **README или protocols не обновлены**
- ❌ Нет communication о результатах
- ❌ Broken cross-references в документации

---

## 💡 Protocol Examples

### **Example 1: Bug Fix Task**
```
Planning: Check recent comments on Issue, understand bug, identify fix approach
Propose: Fix steps + Issue closure + documentation updates
Execute: Implement fix, test, document
Document: Close Issue, update troubleshooting docs, UPDATE README navigation, communicate fix
```

### **Example 2: New Feature Task**  
```
Planning: Check project status, feature requirements, design approach, documentation needs
Propose: Implementation plan + new Issues + comprehensive docs + system integration
Execute: Build feature, test, integrate
Document: Update Issues, create user guides, ADD TO README navigation, UPDATE protocols, announce feature
```

### **Example 3: Documentation Task** - ENHANCED
```
Planning: Check recent activity, documentation gaps, target audience, related Issues, WHERE TO INTEGRATE
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
- New agent начинает с Planning phase (INCLUDING context awareness check)
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
1. **Context:** "Что изменилось с последнего обновления?"
2. **Discovery:** "Как future AI agent найдет эту документацию?"
3. **Navigation:** "Где создать links для accessibility?"
4. **Integration:** "Какие protocols нужно обновить?"
5. **Workflow:** "Влияет ли на AI execution flow?"

### **Enforcement:**
- **Context awareness НЕ optional** - обязательно в Planning phase
- **Documentation tasks НЕ считаются complete** пока document остается isolated

---

## 📚 **Protocol Discipline Guidelines**

### **🎯 Key Mindset:**
- **Protocol = Discipline, не Guideline**
- **NO shortcuts даже для "obvious" tasks**
- **Context First, Solutions Second ALWAYS**
- **When in doubt, follow the protocol completely**

### **🚫 Common Anti-Patterns to AVOID:**
- "This is too simple for full protocol"
- "I already know what needs to be done"
- "Let me quickly fix this without checking context"
- "Skip Context Awareness, it's obvious"
- "Rush to propose solution without planning"

### **✅ Proper Mindset:**
- "Even simple tasks benefit from systematic approach"
- "Context Awareness reveals unexpected information"
- "Following protocol prevents errors and rework"
- "Structured approach improves quality"
- "Protocol compliance builds team trust"

---

**Protocol Version:** 1.3  
**Updated:** August 2025  
**Changes:** Added Mandatory Protocol Enforcement section, Pre-Response Checklist, Warning Signs, and enhanced Context Awareness requirements
**Scope:** Applies to all AI agent activities in the project

---

*This enhanced protocol with enforcement mechanisms ensures AI agents maintain discipline and never skip critical steps, regardless of perceived task simplicity.*