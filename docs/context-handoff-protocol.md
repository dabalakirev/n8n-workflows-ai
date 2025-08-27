# Context Handoff Protocol

## 🔄 Процедура смены AI агента

### Когда нужна смена чата:
- Приближение к лимиту контекста
- Смена фазы проекта (dev → testing → prod)
- Долгие задачи требующие "свежего старта"

### Перед завершением сессии:
1. AI агент создает/обновляет `current-session-state.md`
2. Коммитит все изменения в GitHub
3. Создает четкие инструкции для следующего агента

### При начале новой сессии:
1. Новый агент читает `current-session-state.md`
2. Проверяет состояние n8n workflows
3. Подтверждает понимание контекста
4. Продолжает работу с указанного места

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

## Current Status
- **Project Phase**: [Development/Testing/Documentation]
- **Last Action**: [What was just completed]
- **Next Action**: [What needs to be done next]

## Repository State
- **Branch**: main
- **Last Commit**: [sha + message]
- **Modified Files**: [list]

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

## Context for Next Agent
- **Role Needed**: [Architect/Developer/Tester]
- **Immediate Tasks**: [priority list]
- **Testing Tasks**: [specific tests needed]
- **Important Context**: [critical info to remember]
```

## 📁 Файловая структура для continuity:

```
docs/
├── current-session-state.md    # Live state
├── testing-strategy.md         # Testing approach with orchestrator
├── session-history/            # Archive of handoffs
│   ├── session-001-handoff.md
│   ├── session-002-handoff.md
│   └── ...
└── ai-assistant-guide.md       # Permanent instructions
```

**Готов внедрить этот протокол прямо сейчас!** 

Начинаем с создания базовой структуры?