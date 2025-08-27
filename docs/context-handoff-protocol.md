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
- **DEV Workflows**: [status of each]
- **PROD Workflows**: [status of each]
- **Issues**: [current blockers/problems]

## Context for Next Agent
- **Role Needed**: [Architect/Developer/Tester]
- **Immediate Tasks**: [priority list]
- **Important Context**: [critical info to remember]
```

## 📁 Файловая структура для continuity:

```
docs/
├── current-session-state.md    # Live state
├── session-history/            # Archive of handoffs
│   ├── session-001-handoff.md
│   ├── session-002-handoff.md
│   └── ...
└── ai-assistant-guide.md       # Permanent instructions
```

**Готов внедрить этот протокол прямо сейчас!** 

Начинаем с создания базовой структуры?