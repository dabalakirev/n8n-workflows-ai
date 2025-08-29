# First Bird - Project Workflows

**Financial Data Automation** workflows для проекта First Bird

## 🐦 Обзор проекта

First Bird - пилотный проект платформы n8n-workflows-ai, демонстрирующий автоматизацию работы с финансовыми данными через Financial Modeling Prep API и AI анализ.

## 📋 Workflows проекта

### 🤖 **AI Deepseek** 
**Файлы:**
- `dev/ai-deepseek-dev.json` - DEV версия с тестовыми триггерами
- `prod/ai-deepseek-prod.json` - PROD версия только с Manual Trigger

**Назначение:** AI Agent для анализа финансовых данных с использованием DeepSeek language model

**Возможности:**
- Обработка естественных запросов на финансовую тематику
- Интеграция с FMP API Router для получения данных
- Intelligent анализ и агрегация финансовой информации
- AI-powered insights и recommendations

**DEV особенности:**
- Manual Trigger для ручного тестирования
- Execute Workflow Trigger для автоматизированного testing через Test Orchestrator
- Тестовые pinned data для быстрой проверки функциональности

### 🔗 **FMP API Router**
**Файлы:**
- `dev/fmp-router-dev.json` - DEV версия с тестовыми триггерами
- `prod/fmp-router-prod.json` - PROD версия только с Manual Trigger

**Назначение:** Universal router для Financial Modeling Prep API endpoints

**Поддерживаемые команды:**
- `Insider.Trading.Latest` - последние сделки инсайдеров
- `Insider.Trading.ReportingName` - сделки конкретного инсайдера
- `Insider.Trading.Search` - сделки по компании
- `Company.Profile` - информация о компании

**Архитектура:**
- Routing Table для динамического mapping команд на API endpoints
- Автоматическое добавление API ключа к запросам
- Error handling и validation входных параметров
- Support для query и path parameters

## 🏗️ Архитектура проекта

### DEV Environment
```
DEV workflows содержат:
├── Manual Trigger          # Ручное тестирование и debugging
├── Execute Workflow Trigger # Автоматизированное testing
└── Основная логика         # Identical с PROD версией
```

### PROD Environment  
```
PROD workflows содержат:
├── Manual Trigger только   # Production stability
└── Основная логика        # Optimized для production use
```

## 🧪 Testing Strategy

### DEV Testing
- **Manual Testing:** Использовать Manual Trigger с pinned test data
- **Automated Testing:** Execute Workflow Trigger интеграция с Test Orchestrator
- **Integration Testing:** AI Deepseek → FMP API Router data flow validation

### Testing Scenarios
1. **AI Deepseek DEV:** Тестовые financial queries и response validation
2. **FMP Router DEV:** Каждый supported endpoint с различными параметрами
3. **Integration Flow:** End-to-end testing AI Agent + API Router workflows

## 🚀 Deployment Process

### DEV → PROD Migration
1. **Test в DEV:** Убедиться что все tests проходят
2. **Validate Configuration:** Проверить credentials и settings
3. **Deploy в PROD:** Import JSON файлов в production n8n
4. **Production Testing:** Manual validation в production environment

## 🔧 Configuration Requirements

### Credentials needed:
- **DeepSeek API:** Для AI language model functionality
- **FMP API Key:** Для Financial Modeling Prep data access

### n8n Requirements:
- **@n8n/n8n-nodes-langchain** package для AI functionality
- **n8n-nodes-base** для core workflow nodes

## 📊 Performance Metrics

### Expected Performance:
- **AI Deepseek response time:** 2-5 seconds для typical queries
- **FMP API Router:** < 2 seconds для data retrieval
- **End-to-end processing:** 3-7 seconds для full AI analysis

### Monitoring:
- Response time tracking через n8n execution logs
- Error rate monitoring для production stability
- API rate limiting awareness для FMP endpoints

## 🔗 Integration Points

### Platform Integration:
- **Test Orchestrator:** Automated testing для всех DEV workflows
- **GitHub Actions:** CI/CD pipeline для workflow validation
- **Platform Documentation:** Cross-references к universal protocols

### Future Projects:
- Router architecture reusable для других API integrations
- AI Agent pattern applicable для различных domains
- Testing framework universal для любых project workflows

---

**Это project-specific документация для First Bird workflows. Для platform-level информации смотрите основную документацию в корне repository.**