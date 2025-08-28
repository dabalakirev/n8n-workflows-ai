# 📝 n8n Workflows AI

**Description**: N8N TDAD - Test Driven AI Development workflows

## 🏗️ **Project Structure**

```
workflows/
├── dev/                    # Development versions (2 triggers each)
│   ├── ai-deepseek-dev.json      (Manual + Execute Workflow)
│   └── fmp-router-dev.json       (Manual + Execute Workflow)
├── prod/                   # Production versions (1 trigger each)  
│   ├── ai-deepseek-prod.json     (Manual only)
│   └── fmp-router-prod.json      (Manual only)
└── README.md              # This file
```

## 🚀 **Workflow Types**

### **AI Deepseek Workflows**
- **Purpose**: AI-powered analysis and automation
- **DEV**: Manual trigger + Execute Workflow (for testing)
- **PROD**: Manual trigger only (for production use)

### **FMP Router Workflows**  
- **Purpose**: Financial data routing and processing
- **DEV**: Manual trigger + Execute Workflow (for testing)
- **PROD**: Manual trigger only (for production use)

## 🔐 **Security**

All workflows use n8n credential references instead of hardcoded API keys:
- **FMP API**: Uses `fmpApiKey` credential reference
- **No hardcoded secrets** in JSON files

## ✅ **GitHub Actions Validation**

Project includes automated validation via `.github/workflows/validate-workflows.yml`:
- **JSON syntax validation** 
- **Trigger count verification** (DEV=2, PROD=1)
- **Security scanning** (no hardcoded keys)
- **Structure compliance** checks

## 🛠️ **Usage**

1. **Import workflows** into your n8n instance
2. **Configure credentials** in n8n (fmpApiKey, etc.)
3. **Use DEV versions** for testing with Test Orchestrator
4. **Use PROD versions** for production deployment

---

*Updated: 28.08.2025 - Issue #15 HOTFIX Complete*