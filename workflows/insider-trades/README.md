# Insider Trades Project - Workflows

**🎯 Project Status:** IN DEVELOPMENT  
**📊 Implementation Progress:** Block 1/5 Complete (3/25 nodes)  
**🔧 Current Workflow:** Insider Trades DEV (`QrzH7RPCQyqBVYbn`)

---

## 📁 Project Structure

```
workflows/insider-trades/
├── dev/                    # DEV workflows (current development)
├── prod/                   # PROD workflows (future deployment)
└── README.md              # This file - project workflow guide
```

---

## 🚀 Current Implementation Status

### ✅ **Block 1: Data Collection & Filtering** - COMPLETE (3/25 nodes)

**Workflow:** Insider Trades DEV (`QrzH7RPCQyqBVYbn`)  
**Status:** Created, requires manual activation

**Implemented Nodes:**
- **Node 1:** Cron Schedule - 60-minute cycle automation
- **Node 2:** FMP Latest Insider Trading - Financial data collection  
- **Node 3:** Filter Trades - P-Purchase + Common Stock filtering
- **Test Webhook** - Validation integration ready

### 🔄 **Next Implementation Phases**

**Block 2: Database Operations** - MongoDB integration (nodes 5-12)  
**Block 3: AI Analysis** - DeepSeek + SerpApi (nodes 13-17)  
**Block 4: Content Publishing** - Telegraph + Telegram (nodes 18-23)  
**Block 5: State Management** - Cycle completion (nodes 24-25)

---

## 🔧 Development Workflow

### **Incremental Development:**
- **Max 3 nodes per iteration** - following Incremental Testing Protocol
- **Test webhook integration** - each block validated through parent workflow
- **Progressive architecture** - block-by-block до complete 25-node system

### **Testing Strategy:**
- **MCP Webhook Testing** - validation через parent workflow Test Webhook
- **Manual activation** - workflows require human activation before testing
- **End-to-end validation** - complete data flow testing

---

## 📊 Complete Architecture Reference

**Total Architecture:** 25 nodes в 5 logical blocks  
**External APIs:** 6 integrations (FMP, MongoDB, DeepSeek, SerpApi, Telegraph, Telegram)  
**Automation Cycle:** 60-minute Cron-based automation

### **Architecture Documentation:**
- **[Level 3: Complete Architecture](../../docs/projects/insider-trades/architecture.md)** - Master architecture overview
- **[Technical Brief](../../docs/projects/insider-trades/technical-brief.md)** - Detailed technical specifications
- **[Brief Idea](../../docs/projects/insider-trades/brief-idea.md)** - Business concept and logic

---

## 🎯 Next Steps

1. **Manual Activation** - activate Insider Trades DEV workflow в n8n UI
2. **Block 1 Testing** - validate data collection через webhook testing
3. **Block 2 Implementation** - MongoDB operations и card management
4. **Progressive Development** - continue block-by-block до completion

---

**🔄 Last Updated:** September 3, 2025  
**📋 Development Status:** Block 1 complete, waiting activation for testing  
**🎯 Next Milestone:** Block 2 Database Operations implementation