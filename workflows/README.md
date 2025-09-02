# n8n Workflows - Project-Centric Architecture

**Project-focused workflow management** для n8n-workflows-ai platform.

## 🎯 **Project-Centric Workflow Benefits**

### **Project Isolation**
- **Clear Separation** - каждый проект в своей папке с dedicated workflows
- **Independent Development** - different domains, APIs, и business logic
- **Project-Specific Documentation** - tailored guides и technical references
- **Environment Management** - DEV/PROD separation per project

## 🚀 Current Projects

### 🐦 First Bird (Complete)
- **Domain**: Financial Data Automation  
- **Status**: ✅ DEV Complete, PROD deployed
- **Components**: AI Deepseek + FMP API Router
- **Documentation**: [first-bird/README.md](first-bird/README.md)

### 📊 Insider Trades (Implementation Ready)
- **Domain**: AI-Powered Insider Trading Analysis
- **Status**: ✅ Level 3 Architecture Complete (25 nodes, 5 blocks)
- **Components**: DeepSeek + SerpApi + Telegraph + Telegram
- **Documentation**: [insider-trades/README.md](insider-trades/README.md)

## 📋 New Project Template

### Minimum Requirements
```
workflows/your-project/
├── dev/                    # DEV workflows
│   └── workflow-dev.json   # Manual + Execute Workflow triggers
├── prod/                   # PROD workflows (future)
│   └── workflow-prod.json  # Manual trigger only
└── README.md              # Project documentation
```

### Required Documentation
- Project overview и scope
- Workflow descriptions
- Configuration guide
- Testing procedures

## 📚 **Related Documentation**

- **Platform Overview**: [../README.md](../README.md) - General platform capabilities и features
- **Platform Roadmap**: [../docs/roadmap.md](../docs/roadmap.md) - Development milestones и progress
- **Testing Strategy**: [../docs/testing-strategy.md](../docs/testing-strategy.md) - Universal testing protocols
- **AI Agent Protocols**: [../docs/ai-agent-roles-protocols.md](../docs/ai-agent-roles-protocols.md) - Development procedures
- **First Bird Project**: [first-bird/README.md](first-bird/README.md) - Complete project technical details
- **Insider Trades Project**: [insider-trades/README.md](insider-trades/README.md) - Implementation-ready architecture

*Platform supports unlimited automation projects with shared testing infrastructure и consistent quality standards.*