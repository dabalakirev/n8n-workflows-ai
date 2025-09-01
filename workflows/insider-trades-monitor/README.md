# Insider Trades Monitor

**Automated Financial Data Processing System** для мониторинга инсайдерских сделок с AI-аналитикой и публикацией в Telegram канале.

## 🎯 Project Overview

**Business Objective:** Каждые 60 минут автоматически:
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

**Data Flow:**
- **Input:** FMP API (Latest Insider Trades + Company Profile)
- **Processing:** MongoDB operations, AI surveys, content generation
- **Output:** Telegram channel с chart preview + Telegraph integration

## 📊 Technical Specifications

### APIs Integration:
- **FMP Insider Trades:** `?page=0&limit=100` filter P-Purchase, Common Stock only
- **FMP Company Profile:** по Symbol для company data
- **DeepSeek AI:** 4 configurable questions, <1000 chars/answer, <$0.05/survey
- **Telegraph:** article generation от AI survey data
- **Telegram Bot:** Channel 3049635154, image preview, inline buttons

### MongoDB Collections:
- **deals** (DB: Trades): карточки сделок с статусами New/Renew/Old
- **surveys** (DB: Trades): AI опросы с token cost tracking

### Business Logic:
- **Session Concept:** One workflow execution = одна сессия
- **Duplicate Detection:** проверка против 30 последних карточек
- **Status Logic:** 
  - `New` → первое обнаружение компании
  - `Renew` → повторное обнаружение в новой сессии
  - `Old` → после публикации в Telegram
- **Publishing Filter:** Only New + Renew cards → Telegram

## 🏗️ Project Structure

```
workflows/insider-trades-monitor/
├── dev/                    # DEV workflows [PLANNED]
├── prod/                   # PROD workflows [FUTURE]
└── README.md               # This file
```

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

## 🔗 Dependencies

**External Services:**
- FMP API (credentials configured) ✅
- DeepSeek API (credentials configured) ✅  
- Telegraph API (credentials configured) ✅
- Telegram Bot API (credentials configured) ✅
- MongoDB (credentials configured) ✅

**Platform Dependencies:**
- n8n MCP testing framework
- GitHub Issues workflow
- Standard CI/CD procedures

## 📅 Development Phases

**Phase 1 (Data Pipeline):** 3-5 working sessions  
**Phase 2 (AI Integration):** 3-4 working sessions
**Phase 3 (Publishing):** 3-4 working sessions  
**Phase 4 (Operations):** 2-3 working sessions

**Total Estimated:** 11-16 working sessions

## 🎫 Related Issues

- **Parent Issue:** [#33 - Insider Trades Automation System - Complete Implementation](https://github.com/dabalakirev/n8n-workflows-ai/issues/33)
- **Phase 1 Issues:** Will be created as development progresses

---

*Created: September 2, 2025*  
*Status: Development Setup*