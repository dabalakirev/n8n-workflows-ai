---
name: 🧪 Testing Task
about: Задача по тестированию workflow
title: '[TEST] '
labels: ['🧪 testing']
assignees: []

---

## 🧪 Тип тестирования
- [ ] 🔍 Unit тестирование (валидация отдельных узлов)
- [ ] 🔗 Integration тестирование (тестирование через Test Orchestrator)
- [ ] 🎭 End-to-end тестирование (полный сценарий)
- [ ] 🚀 Production verification (проверка в PROD)
- [ ] 🔄 Regression тестирование (после изменений)

## 🎯 Целевой workflow
- [ ] AI Deepseek
- [ ] FMP API Router
- [ ] Test Orchestrator
- [ ] Все workflows (full regression)

## 🌍 Окружение тестирования
- [ ] DEV (разработка)
- [ ] Test (через Test Orchestrator)  
- [ ] PROD (production verification)

## 📋 Сценарии тестирования

### Тестовые данные:
```json
{
  "input": {
    "example": "test data"
  }
}
```

### Ожидаемые результаты:
```json
{
  "expected": {
    "status": "success",
    "data": "expected output"
  }
}
```

### Критерии прохождения:
- [ ] Workflow выполняется без ошибок
- [ ] Время выполнения < ___ секунд
- [ ] Корректная обработка ошибок
- [ ] Правильный формат выходных данных
- [ ] Другие критерии: ___________

## 🔧 Техническая реализация

### Метод тестирования:
- [ ] Webhook trigger (Test Orchestrator)
- [ ] Manual execution в n8n
- [ ] API validation только
- [ ] Mock данные
- [ ] Real API calls

### Инструменты:
- [ ] n8n built-in тестирование
- [ ] Custom validation scripts
- [ ] Test Orchestrator workflow
- [ ] External testing tools

## ⚠️ Edge cases для проверки
- [ ] Пустые входные данные
- [ ] Некорректные форматы данных
- [ ] API timeouts/errors
- [ ] Rate limiting
- [ ] Network failures
- [ ] Другие: ___________

## 📊 Ожидаемые результаты теста

### Success scenarios:
1. ✅ Scenario 1: ___________
2. ✅ Scenario 2: ___________

### Error handling scenarios:
1. ❌ Error 1: ___________  
2. ❌ Error 2: ___________

## 🔄 Связанные задачи
- Тестирует feature: #___
- Блокируется: #___
- Блокирует: #___

## 📅 Критерии готовности
- [ ] Все тестовые сценарии пройдены
- [ ] Edge cases проверены
- [ ] Результаты задокументированы
- [ ] Regression тесты не сломались
- [ ] Performance соответствует требованиям

## ⚡ Приоритет
- [ ] 🔴 Critical (блокирует релиз)
- [ ] 🟡 High (важно для качества)
- [ ] 🟢 Medium (дополнительная проверка)
- [ ] ⚪ Low (nice to have coverage)

## 🚨 Действия при провале тестов
- [ ] Создать Bug Report
- [ ] Откатиться к предыдущей версии
- [ ] Заблокировать deploy в PROD
- [ ] Уведомить команду