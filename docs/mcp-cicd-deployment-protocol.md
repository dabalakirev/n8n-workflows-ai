# Simplified MCP CI/CD Protocol

## ⚠️ ОБЯЗАТЕЛЬНЫЙ ПРОТОКОЛ
Упрощенный CI/CD процесс для n8n workflow разработки с unified Developer-Tester ролью и incremental подходом.

## 🎯 Цель
Streamlined разработка n8n workflows через MCP с built-in testing и architecture validation.

---

## 📚 Documentation Dependencies

### **🔧 ОБЯЗАТЕЛЬНЫЕ ПЛАТФОРМЕННЫЕ ПРОТОКОЛЫ:**
- **[AI Agent Execution Protocol](docs/ai-agent-execution-protocol.md)** - 5-step workflow для всех задач
- **[AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)** - Role definitions (Developer роль)
- **[MCP Webhook Testing Guide](docs/mcp-webhook-testing-guide.md)** - Testing procedures
- **[GitHub Issues Protocol](docs/github-issues-protocol.md)** - Issue management

### **📋 PROJECT-SPECIFIC ДОКУМЕНТАЦИЯ:**
- **Architecture Overview** - `docs/projects/[project]/architecture.md`
  - **⚠️ ВАЖНО:** Из architecture.md найти нужный блок и читать ТОЛЬКО его
  - НЕ загружать всю архитектуру в context одновременно
- **Credentials Reference** - `docs/projects/[project]/credentials-reference.md`

### **🔍 n8n PLATFORM DOCUMENTATION:**
- **n8n Node Documentation** - через MCP `get_node_documentation(nodeType)`
- **Validate configuration** - `validate_node_operation(nodeType, config)`

---

## 🎭 Developer-Tester Role

### **UNIFIED RESPONSIBILITIES:**
- **Verify architecture** против n8n documentation перед началом
- **Develop minimal node groups** (1-3 nodes max)
- **Test each group** immediately после creation
- **Document progress** в Issue comments

---

## 🚨 Architecture Issue Escalation

**ЕСЛИ обнаружены проблемы в architecture:**

1. **🛑 STOP Development** - документировать проблему в Issue
2. **📝 Request Approval** для изменения architecture
3. **⏳ Wait for Approval** перед продолжением
4. **✅ Update Architecture** после одобрения

**Issue Comment Format:**
```markdown
## ⚠️ ARCHITECTURE ISSUE
**Problem:** [technical issue]
**Proposed Solution:** [brief description]
**Requesting approval** to proceed
```

---

## 🔄 Development Workflow

### **PROCESS:**
1. **Read architecture.md** - найти нужный блок для task
2. **Validate architecture** против n8n documentation
3. **Create minimal node group** (1-3 nodes)
4. **Test via webhook** immediately
5. **Document progress** в Issue comments
6. **Clean temporary nodes** (keep input webhook)
7. **Repeat** для next group

---

## 📝 Development Journal

**ОБЯЗАТЕЛЬНО документировать в Issue comments:**

**Session Start:**
```markdown
🚀 **Development Session**
Target: [node group]
Plan: [brief plan]
```

**Progress:**
```markdown
✅ **Progress Update**  
Completed: [achievements]
Next: [next steps]
Notes: [important details]
```

**Issues:**
```markdown
⚠️ **Problem Found**
Issue: [description] 
Solution: [what you did]
```

---

## 🚨 Critical Rules

- **NO architecture changes без approval**
- **ALWAYS test each node group immediately**  
- **Document progress в Issue comments**
- **Read ONLY нужный architecture block**
- **Clean temporary nodes after testing**

---

*Protocol ensures systematic n8n workflow development с built-in quality controls и streamlined developer experience.*