# FMP API Reference - First Bird Project

**Financial Modeling Prep API** integration reference для проекта First Bird

## 🔗 API Overview

**Base URL:** `https://financialmodelingprep.com`  
**Authentication:** API Key required  
**Rate Limits:** Зависит от subscription plan  
**Documentation:** [financialmodelingprep.com/developer/docs](https://financialmodelingprep.com/developer/docs)

## 🛠️ Supported Endpoints

### **1. Insider Trading - Latest**
**Command:** `Insider.Trading.Latest`  
**Endpoint:** `/stable/insider-trading/latest`  
**Method:** GET

**Parameters:**
- `page` (optional): Page number для pagination
- `limit` (optional): Number of records to return

**Example Request:**
```json
{
  "toolName": "Insider.Trading.Latest",
  "params": {
    "page": 1,
    "limit": 10
  }
}
```

**Response Data:**
- Transaction details (buy/sell)
- Company information
- Insider name и title  
- Transaction date и amounts
- Stock price information

### **2. Insider Trading - By Reporting Name**
**Command:** `Insider.Trading.ReportingName`  
**Endpoint:** `/stable/insider-trading/reporting-name`  
**Method:** GET

**Parameters:**
- `name` (required): Insider name для search

**Example Request:**
```json
{
  "toolName": "Insider.Trading.ReportingName", 
  "params": {
    "name": "Elon Musk"
  }
}
```

**Use Cases:**
- Track specific executive transactions
- Monitor insider activity patterns
- Research individual trading behavior

### **3. Insider Trading - Company Search**
**Command:** `Insider.Trading.Search`  
**Endpoint:** `/stable/insider-trading/search`  
**Method:** GET

**Parameters:**
- `symbol` (required): Company ticker symbol
- `page` (optional): Page number для pagination  
- `limit` (optional): Number of records to return

**Example Request:**
```json
{
  "toolName": "Insider.Trading.Search",
  "params": {
    "symbol": "AAPL", 
    "page": 1,
    "limit": 20
  }
}
```

**Use Cases:**
- Company-specific insider analysis
- Historical trading pattern research
- Investment decision support

### **4. Company Profile**
**Command:** `Company.Profile`  
**Endpoint:** `/stable/profile`  
**Method:** GET

**Parameters:**
- `symbol` (required): Company ticker symbol

**Example Request:**
```json
{
  "toolName": "Company.Profile",
  "params": {
    "symbol": "MSFT"
  }
}
```

**Response Data:**
- Company name и description
- Industry и sector classification
- Market capitalization
- Contact information
- Business overview

## 🔧 Router Implementation

### **Routing Table:**
```javascript
const routingTable = {
  'Insider.Trading.Latest': { path: '/stable/insider-trading/latest', paramIn: 'query' },
  'Insider.Trading.ReportingName': { path: '/stable/insider-trading/reporting-name', paramIn: 'query' },
  'Insider.Trading.Search': { path: '/stable/insider-trading/search', paramIn: 'query' },
  'Company.Profile': { path: '/stable/profile', paramIn: 'query' }
};
```

### **Authentication Handling:**
```javascript
// API key автоматически добавляется к каждому запросу
params.apikey = $credentials.fmpApiKey;
```

### **URL Construction:**
```javascript
// Query parameters автоматически encoded
const queryParts = [];
for (const k in params) {
  if (params[k] !== undefined && params[k] !== null) {
    queryParts.push(encodeURIComponent(k) + '=' + encodeURIComponent(params[k]));
  }
}
finalUrl += '?' + queryParts.join('&');
```

## 📊 API Response Formats

### **Insider Trading Response:**
```json
[
  {
    "filingDate": "2024-01-15",
    "transactionDate": "2024-01-12", 
    "reportingName": "John Smith",
    "typeOfOwner": "Director",
    "securityName": "Common Stock",
    "symbol": "AAPL",
    "transactionType": "Buy",
    "sharesOwned": 1000,
    "pricePerShare": 150.25,
    "totalValue": 150250
  }
]
```

### **Company Profile Response:**
```json
[
  {
    "symbol": "AAPL",
    "companyName": "Apple Inc.", 
    "industry": "Consumer Electronics",
    "sector": "Technology",
    "description": "Apple Inc. designs, manufactures...",
    "ceo": "Tim Cook",
    "employees": 164000,
    "city": "Cupertino",
    "state": "California",
    "country": "United States"
  }
]
```

## ⚠️ Error Handling

### **Common Error Scenarios:**

#### **Invalid API Key:**
```json
{
  "Error Message": "Invalid API key. Please retry or visit our documentation to create one FREE https://financialmodelingprep.com/developer/docs"
}
```

#### **Invalid Symbol:**
```json
{
  "Error Message": "Invalid symbol"
}
```

#### **Rate Limit Exceeded:**
```json
{
  "Error Message": "API calls limit reached. Please upgrade your plan or wait until the next period."
}
```

### **Router Error Handling:**
```javascript
if (!route) {
  throw new Error(`Ошибка: Команда "${toolName}" не найдена в таблице маршрутизации.`);
}

if (!apiKey) {
  throw new Error('FMP API Key не настроен. Создайте credential "FMP API Key" в n8n.');
}
```

## 🔐 Security Best Practices

### **API Key Management:**
- **Never hardcode** API keys в workflow files
- **Use n8n credentials** для secure key storage
- **Rotate keys** regularly для security
- **Monitor usage** для unexpected activity

### **Data Protection:**
- **Financial data** processed но не stored long-term
- **Temporary processing** только в memory during execution
- **No logging** sensitive financial information
- **Secure transmission** через HTTPS only

## 📈 Performance Optimization

### **API Efficiency:**
- **Pagination** для large datasets
- **Appropriate limits** prevent timeout issues
- **Caching** where applicable (future enhancement)
- **Batch requests** when possible

### **Rate Limiting:**
- **Monitor usage** против subscription limits
- **Implement delays** если approaching limits
- **Error recovery** для rate limit scenarios
- **Usage tracking** для cost management

## 🧪 Testing Procedures

### **Endpoint Testing:**
```json
// Test data для каждого endpoint
{
  "Insider.Trading.Latest": { "limit": 5 },
  "Insider.Trading.ReportingName": { "name": "Elon Musk" },
  "Insider.Trading.Search": { "symbol": "AAPL", "limit": 5 },
  "Company.Profile": { "symbol": "MSFT" }
}
```

### **Validation Criteria:**
- **Response structure** matches expected format
- **Data types** correct для each field
- **Required fields** present в response
- **Error handling** proper для invalid inputs

### **Test Automation:**
- **DEV workflows** contain test triggers
- **Test Orchestrator** integration for automated testing
- **Response validation** через automated checks
- **Performance monitoring** response times

## 🔄 Extension Guidelines

### **Adding New Endpoints:**

1. **Update Routing Table:**
```javascript
'New.Endpoint.Command': { path: '/stable/new-endpoint', paramIn: 'query' }
```

2. **Document Parameters:**
```markdown
### **New Endpoint**
**Command:** `New.Endpoint.Command`
**Parameters:** 
- `param1` (required): Description
```

3. **Add Test Cases:**
```json
{
  "toolName": "New.Endpoint.Command",
  "params": { "param1": "test_value" }
}
```

4. **Update AI Agent Description:**
- Add command to AI Agent tool description
- Include parameter requirements
- Provide usage examples

### **Maintenance:**
- **Regular testing** всех endpoints
- **Documentation updates** для API changes
- **Error monitoring** для new issues
- **Performance tracking** для optimization

---

**Этот API reference обеспечивает complete coverage FMP integration для First Bird project с focus на security, performance, и maintainability.**

*Last Updated: August 2025 - Issue #21 Project-Centric Architecture*