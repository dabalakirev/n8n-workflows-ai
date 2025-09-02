# MCP CI/CD Deployment Protocol

## ⚠️ ОБЯЗАТЕЛЬНЫЙ ПРОТОКОЛ
Это ФУНДАМЕНТАЛЬНЫЙ план действий, который ОБЯЗАТЕЛЬНО должен выполняться в строгой последовательности. Переход к следующему пункту БЕЗ выполнения предыдущих ЗАПРЕЩЕН.

## 🎯 Цель
CI/CD процесс для n8n workflow разработки с использованием MCP-first подхода.

## 🔄 Основные фазы

### 1. **🏗️ Architecture Design**
- Анализ требований и планирование
- Создание Issues с критериями успеха
- Определение MCP подхода

### 2. **💻 MCP-First Development**
- Анализ текущего состояния (`n8n_list_workflows`)
- Реализация через MCP (`n8n_create_workflow`, `n8n_update_full_workflow`)
- **DEV триггеры**: Manual + Execute Workflow (для тестирования)
- Синхронизация с GitHub

### 🔐 **Credentials Requirements**
- **Source:** Use exact credential IDs from `docs/projects/[project]/credentials-reference.md`  
- **Format:** Copy credential objects with ID + name from reference file
- **Validation:** Verify credential names match n8n instance before deployment

### 3. **🧪 Testing**
- Выполнение тестов workflow
- Анализ результатов выполнения
- Создание Bug Issues при необходимости

### 4. **🔄 DEV-GitHub Sync**
- **ПОСЛЕ успешных тестов**: синхронизация DEV workflows с GitHub
- Обновление DEV файлов в папке проекта
- Валидация соответствия n8n ↔ GitHub

### 5. **🚀 Production Deployment**
- **PROD триггер**: только Manual (безопасность)
- Удаление Execute Workflow триггера из DEV версии
- Валидация и синхронизация с GitHub

### 6. **🏷️ Release Management**
- Семантическое версioning
- Создание GitHub Release
- Публикация release notes

### 7. **📚 Documentation**
- Обновление документации workflow
- Поддержка cross-references

## 🚨 Критические требования

### **Триггеры:**
- **DEV workflows**: 2 триггера (Manual + Execute Workflow)
- **PROD workflows**: 1 триггер (только Manual)

### **MCP-First подход:**
```bash
# Development
n8n_create_workflow({name, nodes, connections})

# Testing  
n8n_get_execution(executionId) // анализ результатов

# DEV-GitHub Sync
github-mcp:create_or_update_file("workflows/project/dev/")

# Production
n8n_create_workflow(prodConfig) // без Execute Workflow триггера
```

### **UI Escalation протокол:**
При ограничениях MCP:
1. **Убедиться**, что ограничение реально (прописано в документации n8n)
2. **Если ограничение реально**: документировать в комментарии текущего Issue
3. **Создать подробную пошаговую инструкцию** для выполнения действия через UI платформы n8n
4. Добавить label "🔴 manual-ui-required"

## 📋 Quality Gates
- [ ] JSON Schema валидация
- [ ] Workflow тестирование
- [ ] DEV-GitHub синхронизация
- [ ] Architecture review
- [ ] Security review (для PROD)

## 🔄 Role Switching формат
```
🎭 [ROLE SWITCH] Current → Next
Reason: [причина перехода]
Context: [контекст проекта]
```

*Протокол обеспечивает систематическую разработку workflow с MCP автоматизацией и production-ready deployment.*