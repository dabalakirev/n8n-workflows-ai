# DEV Workflows

Эта папка содержит DEV версии n8n workflows для разработки и тестирования.

## Характеристики DEV workflows:
- **2 триггера**: Manual Trigger + Execute Workflow Trigger
- **Тестирование**: Автоматически тестируются через Test Orchestrator
- **Окружение**: Разработка и отладка
- **Названия**: Суффикс `-dev` в имени

## Список workflows:
- `ai-deepseek-dev.json` - AI агент с DeepSeek для финансового анализа
- `fmp-router-dev.json` - API роутер для Financial Modeling Prep

## Использование:
1. Импортировать в DEV проект n8n
2. Настроить credentials
3. Тестировать через Test Orchestrator
4. После валидации мигрировать в PROD
