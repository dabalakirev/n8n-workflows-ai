# Context Handoff Protocol

## ⚠️ КРИТИЧЕСКИ ВАЖНО
**Каждый новый AI агент ОБЯЗАН:**
1. **Прочитать ВСЕ протоколы** проекта перед началом работы
2. **Следовать AI Agent Execution Protocol** для каждого задания  
3. **Создавать Issues** для всех изменений согласно GitHub Issues Protocol

## 🚨 PROJECT DOCUMENTATION ISOLATION - CRITICAL

### **⛔ НЕ ЧИТАТЬ при onboarding (если НЕТ прямого указания):**
- `docs/projects/` - **Документация завершенных проектов**
- `workflows/[project-name]/` - **Project-specific workflow documentation**

**Исключения:**
- ✅ Только при **прямом указании** изучить specific project
- ✅ При назначении на **maintenance existing project**
- ✅ При **explicit reference** к проекту в assignment

### **📋 Platform vs Project Documentation:**

| **📚 PLATFORM (ЧИТАТЬ ОБЯЗАТЕЛЬНО)** | **🚫 PROJECT (НЕ ЧИТАТЬ без указания)** |
|---------------------------------------|------------------------------------------|
| `docs/ai-agent-*` protocols | `docs/projects/first-bird/` |
| `docs/testing-strategy.md` | `workflows/first-bird/` |
| `docs/github-issues-protocol.md` | `docs/projects/[any-project]/` |
| **Main README.md** | `workflows/[any-project]/` |

**Key Principle:** **Platform Knowledge First** - Изучить platform protocols BEFORE diving в specific projects

## 📋 ОБЯЗАТЕЛЬНЫЕ ПРОТОКОЛЫ (читать в порядке приоритета)

### 🤖 [AI Agent Execution Protocol](ai-agent-execution-protocol.md) 
**ЧИТАТЬ ПЕРВЫМ** - обязательный 5-step workflow для всех заданий

### 🎫 [GitHub Issues Protocol](github-issues-protocol.md)
Все изменения требуют создания Issues с правильными типами и форматом

### 🎭 [AI Agent Roles & Protocols](ai-agent-roles-protocols.md)
Role definitions и Issue creation права

### 🧪 [MCP Webhook Testing Guide](mcp-webhook-testing-guide.md)
Practical testing procedures для workflow validation

### 📚 [Documentation Consistency Procedure](documentation-consistency-procedure.md)
Prevent duplication и maintain consistency

### 🔄 [Roadmap](roadmap.md)
Текущий статус платформы и приоритеты

## 🔄 Процедура смены агента

### При завершении сессии:
1. Завершить Document phase текущего задания
2. Коммитить все изменения
3. Создать handoff инструкции

### При начале новой сессии:
1. **ПЕРВОЕ ДЕЙСТВИЕ**: Читать AI Agent Execution Protocol
2. **Изучить ТОЛЬКО platform protocols** (НЕ project documentation)
3. Проверить состояние workflows и Issues
4. Начинать с Planning phase согласно Execution Protocol

## 📋 Enhanced Handoff Template
```markdown
# Session Handoff - [Date]

## Protocol Compliance 
- [ ] AI Agent Execution Protocol прочитан
- [ ] Platform protocols изучены (НЕ project docs)
- [ ] Issues проверены
- [ ] Current project assignment понят

## Current Status
- **Active Assignment**: [текущее задание]
- **Project Scope**: [platform/specific project]
- **Execution Phase**: [Planning/Propose/Execute/Document]
- **Next Steps**: [что нужно сделать дальше]

## Repository State
- **Active Issues**: [список открытых Issues]
- **n8n Workflows**: [статус DEV/PROD workflows]
- **Project Focus**: [platform improvement/project work]
```

## 🚨 Нарушения протокола
- **Пропуск AI Agent Execution Protocol** - критическое нарушение
- **Чтение project documentation без указания** - waste of context
- Изменения без Issues
- Игнорирование Testing Strategy
- Работа без изучения platform protocols

## ✅ Success Indicators
- **Efficient Onboarding**: AI agent knows platform без diving в irrelevant project details
- **Focused Context**: Clear understanding current assignment scope
- **Protocol Compliance**: Following established procedures consistently

*Соблюдение протоколов обязательно для всех участников проекта.*