# GitHub Issues Usage Protocol

## 📋 Общие принципы

GitHub Issues используются для **трекинга всех изменений** в проекте n8n workflows, обеспечивая прозрачность, документирование решений и контроль качества.

**⚡ ВАЖНО:** Управление Issues является частью **[AI Agent Execution Protocol](ai-agent-execution-protocol.md)**. Все AI агенты должны следовать 5-step execution flow, включая обязательные Issues Management actions.

## 📝 Issue Naming Convention

### **Обязательный формат заголовков:**
```
[TYPE] Краткое описание задачи
```

**Всегда указывать ТИП в квадратных скобках первым:**
- `[DOCS] Обновить архитектурную документацию`  
- `[BUG] FMP API Router падает при timeout`
- `[FEATURE] Добавить Slack уведомления`
- `[TEST] Создать тестовые webhook scenarios`
- `[АРХИТЕКТУРА] Внедрить Test Webhook - Test Execution подход`

### **Допустимые ТИПЫ (обязательно один из списка):**
- `[BUG]` - ошибки и неисправности
- `[FEATURE]` - новые функции
- `[ENHANCEMENT]` - улучшения существующих функций
- `[DOCS]` - задачи по документации
- `[TEST]` - тестовые задачи
- `[WORKFLOW]` - изменения в n8n workflow
- `[АРХИТЕКТУРА]` - архитектурные изменения уровня платформы

### **Приоритет указывается только в Labels:**
Приоритет НЕ указывается в заголовке - для этого есть labels:
- 🔴 `critical` - критические (блокируют работу, архитектурные)
- 🟡 `high` - высокие (важные функции)
- 🟢 `medium` - средние (улучшения UX)
- ⚪ `low` - низкие (nice to have)

**⚡ КРИТИЧЕСКИ ВАЖНО:** Всегда указывайте ТИП первым - это предотвращает ошибки в GitHub Actions и обеспечивает правильную категоризацию.

## ✅ ОБЯЗАТЕЛЬНО создаем Issues когда:

### 🔄 Изменения в workflow:
- **Создание нового workflow** любого типа
- **Добавление/удаление узлов** в существующий workflow
- **✅ Добавление test webhook triggers** в parent workflows
- **Изменение логики или параметров** узлов
- **Обновление API endpoints** или credentials
- **Миграция DEV → PROD** (каждый перенос)
- **Изменение структуры connections** между узлами
- **✅ Parent-child workflow integration** changes

**Примеры:**
- `[FEATURE] Создать workflow для анализа криптовалют`
- `[ENHANCEMENT] Добавить error handling в FMP API Router`
- `[WORKFLOW] Миграция AI Deepseek v1.2 в PROD`
- `✅ [WORKFLOW] Добавить test webhook в AI Deepseek DEV`

### 🐛 Проблемы и баги:
- **Workflow выдает ошибки** при выполнении
- **Неожиданное поведение** узлов или логики
- **Проблемы с API интеграциями** (timeouts, 404, etc.)
- **✅ Ошибки в parent-child workflow interactions**
- **✅ Test webhook configuration problems**
- **Проблемы синхронизации** GitHub ↔ n8n
- **Performance issues** (медленное выполнение)

**Примеры:**
- `[BUG] FMP API Router возвращает 500 для Insider.Trading.Latest`
- `✅ [BUG] Parent workflow test webhook не вызывает child workflows`
- `✅ [BUG] Child workflow integration с parent не работает correctly`

### 🧪 Тестирование:
- **Создание новых тестовых сценариев**
- **✅ Test webhook setup и configuration**
- **✅ Parent workflow testing через test webhooks**
- **✅ Child workflow integration validation**
- **Regression тестирование** после изменений
- **Performance тестирование** workflows
- **Интеграционное тестирование** новых API
- **End-to-end тестирование** полных сценариев

**Примеры:**
- `[TEST] Создать regression тесты для FMP API изменений`
- `✅ [TEST] Протестировать AI Deepseek через test webhook`
- `✅ [TEST] Валидировать parent-child workflow integration`

### 📚 Документация:
- **Обновление архитектурных решений** и диаграмм
- **✅ Testing methodology documentation updates**
- **✅ Test webhook procedures guides**
- **Создание новых руководств** по использованию
- **Обновление API документации** после изменений
- **Изменения в процессах разработки**
- **Документирование новых patterns** и best practices

**Примеры:**
- `[DOCS] Обновить схему testing архитектуры`
- `✅ [DOCS] Создать руководство по test webhook configuration`
- `✅ [DOCS] Документировать Test Webhook - Test Execution подход`

### 🏗️ Архитектурные изменения:
- **Изменения в структуре проекта** (папки, файлы)
- **✅ Testing methodology changes** (Test Orchestrator → Test Webhook approach)
- **✅ Protocol updates** для new testing architecture
- **Новые environments** (DEV/PROD/TEST настройки)
- **Обновления MCP серверов** и интеграций
- **Изменения в CI/CD процессах**
- **Рефакторинг** существующих решений

**Примеры:**
- `[ENHANCEMENT] Реструктурировать папки workflows`
- `[FEATURE] Добавить Slack MCP для уведомлений`
- `✅ [АРХИТЕКТУРА] Внедрить Test Webhook - Test Execution подход`

## ❌ НЕ создаем Issues для:

### 💬 Простые консультации:
- Объяснение **как работает** существующий workflow
- Вопросы по **использованию n8n функций**
- Разъяснения по **существующей документации**
- **✅ Clarification вопросы** о Test Webhook - Test Execution подходе без changes
- Обычные **обсуждения архитектуры** без планируемых изменений
- **Brainstorming** и исследовательские вопросы

