# n8n Workflows

Эта папка содержит все n8n workflows проекта, разделенные по окружениям DEV и PROD.

## 📁 Структура

```
workflows/
├── dev/                    # DEV workflows для разработки и тестирования
│   ├── ai-deepseek-dev.json      # AI агент с DeepSeek (2 триггера)
│   ├── fmp-router-dev.json       # API роутер для FMP (2 триггера)  
│   └── README.md                 # Документация DEV окружения
├── prod/                   # PROD workflows для производственного использования
│   ├── ai-deepseek-prod.json     # AI агент с DeepSeek (1 триггер)
│   ├── fmp-router-prod.json      # API роутер для FMP (1 триггер)
│   └── README.md                 # Документация PROD окружения
└── README.md              # Этот файл
```

## 🔧 Окружения

### 🔄 **DEV Environment**
- **Цель**: Разработка, тестирование, отладка
- **Триггеры**: Manual Trigger + Execute Workflow Trigger
- **Тестирование**: Автоматическое через Test Orchestrator
- **Особенности**: Pinned test data, расширенное логирование

### 🚀 **PROD Environment**  
- **Цель**: Производственное использование
- **Триггеры**: Только Manual Trigger
- **Стабильность**: Полностью протестированные версии
- **Особенности**: Производственные credentials, мониторинг

## 📊 Workflows

### AI Deepseek
**Описание**: AI агент с DeepSeek для анализа финансовых данных через FMP API

**DEV версия** (`ai-deepseek-dev.json`):
- Manual Trigger для ручного тестирования
- Execute Workflow Trigger для Test Orchestrator
- Test data в pinData для быстрых тестов

**PROD версия** (`ai-deepseek-prod.json`):
- Только Manual Trigger  
- Производственный prompt
- Без test data

### FMP API Router
**Описание**: API роутер для Financial Modeling Prep с маршрутизацией команд

**DEV версия** (`fmp-router-dev.json`):
- Manual Test Trigger для локального тестирования
- Execute Workflow Trigger для интеграции с AI Deepseek
- Test data в pinData

**PROD версия** (`fmp-router-prod.json`):
- Только Manual Trigger
- Без test data
- Оптимизированная производительность

## 🚀 Workflow Migration Process

### DEV → PROD Migration:
1. **Разработка** изменений в DEV версии
2. **Тестирование** через Test Orchestrator 
3. **Валидация** через GitHub Actions
4. **Manual review** и approval
5. **Migration** в PROD после подтверждения
6. **Deploy** в производственное n8n окружение

## 🧪 Тестирование

### GitHub Actions Validation:
- JSON структура проверяется автоматически
- DEV workflows должны иметь 2 триггера
- PROD workflows должны иметь 1 триггер
- Security scan на hardcoded secrets

### Test Orchestrator (планируется):
- Автоматическое тестирование DEV workflows
- Integration testing между AI Deepseek и FMP Router
- Performance и reliability тесты

## 📋 Использование

### Для разработчиков:
1. Импортировать DEV workflows в DEV проект n8n
2. Настроить необходимые credentials
3. Тестировать через Manual triggers
4. Использовать Test Orchestrator для автоматических тестов

### Для production:
1. Импортировать PROD workflows в PROD проект n8n  
2. Настроить production credentials
3. Настроить мониторинг и alerting
4. Запускать только через Manual trigger

## ⚠️ Важные правила

1. **НЕ модифицировать PROD файлы напрямую** - только через DEV → PROD процесс
2. **Следовать naming convention** с суффиксами -dev/-prod
3. **Поддерживать синхронность** между DEV и PROD логикой
4. **Тестировать все изменения** в DEV перед миграцией
5. **Использовать Version Control** для всех изменений

## 🔗 Связанные ресурсы

- [Project Roadmap](../docs/roadmap.md) - общий план развития
- [Testing Strategy](../docs/testing-strategy.md) - стратегия тестирования  
- [GitHub Issues Protocol](../docs/github-issues-protocol.md) - процесс работы с задачами
- [AI Agent Roles & Protocols](../docs/ai-agent-roles-protocols.md) - роли AI агента

---

**Статус**: ✅ Структура обновлена (Issue #15 - Hotfix)  
**Последнее обновление**: August 2025  
**Версия**: v1.1 (DEV/PROD разделение)
