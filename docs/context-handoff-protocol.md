# Context Handoff Protocol

## ⚠️ КРИТИЧЕСКИ ВАЖНО

**Каждый новый AI агент ОБЯЗАН:**
1. **Прочитать ВСЕ протоколы** проекта перед началом работы
2. **Строго следовать** установленным процедурам
3. **Следовать AI Agent Execution Protocol** для каждого задания
4. **Создавать Issues** для всех изменений согласно GitHub Issues Protocol
5. **Не нарушать** установленную архитектуру и процессы

## 🔄 Процедура смены AI агента

### Когда нужна смена чата:
- Приближение к лимиту контекста
- Смена фазы проекта (dev → testing → prod)
- Долгие задачи требующие "свежего старта"

### Перед завершением сессии:
1. AI агент **завершает Document phase** текущего задания
2. Создает/обновляет `current-session-state.md` с execution status
3. Коммитит все изменения в GitHub
4. Создает четкие инструкции для следующего агента
5. **Проверяет соблюдение всех протоколов**

### При начале новой сессии:
1. **ПЕРВОЕ ДЕЙСТВИЕ**: Читает ВСЕ файлы в `docs/` папке
2. Изучает установленные протоколы:
   - **[AI Agent Execution Protocol](ai-agent-execution-protocol.md)** - ОБЯЗАТЕЛЬНЫЙ workflow
   - [GitHub Issues Protocol](github-issues-protocol.md) 
   - [Testing Strategy](testing-strategy.md)
   - Этот Context Handoff Protocol
3. Проверяет состояние n8n workflows
4. Читает `current-session-state.md`
5. Подтверждает понимание контекста
6. **Начинает новые задания с Planning phase** согласно Execution Protocol

## 📋 Обязательные протоколы для изучения

### 🤖 AI Agent Execution Protocol
- **Обязательный 5-step flow** для всех заданий: Plan → Propose → Get Approval → Execute → Document
- **Mandatory action types** для team collaboration
- **Integration со всеми другими протоколами**
- 📖 **[ОБЯЗАТЕЛЬНО К ИЗУЧЕНИЮ ПЕРВЫМ →](ai-agent-execution-protocol.md)**

### 🎫 GitHub Issues Protocol
- **Все изменения** требуют создания Issues
- **Обязательные шаблоны** для разных типов задач
- **Lifecycle управление** от создания до закрытия
- 📖 **[ОБЯЗАТЕЛЬНО К ИЗУЧЕНИЮ →](github-issues-protocol.md)**

### 🧪 Testing Strategy  
- **Test Orchestrator** архитектура
- **Двойные триггеры** в DEV workflows
- **Валидация** перед PROD deploy
- 📖 **[ОБЯЗАТЕЛЬНО К ИЗУЧЕНИЮ →](testing-strategy.md)**

## 🧪 Тестовая архитектура

### Структура DEV workflows:
**Все DEV workflows имеют ДВА триггера:**
```
DEV Workflow:
├── Manual Trigger (основной, для ручного запуска)
└── Execute Workflow Trigger (тестовый, для вызова оркестратором)
    ↑
    └── Test Orchestrator
```

### Test Orchestrator:
- Специальный workflow с Webhook триггером
- Вызывает все DEV workflows через Execute Workflow узлы
- Собирает результаты тестирования
- Возвращает сводный отчет

### PROD vs DEV различия:
- **DEV**: 2 триггера (Manual + Execute Workflow)
- **PROD**: 1 триггер (только Manual)

## 📋 Template для передачи контекста:

```markdown
# Session Handoff - [Date]

## Protocol Compliance Check
- [ ] Новый агент прочитал AI Agent Execution Protocol (FIRST!)
- [ ] Новый агент прочитал GitHub Issues Protocol
- [ ] Новый агент прочитал Testing Strategy  
- [ ] Новый агент прочитал Context Handoff Protocol
- [ ] Все активные Issues проверены и поняты

## Current Execution Status
- **Active Assignment**: [Current task being worked on]
- **Execution Phase**: [Planning/Propose/Approval/Execute/Document]
- **Approved Plan**: [What was approved for execution]
- **Completion Status**: [What's been completed]
- **Next Steps**: [What needs to be done next in execution flow]

## Current Status
- **Project Phase**: [Development/Testing/Documentation]
- **Last Action**: [What was just completed]
- **Next Action**: [What needs to be done next]
- **Protocols Followed**: [Which protocols were followed in last session]

## Repository State
- **Branch**: main
- **Last Commit**: [sha + message]
- **Modified Files**: [list]
- **Active Issues**: [list of open Issues with links]

## n8n State  
- **DEV Workflows**: [status of each + testing triggers]
- **PROD Workflows**: [status of each]
- **Test Orchestrator**: [webhook URL, last test results]
- **Issues**: [current blockers/problems]

## Testing Context
- **Last Test Run**: [date/time]
- **Test Results**: [pass/fail summary]
- **Test Coverage**: [which workflows tested]
- **Known Test Issues**: [current testing problems]

## Protocol Violations (if any)
- **Issues Created**: [list any protocol violations from last session]
- **Corrective Actions**: [what was done to fix violations]

## Context for Next Agent
- **Role Needed**: [Architect/Developer/Tester]
- **Immediate Tasks**: [priority list with Issue numbers]
- **Testing Tasks**: [specific tests needed with Issue numbers]
- **Protocol Requirements**: [specific protocol compliance needed]
- **Execution Context**: [current assignment execution status]
- **Important Context**: [critical info to remember]

## Next Agent Instructions
1. READ AI Agent Execution Protocol FIRST - mandatory workflow
2. READ ALL OTHER DOCUMENTATION in docs/ folder  
3. Check current execution status and continue from appropriate phase
4. Check all active GitHub Issues before making ANY changes
5. Follow 5-step execution flow for all new assignments
6. Update this handoff document before ending session
```

## 📁 Файловая структура для continuity:

```
docs/
├── ai-agent-execution-protocol.md     # FIRST TO READ - mandatory workflow
├── current-session-state.md           # Live state (READ AFTER execution protocol)
├── github-issues-protocol.md          # ОБЯЗАТЕЛЬНО к изучению
├── testing-strategy.md                # ОБЯЗАТЕЛЬНО к изучению  
├── context-handoff-protocol.md        # Этот файл
├── session-history/                   # Archive of handoffs
│   ├── session-001-handoff.md
│   ├── session-002-handoff.md
│   └── ...
└── ai-assistant-guide.md              # Permanent instructions
```

## 🚨 Нарушения протокола

### Если новый агент нарушает протоколы:
1. **Немедленно остановить работу**
2. **Создать Issue** о нарушении протокола (если еще не в execution flow)
3. **Исправить нарушения** 
4. **Задокументировать** в session handoff
5. **Продолжить работу** только после исправления согласно Execution Protocol

### Типичные нарушения:
- **Пропуск AI Agent Execution Protocol** - самое серьезное нарушение
- Изменения без создания Issues
- Игнорирование Testing Strategy
- Не чтение документации перед началом работы
- Работа без понимания архитектуры проекта
- **Выполнение действий без approval** в Execution Protocol

---

**Соблюдение протоколов не опционально - это обязательное требование для всех участников проекта, включая AI агентов. AI Agent Execution Protocol является основополагающим для всех операций.**