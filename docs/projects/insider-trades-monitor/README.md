# Insider Trades Monitor - Project Documentation

## 🎯 Project Overview

**Automated financial data processing system** для мониторинга инсайдерских сделок с AI-аналитикой и публикацией в Telegram канале.

### 📋 Business Objective
Каждые 60 минут автоматически:
1. Собирать новые инсайдерские сделки через FMP API
2. Создавать/обновлять карточки в MongoDB
3. Генерировать AI-опросы через DeepSeek
4. Создавать статьи в Telegraph
5. Публиковать в Telegram канал с форматированными данными

## 🏗️ Technical Architecture

**Parent Workflow:** `Insider Trades Monitor` (60min cron + Test Webhook)
```
┌─ Stage 1: FMP Data Collection & MongoDB Updates
├─ Stage 2: DeepSeek AI Survey Generation  
├─ Stage 3: Telegraph Article Creation
├─ Stage 4: Telegram Channel Publishing
└─ Status Management (New/Renew → Old)
```

## 📊 Data Structures

### MongoDB Schema Examples

#### Deals Collection (trades.deals)
```json
{
  "Trade_status": "New",
  "Symbol": "AAPL", 
  "Company name": "Apple Inc.",
  "Company Marketcap": 3500000000000,
  "Industry": "Consumer Electronics",
  "Chart": "https://images.weserv.nl/?url=finviz.com/chart.ashx%3Ft%3DAAPL",
  "Company about": "Designs and sells smartphones, computers and services.",
  "Trades": [
    {
      "Insider_name": "Tim Cook",
      "Role": "CEO", 
      "Filling_date": "2025-07-15",
      "Deal_date": "2025-07-10",
      "Price": 225.3,
      "Value": 1500000,
      "Code": "P",
      "Ownership type": "Direct",
      "SEC_link": "https://www.sec.gov/ixviewer/doc?action=aapl-20250710"
    }
  ]
}
```

#### Surveys Collection (trades.surveys)
```json
{
  "symbol": "NVDA",
  "polled_at": "2025-09-01T09:00:00Z",
  "qa": [
    { 
      "q": "Чем зарабатывает компания?", 
      "a": "Продажи GPU и платформ для дата-центров, сетевые решения и программный стек для ИИ." 
    },
    { 
      "q": "Ключевые риски?", 
      "a": "Зависимость от спроса в ЦОД, ограничения экспорта и усиление конкуренции." 
    },
    { 
      "q": "Драйверы роста в ближайший год?", 
      "a": "Массовое внедрение ИИ, развитие сетей и софта поверх аппаратуры." 
    },
    { 
      "q": "Что важно знать инвестору сейчас?", 
      "a": "Сильный бэклог заказов, но возможна волатильность из-за цикла модернизации ЦОД." 
    }
  ],
  "tokens_used": 1820,
  "cost_usd": 0.09
}
```

## 🔌 API Specifications

### FMP API Endpoints
- **Insider Latest Trades:** `https://financialmodelingprep.com/stable/insider-trading/latest?page=0&limit=100`
- **Company Profile:** `https://financialmodelingprep.com/stable/profile?symbol=AAPL`

### DeepSeek AI Integration
- **Cost Target:** <$0.05 per survey
- **Pricing:** $0.56/million INPUT tokens, $1.68/million OUTPUT tokens
- **Response Limit:** ≤1000 chars per answer

### Telegraph Integration
- **Credential:** "Telegraph API" 
- **Article Structure:** Company + ticker title, paragraph per question

### Telegram Integration
- **Credential:** "Telegram API"
- **Channel ID:** 3049635154
- **Features:** Chart preview, inline "ПОДРОБНЕЕ" button

## 🔄 Business Logic

### Session Management
- **Session:** One workflow execution = одна сессия
- **Duplicate Detection:** проверка против 30 последних карточек

### Status Logic
- **New:** первое обнаружение компании
- **Renew:** повторное обнаружение в новой сессии  
- **Old:** после публикации в Telegram

### Publishing Filter
- **Input:** Only New + Renew cards → Telegram
- **Result:** Status New/Renew → Old

## 🎫 Development Issues

Планируется разбивка на 12 Issues в 4 фазах:

### Phase 1: Core Data Pipeline (3 Issues)
- FMP API Integration & Data Processing  
- MongoDB Operations & Data Management
- Data Pipeline Validation

### Phase 2: AI Integration & Content Generation (3 Issues)
- DeepSeek AI Survey System
- Telegraph Article Generation
- AI & Content Pipeline Testing

### Phase 3: Publishing & System Integration (3 Issues)  
- Telegram Channel Publishing
- Complete System Assembly & Orchestration
- End-to-End System Validation

### Phase 4: Operations & Documentation (3 Issues)
- Logging & Monitoring System
- Complete Project Documentation  
- Deployment & Production Readiness

## 📊 Success Criteria

**✅ System считается complete когда:**
- ✅ 60-minute automation работает стабильно
- ✅ FMP API integration с правильной фильтрацией
- ✅ MongoDB operations с status management
- ✅ DeepSeek AI surveys с cost tracking <$0.05
- ✅ Telegraph articles generation working
- ✅ Telegram publishing с formatting + buttons
- ✅ Status transitions New → Renew → Old
- ✅ Comprehensive testing через MCP Webhook
- ✅ Complete documentation
- ✅ Production deployment ready

---

*Created: September 2, 2025*  
*Parent Issue: #33*  
*Status: Setup Phase*