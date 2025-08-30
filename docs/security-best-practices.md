# Security Best Practices

## 🔑 Credentials

**NEVER:**
- ❌ Hardcode credentials in workflows/code  
- ❌ Commit secrets to Git
- ❌ Share credentials in plain text

## 🌐 API Security

**Essential Rules:**
- ✅ HTTPS only for all API calls
- ✅ Validate all inputs before processing
- ✅ Implement rate limiting in workflows
- ✅ Use strong authentication (OAuth 2.0, API keys)

## 🎫 GitHub Security

**Repository Protection:**
- ❌ Never commit credentials/secrets
- ✅ Use .gitignore for sensitive files  
- ✅ Enable branch protection on main
- ✅ Require code reviews before merge

## 🤖 AI Agent Security

**Data Protection:**
- ✅ Minimize data sent to AI systems
- ✅ Scrub sensitive data from prompts
- ✅ Validate AI outputs before use
- ✅ Implement session timeouts

## 🚨 Incident Response

**If Security Incident:**
1. **Stop** - Contain the incident immediately
2. **Assess** - Determine scope and impact  
3. **Rotate** - Change all potentially compromised credentials
4. **Document** - Log everything for analysis
5. **Review** - Update security measures

## ✅ Security Checklist

**Before Deployment:**
- [ ] No hardcoded credentials
- [ ] All APIs use HTTPS
- [ ] Input validation implemented
- [ ] Secrets properly stored
- [ ] Access permissions minimal

---

**Key Principle:** **Security by Default** - secure first, optimize later.