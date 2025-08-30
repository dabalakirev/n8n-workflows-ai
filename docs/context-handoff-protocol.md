# Context Handoff Protocol

## ⚠️ КРИТИЧЕСКИ ВАЖНО
**Каждый новый AI агент ОБЯЗАН:**
1. **Прочитать ВСЕ протоколы** проекта перед началом работы
2. **Следовать AI Agent Execution Protocol** для каждого задания  
3. **Создавать Issues** для всех изменений согласно GitHub Issues Protocol

## 📋 ОБЯЗАТЕЛЬНЫЕ ПРОТОКОЛЫ (читать в порядке приоритета)

### 🤖 [AI Agent Execution Protocol](ai-agent-execution-protocol.md) 
**ЧИТАТЬ ПЕРВЫМ** - обязательный 5-step workflow для всех заданий

### 🎫 [GitHub Issues Protocol](github-issues-protocol.md)
Все изменения требуют создания Issues с правильными типами и форматом

### 🧪 [Testing Strategy](testing-strategy.md)
Test Orchestrator архитектура и валидация workflows

### 🔄 [Roadmap](roadmap.md)
Текущий статус платформы и приоритеты

## 🔄 Процедура смены агента

### При завершении сессии:
1. Завершить Document phase текущего задания
2. Обновить `current-session-state.md` 
3. Коммитить все изменения
4. Создать handoff инструкции

### При начале новой сессии:
1. **ПЕРВОЕ ДЕЙСТВИЕ**: Читать AI Agent Execution Protocol
2. Изучить все протоколы в `docs/` папке
3. Проверить состояние workflows и Issues
4. Прочитать `current-session-state.md`
5. Начинать с Planning phase согласно Execution Protocol

## 🧪 Тестовая архитектура
**DEV workflows**: 2 триггера (Manual + Execute Workflow для Test Orchestrator)
**PROD workflows**: 1 триггер (только Manual)

## 📋 Handoff Template
```markdown
# Session Handoff - [Date]

## Protocol Compliance 
- [ ] AI Agent Execution Protocol прочитан
- [ ] Все протоколы изучены
- [ ] Issues проверены

## Current Status
- **Active Assignment**: [текущее задание]
- **Execution Phase**: [Planning/Propose/Execute/Document]
- **Next Steps**: [что нужно сделать дальше]

## Repository State
- **Active Issues**: [список открытых Issues]
- **n8n Workflows**: [статус DEV/PROD workflows]
- **Test Results**: [последние результаты тестирования]
```

## 🚨 Нарушения протокола
- **Пропуск AI Agent Execution Protocol** - критическое нарушение
- Изменения без Issues
- Игнорирование Testing Strategy
- Работа без изучения документации

*Соблюдение протоколов обязательно для всех участников проекта.*