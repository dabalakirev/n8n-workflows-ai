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

## 5. 📚 Document (Документирование)

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

#### **💬 Progress Communication**  
- **Status updates** - о ходе выполнения в Issue комментариях
- **Results summary** - итоговые результаты и deliverables
- **Lessons learned** - важные findings для будущих задач

#### **🔗 Cross-references**
- **Link related Issues** - через "relates to #N", "fixes #N"
- **Update document links** - при изменении структуры
- **Maintain navigation** - README, Wiki links актуальны

**Результат:** Полная командная transparency и документальное покрытие

---

## 🛡️ Mandatory Action Types

### **При каждом задании проверить необходимость:**

| Action Type | When Required | Example |
|------------|---------------|---------|
| **Issues Management** | Always | Create/Update/Close Issues |
| **Documentation** | When functionality changes | Update README, guides, specs |
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
- Issues lifecycle management
- Knowledge sharing activities

---

## 🎯 Success Criteria

**Задание считается выполненным когда:**
- ✅ Все planned actions завершены
- ✅ Соответствующие Issues обновлены/закрыты
- ✅ Документация актуализирована
- ✅ Команда informative о результатах

**Задание НЕ завершено если:**
- ❌ Issues остались без обновления
- ❌ Документация не отражает изменения
- ❌ Нет communication о результатах
- ❌ Broken cross-references в документации

---

## 💡 Protocol Examples

### **Example 1: Bug Fix Task**
```
Planning: Understand bug, identify fix approach, determine docs impact
Propose: Fix steps + Issue closure + documentation updates
Execute: Implement fix, test, document
Document: Close Issue, update troubleshooting docs, communicate fix
```

### **Example 2: New Feature Task**  
```
Planning: Feature requirements, design approach, documentation needs
Propose: Implementation plan + new Issues + comprehensive docs
Execute: Build feature, test, integrate
Document: Update Issues, create user guides, announce feature
```

### **Example 3: Documentation Task**
```
Planning: Documentation gaps, target audience, related Issues
Propose: Documentation structure + Issue updates + cross-references  
Execute: Write documentation, review, publish
Document: Close Issues, update navigation, communicate availability
```

---

## 🔄 Integration with Project Protocols

### **Relationship to other protocols:**
- **AI Agent Roles Protocol** - определяет роли, этот протокол - execution process
- **GitHub Issues Protocol** - обеспечивает compliance с Issues management
- **Context Handoff Protocol** - этот протокол создает context для handoff

### **When switching between AI agents:**
- Current agent должен завершить Document phase
- New agent начинает с Planning phase для новых задач
- Ongoing tasks передаются с current execution status

---

**Protocol Version:** 1.0  
**Created:** August 2025  
**Scope:** Applies to all AI agent activities in the project

---

*This protocol ensures consistent team collaboration and knowledge management while preserving AI agent autonomy in technical implementation details.*