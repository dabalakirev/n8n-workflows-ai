# Testing Strategy - Test Orchestrator Architecture

## 🎯 Общая концепция

Используем **Test Orchestrator** - специальный workflow, который управляет тестированием всех DEV workflows через n8n API.

## 🏗️ Архитектура тестирования

### DEV Workflow структура (двойные триггеры):
```
┌─────────────────────────────────────────┐
│             DEV Workflow                │
│                                         │
│  Manual Trigger ──┐                     │
│                   ├──→ [Основная логика]│──→ Output
│  Execute Workflow │                     │
│  Trigger ──────────┘                    │
│      ↑                                  │
│      │ Вызывается Test Orchestrator     │
└─────────────────────────────────────────┘
```

### Test Orchestrator структура:
```
┌──────────────────────────────────────────────────────┐
│                Test Orchestrator                     │
│                                                      │
│ Webhook ──→ Execute ──→ Execute ──→ Execute ──→ Report│
│ Trigger     DEV WF1     DEV WF2     DEV WF3     Node │
│                                                      │
│ Input: тестовые данные                               │
│ Output: сводный отчет по всем тестам                 │
└──────────────────────────────────────────────────────┘
```

## 🔄 Процесс тестирования

### 1. Подготовка DEV workflow:
```javascript
// Каждый DEV workflow должен иметь:
1. Manual Trigger (основной)
2. Execute Workflow Trigger (тестовый)
3. Общий выход из обоих триггеров в основную логику
```

### 2. Test Orchestrator workflow:
- **Webhook Trigger** - принимает команды на тестирование
- **Execute Workflow узлы** - вызывают каждый DEV workflow
- **Aggregation Logic** - собирает результаты всех тестов
- **Report Generator** - формирует сводный отчет

### 3. Запуск тестирования:
```
AI Agent ──→ POST к Webhook ──→ Test Orchestrator ──→ Тестирует все DEV workflows ──→ Результат
```

## 📊 Тестовые данные и результаты

### Input для Test Orchestrator:
```json
{
  "testSuite": "full|quick|specific",
  "workflows": ["ai-deepseek", "fpm-router"],
  "testData": {
    "ai-deepseek": { "input": "test query" },
    "fmp-router": { "toolName": "test", "params": {} }
  }
}
```

### Output от Test Orchestrator:
```json
{
  "testResults": {
    "ai-deepseek": { "status": "pass|fail", "error": null, "duration": "2.3s" },
    "fmp-router": { "status": "pass", "error": null, "duration": "1.1s" }
  },
  "summary": {
    "total": 2,
    "passed": 2,
    "failed": 0,
    "duration": "3.4s"
  }
}
```

## 🚀 DEV vs PROD различия

### DEV Environment:
- **Количество триггеров**: 2 (Manual + Execute Workflow)
- **Назначение**: Разработка + тестирование
- **Test Orchestrator**: Присутствует
- **Webhook URLs**: Доступны для тестирования

### PROD Environment:
- **Количество триггеров**: 1 (только Manual)
- **Назначение**: Продакшн использование
- **Test Orchestrator**: Отсутствует
- **Webhook URLs**: Отсутствуют

## 🔧 Практическая реализация

### Создание DEV workflow:
1. Копируем PROD версию
2. Добавляем Execute Workflow Trigger
3. Соединяем оба триггера с основной логикой
4. Тестируем через оркестратор

### Перенос в PROD:
1. Копируем DEV workflow
2. **Удаляем Execute Workflow Trigger**
3. Оставляем только Manual Trigger
4. Деплоим в PROD проект

## ⚠️ Важные ограничения

### n8n API ограничения:
- ❌ Нельзя активировать/деактивировать workflows программно
- ❌ Нельзя выполнять workflows с Manual Trigger напрямую
- ✅ Можно вызывать workflows через Execute Workflow узлы
- ✅ Можно запускать workflows через Webhook

### Тестовые ограничения:
- Manual Trigger логика тестируется косвенно
- Некоторые trigger-специфичные особенности могут отличаться
- Schedule triggers не тестируются

## 📝 Чеклист для настройки

### DEV Workflow:
- [ ] Manual Trigger настроен
- [ ] Execute Workflow Trigger добавлен  
- [ ] Оба триггера ведут к общей логике
- [ ] Workflow протестирован через оркестратор

### Test Orchestrator:
- [ ] Webhook Trigger настроен
- [ ] Execute Workflow узлы для всех DEV workflows
- [ ] Сбор и агрегация результатов
- [ ] Формирование отчета

### PROD Migration:
- [ ] Execute Workflow Trigger удален
- [ ] Только Manual Trigger остался
- [ ] Логика полностью идентична DEV
- [ ] Финальная проверка работоспособности

---

*Эта стратегия обеспечивает надежное тестирование DEV workflows перед переносом в PROD, сохраняя архитектурную целостность системы.*