### 🔧 Мелкие правки:
- Исправление **опечаток** в документации (< 5 строк)
- Обновление **комментариев** в workflow JSON
- **Форматирование** файлов без изменения логики
- **Косметические изменения** без функционального impact

### 📊 Мониторинг и статус:
- **Проверка статуса** workflow (активен/неактивен)
- **Получение логов** выполнения для анализа
- **Просмотр метрик** и статистики
- **Диагностика** без планируемых изменений

### 🎓 Обучение и исследования:
- **Изучение возможностей** n8n без изменений
- **Эксперименты** без сохранения в репозиторий
- **Proof-of-concept** без планируемого деплоя
- **Обучающие вопросы** по технологиям

## 🔄 Lifecycle Issues

### Создание Issue:
1. **До начала любой работы** - создаем соответствующий Issue
2. **Выбираем правильный шаблон** (Bug/Feature/Enhancement/Docs/Test)
3. **Заполняем все обязательные поля** по шаблону
4. **Обязательно указываем TYPE в заголовке**: `[TYPE] Description`
5. **Назначаем appropriate labels** для приоритета и категорий
6. **✅ Include testing requirements** для новых features
7. **Начинаем работу ТОЛЬКО после** создания Issue

### Во время работы:
- **Обновляем прогресс** в комментариях к Issue
- **Отмечаем выполненные** чек-поинты в description
- **✅ Добавляем результаты test webhook testing** и валидации
- **Документируем найденные проблемы** и их решения
- **Обновляем timeline** если требуется больше времени

### Закрытие Issue:
- **Все критерии приемки выполнены** (checklist в Issue)
- **✅ Изменения протестированы через test webhook approach** (ссылки на результаты)
- **Документация обновлена** (если требовалось)
- **Коммит содержит** `fixes #N`, `closes #N` или `resolves #N`
- **Результат задокументирован** в комментариях

## 📊 Labels и категоризация

### Типы Issues:
- `🐛 bug` - ошибки и неисправности
- `✨ enhancement` - улучшения функций
- `🔧 workflow` - изменения в workflow
- `📚 documentation` - задачи по документации
- `🧪 testing` - тестовые задачи
- `🏗️ architecture` - архитектурные изменения

### Приоритеты:
- `🔴 critical` - критические проблемы (блокируют работу)
- `🟡 high` - высокий приоритет (важные функции)
- `🟢 medium` - средний приоритет (улучшения UX)
- `⚪ low` - низкий приоритет (nice to have)

### Environments:
- `🔄 dev` - относится к DEV окружению
- `🚀 prod` - относится к PROD окружению
- `✅ test-webhook` - связано с test webhook approach
- `🌐 языковая-политика` - language compliance issues

### Specific Components:
- `🤖 ai-deepseek` - AI Deepseek workflow issues
- `🔗 fmp-router` - FMP Router workflow issues
- `⚡ urgent` - требует немедленного внимания
- `🛠️ cicd` - CI/CD pipeline issues

## ⚠️ Исключения и особые случаи

### Экстренные ситуации:
- При **критических ошибках в PROD** - сначала исправляем, потом создаем Issue
- **Hot fixes** - создаем Issue post-factum с меткой `🚨 hotfix`

### Batch операции:
- **Множественные похожие изменения** можно объединить в один Issue
- **Рефакторинг нескольких workflow** - один Issue с детальным планом
- **✅ Testing approach migration** - один Issue для complete methodology change

### Dependency Issues:
- **Блокирующие задачи** должны быть явно указаны через `blocks #N`
- **Связанные Issues** отмечаем через `relates to #N`
- **✅ Superseding issues** - когда новый approach замещает старый

### **✅ Testing Approach Transition:**
- **Legacy approach deprecation** - Issues для phasing out старых методов
- **New approach implementation** - Issues для внедрения test webhook approach
- **Migration coordination** - Issues для coordinating transition between approaches

## 🤖 Integration с AI Agent Execution Protocol

### **Issues Management как Mandatory Action Type:**
- **Create Issues** - в Planning/Propose phases для новых задач
- **Update Issues** - в Execute phase для progress tracking
- **Close Issues** - в Document phase при completion

### **Execution Flow Integration:**
```
Planning Phase → Assess Issues Impact → Create necessary Issues
Propose Phase → Include Issues Management в proposal
Execute Phase → Update Issues with progress
Document Phase → Close completed Issues, update related Issues
```

### **Team Collaboration через Issues:**
- **Progress Communication** - все status updates в Issue comments
- **Cross-references** - linking related Issues через #N
- **Knowledge Sharing** - результаты и lessons learned в Issues

### **✅ Testing Integration Requirements:**
- **Include test webhook requirements** в feature Issues
- **Document testing methodology** в architectural Issues
- **Track parent-child workflow issues** separately
- **Link testing Issues** to corresponding feature/bug Issues

---

## 🎯 Цель протокола

Этот протокол обеспечивает:
- **Прозрачность** всех изменений в проекте
- **Документирование** архитектурных решений
- **Контроль качества** через review process
- **✅ Testing methodology tracking** через structured Issues
- **Историю изменений** для troubleshooting
- **Планирование** и приоритизацию задач
- **Team collaboration** через structured communication
- **Consistent naming** для лучшей navigation и фильтрации
- **Совместимость с GitHub Actions** через правильную категоризацию
- **✅ Language policy compliance** через appropriate labels и descriptions

**Следование протоколу обязательно для всех участников проекта, включая AI агентов. Issues management является integral частью AI Agent Execution Protocol и поддерживает новый Test Webhook - Test Execution подход.**