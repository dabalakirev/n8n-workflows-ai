# Insider Trades - Credentials Reference

**🎯 НАЗНАЧЕНИЕ:** Точные credential IDs и names для разработки Insider Trades workflows через n8n MCP

**📅 СОЗДАН:** September 2, 2025  
**🔄 ИСТОЧНИК:** N8N Workflow "Credentials id" (ID: gQuaypHWo7fUsHWi)

---

## 🔐 **VERIFIED CREDENTIALS LIST**

### **1. Telegram Bot API**
```json
"credentials": {
  "telegramApi": {
    "id": "IPk73kQxS5AUJ1Ni",
    "name": "Telegram API"
  }
}
```
- **Node Type:** `n8n-nodes-base.telegramTrigger`, `n8n-nodes-base.telegram`
- **Usage:** Block 4 (Telegram publishing)
- **Channel ID:** `3049635154`

### **2. MongoDB Connection**
```json
"credentials": {
  "mongoDb": {
    "id": "Jb779SAaphmHAOGs", 
    "name": "MongoDB account"
  }
}
```
- **Node Type:** `n8n-nodes-base.mongoDb`
- **Usage:** Blocks 2,3,4,5 (Database operations)
- **Collections:** `deals`, `surveys`

### **3. Telegraph API**
```json
"credentials": {
  "httpQueryAuth": {
    "id": "O5WldXH0xHIjyQgD",
    "name": "Telegraph API"
  }
}
```
- **Node Type:** `n8n-nodes-base.httpRequest`
- **Usage:** Block 4 (Content publishing)
- **API:** `https://api.telegra.ph/`

### **4. SerpAPI Google Search**
```json
"credentials": {
  "serpApi": {
    "id": "75EBIHKM5Q7jnT86",
    "name": "SerpAPI account"
  }
}
```
- **Node Type:** `n8n-nodes-serpapi.serpApi`, `@n8n/n8n-nodes-langchain.toolSerpApi`
- **Usage:** Block 3 (AI Agent web search)
- **Integration:** AI Agent → SerpApi Tool

### **5. FMP API (Existing)**
```json
"credentials": {
  "httpQueryAuth": {
    "id": "k887gSxTZZEgRYIa",
    "name": "FMP API"
  }
}
```
- **Node Type:** `n8n-nodes-base.httpRequest`
- **Usage:** Blocks 1,2 (Financial data collection)
- **API:** `https://financialmodelingprep.com/`

### **6. DeepSeek API (Existing)**
```json
"credentials": {
  "deepSeekApi": {
    "id": "sFuzOe0ydJ9CEn0H",
    "name": "DeepSeek API"
  }
}
```
- **Node Type:** `@n8n/n8n-nodes-langchain.lmChatDeepSeek`
- **Usage:** Block 3 (AI Agent language model)
- **Integration:** AI Agent → DeepSeek Chat Model

---

## 🛠️ **DEVELOPMENT USAGE**

### **При создании workflows через n8n MCP:**

**Используйте точные credential references:**
```javascript
// Пример для MongoDB node
const mongoNode = {
  "type": "n8n-nodes-base.mongoDb",
  "credentials": {
    "mongoDb": {
      "id": "Jb779SAaphmHAOGs",
      "name": "MongoDB account"
    }
  }
  // ... остальная конфигурация
};
```

### **Credential Mapping по блокам:**

**Block 1: Data Collection**
- FMP API (`k887gSxTZZEgRYIa`) - Financial data

**Block 2: Database Operations** 
- MongoDB (`Jb779SAaphmHAOGs`) - Card management
- FMP API (`k887gSxTZZEgRYIa`) - Company profiles

**Block 3: AI Analysis**
- MongoDB (`Jb779SAaphmHAOGs`) - Survey storage
- DeepSeek (`sFuzOe0ydJ9CEn0H`) - Language model
- SerpAPI (`75EBIHKM5Q7jnT86`) - Web search

**Block 4: Content Publishing**
- MongoDB (`Jb779SAaphmHAOGs`) - Content queries  
- Telegraph (`O5WldXH0xHIjyQgD`) - Article creation
- Telegram (`IPk73kQxS5AUJ1Ni`) - Channel publishing

**Block 5: State Management**
- MongoDB (`Jb779SAaphmHAOGs`) - Status updates

---

## ⚠️ **IMPORTANT NOTES**

### **Credential Security:**
- ✅ **IDs are not sensitive** (per n8n documentation)
- ✅ **Names can be descriptive** for easier identification
- ❌ **Never expose actual API keys** in workflow JSON

### **Development Process:**
1. **Use exact IDs** from this reference
2. **Match node types** с credential types  
3. **Verify credential names** match n8n instance
4. **Test connectivity** before full workflow deployment

### **Credential Verification:**
```bash
# Через n8n MCP можно создать test nodes для проверки credentials
n8n_create_workflow({
  name: "Credential Test",
  nodes: [/* node with credential reference */]
})
```

---

## 🔄 **MAINTENANCE**

**Обновление при изменениях:**
- При создании новых credentials в n8n → обновить этот файл
- При rotation API keys → credential IDs остаются теми же
- При migration n8n instance → потребуется новый credential mapping

**Источник проверки:**
N8N Workflow "Credentials id" содержит все actual credential references для verification.

---

*Last verified: September 2, 2025*  
*Workflow source: gQuaypHWo7fUsHWi*