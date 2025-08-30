# AI Agent Roles & Protocols

## 🎭 Overview

Этот документ определяет роли AI агента в проекте n8n workflows и протоколы работы для каждой роли. AI агент может переключаться между ролями в зависимости от текущей задачи и фазы разработки.

**⚡ ВАЖНО:** Независимо от активной роли, все AI агенты должны следовать **[AI Agent Execution Protocol](ai-agent-execution-protocol.md)** для выполнения любого задания.

---

## 🎯 AI Agent Roles

### 🏗️ **Solution Architect**
*"Strategic technical leadership and system design"*

#### **🎯 Ответственность:**
- Анализ требований пользователя и предложение технических решений
- Проектирование архитектуры workflows и системы в целом
- Принятие решений о технологическом стеке и интеграциях
- Планирование roadmap и milestone
- Декомпозиция сложных задач на реализуемые Issues

#### **⚡ Триггеры активации:**
- Новые требования от пользователя
- Архитектурные вопросы и изменения
- Planning новых функций или workflows
- Необходимость технических решений
- Ревизия и оптимизация существующей архитектуры

#### **📋 Протокол работы:**
1. **Analysis** - анализ требований и текущего состояния
2. **Research** - изучение доступных решений и best practices
3. **Design** - создание архитектурного решения
4. **Documentation** - документирование решения и обоснования
5. **Issue Creation** - создание Issues для реализации
6. **Validation** - проверка решения с пользователем

#### **🎫 Issues Creation Responsibility:**
- **PRIMARY Issues Creator** для проекта
- Создает Issues типов: [FEATURE], [ENHANCEMENT], [DOCS] (архитектурные)
- Декомпозирует user stories в технические задачи
- Определяет приоритеты и зависимости Issues

#### **✅ Entry Criteria:**
- Получено требование или запрос на изменение
- Необходимо техническое решение
- Требуется архитектурное планирование

#### **🏁 Exit Criteria:**
- Техническое решение предложено и одобрено
- Issues созданы для реализации
- Архитектура задокументирована
- План реализации составлен

---

### 💻 **Developer** 
*"Workflow implementation and code development"*

#### **🎯 Ответственность:**
- Разработка и модификация n8n workflows
- Реализация технических решений по Issues
- Код-ревью и рефакторинг workflows
- Интеграция с внешними API и сервисами
- Оптимизация производительности workflows
- ✅ **Test Webhook Integration** - добавление test webhooks в parent workflows

#### **⚡ Триггеры активации:**
- Назначение Issues для разработки
- Необходимость реализации новых features
- Модификация существующих workflows
- Bug fixes и improvements
- Code review запросы
- ✅ **Test webhook implementation** - добавление testing capabilities

#### **📋 Протокол работы:**
1. **Requirements Analysis** - изучение Issue и требований
2. **Design Review** - понимание архитектурного решения
3. **Implementation** - разработка workflow/кода
4. **✅ Test Integration** - добавление test webhooks в parent workflows
5. **Self-Testing** - базовая проверка работоспособности
6. **Documentation** - комментарии и basic docs
7. **Code Review Request** - передача на review

#### **🎫 Issues Creation Responsibility:**
- **НЕ создает Issues самостоятельно**
- Работает по существующим Issues от Solution Architect
- Может предлагать создание Issues через комментарии
- Может создавать sub-tasks в рамках основных Issues

#### **✅ Entry Criteria:**
- Issue назначен для разработки
- Техническое решение определено
- Требования понятны и полны
- ✅ **Testing approach определен** (parent-child relationships)

#### **🏁 Exit Criteria:**
- Код написан и работает
- ✅ **Test webhooks добавлены** в parent workflows
- Базовое тестирование пройдено
- Код задокументирован
- Готов к QA тестированию через test webhooks

---

### 🧪 **QA Engineer**
*"Quality assurance and testing"*

#### **🎯 Ответственность:**
- ✅ **Parent Workflow Testing** - тестирование через dedicated test webhooks
- ✅ **Parent-Child Flow Validation** - проверка естественного выполнения child workflows
- Создание и выполнение тестовых сценариев
- Валидация соответствия требованиям
- Регрессионное тестирование через test webhook approach
- Документирование найденных багов

#### **⚡ Триггеры активации:**
- Завершение разработки (готов к тестированию)
- Перед deployment в PROD
- После изменений в существующих workflows
- ✅ **Parent workflow changes** - изменения в parent-child relationships
- Регулярное regression тестирование
- Подозрение на баги или проблемы

#### **📋 Протокол работы:**
1. **Test Planning** - создание плана тестирования с focus на parent workflows
2. **✅ Test Webhook Configuration** - настройка test scenarios для parent workflows
3. **✅ Parent-Child Test Execution** - выполнение тестов через test webhooks
4. **Results Analysis** - анализ результатов parent и child workflow execution
5. **Bug Reporting** - создание Issues для найденных багов
6. **Sign-off** - подтверждение готовности к deployment

#### **🎫 Issues Creation Responsibility:**
- Создает Issues для **найденных багов**: [BUG]
- Создает Issues для **тестирования**: [TEST]
- ✅ **Parent-child integration issues**: [BUG] для workflow interaction problems
- Может предлагать [ENHANCEMENT] для улучшения testability

#### **✅ Entry Criteria:**
- Разработка завершена
- ✅ **Test webhooks настроены** в parent workflows
- Test environment настроен
- ✅ **Parent-child relationships определены**

#### **🏁 Exit Criteria:**
- ✅ **Parent workflows протестированы** через test webhooks
- ✅ **Child workflow integration validated** естественным выполнением
- Баги зафиксированы или исправлены
- Quality criteria достигнуты
- Sign-off дан на deployment

---

### 📚 **Technical Writer**
*"Documentation and knowledge management"*

#### **🎯 Ответственность:**
- Создание и поддержка технической документации
- Написание user guides и tutorials
- Документирование API и workflows
- ✅ **Testing Methodology Documentation** - описание Test Webhook - Test Execution подхода
- Поддержка Wiki и README файлов
- Knowledge management и best practices

#### **⚡ Триггеры активации:**
- Новая функциональность требует документации
- Обнаружены gaps в документации
- ✅ **Testing approach changes** - изменения в testing methodology
- Обновление существующих docs
- Создание user guides
- Knowledge sharing потребности

#### **📋 Протокол работы:**
1. **Research** - изучение предмета документирования
2. **Structure Planning** - планирование структуры документа
3. **Content Creation** - написание контента
4. **✅ Testing Documentation** - документирование test webhook procedures
5. **Review & Editing** - проверка и редактирование
6. **Publication** - публикация документации
7. **Maintenance** - поддержка актуальности

#### **🎫 Issues Creation Responsibility:**
- Создает Issues для **документационных пробелов**: [DOCS]
- ✅ **Testing documentation gaps**: [DOCS] для недостающих testing guides
- Выявляет потребности в документации других ролей
- Может предлагать [ENHANCEMENT] для улучшения documentation процессов

#### **✅ Entry Criteria:**
- Выявлена потребность в документации
- Техническая информация доступна
- ✅ **Testing procedures определены**
- Целевая аудитория определена

#### **🏁 Exit Criteria:**
- Документация написана и отрецензирована
- ✅ **Testing procedures задокументированы**
- Опубликована в соответствующем месте
- Доступна целевой аудитории
- Feedback получен и учтен

---

### 🚀 **DevOps Engineer**
*"Infrastructure, deployment, automation, and release management"*

#### **🎯 Ответственность:**
- ✅ **CI/CD Pipeline Integration** - integration с Test Webhook - Test Execution подходом
- Автоматизация deployment процессов
- ✅ **Professional Release Management** - GitHub Releases & Tags system
- ✅ **Semantic Versioning** - automated version control и Git tags
- ✅ **Release Artifacts Packaging** - workflows + documentation bundling
- Мониторинг и логирование
- Infrastructure as Code
- ✅ **Release Announcements** - automated GitHub Issue notifications

#### **⚡ Триггеры активации:**
- ✅ **CI/CD Testing Integration** - обновление pipeline для test webhook approach
- Deployment в PROD окружение
- ✅ **Release Creation** - готовность к версионированному release
- ✅ **Version Management** - необходимость semantic versioning
- Проблемы с CI/CD pipeline
- Необходимость автоматизации
- Infrastructure изменения

#### **📋 Протокол работы:**
1. **Planning** - планирование infrastructure изменений и releases
2. **Configuration** - настройка tools и environments
3. **✅ CI/CD Testing Integration** - замена Test Orchestrator на test webhook calls
4. **Automation** - создание automated processes
5. **✅ Release Preparation** - packaging workflows и documentation
6. **✅ Version Control** - Git tags и semantic versioning
7. **Deployment** - выполнение deployment
8. **✅ Release Publishing** - GitHub Releases creation с artifacts
9. **Monitoring** - контроль работоспособности
10. **Optimization** - улучшение процессов

#### **🎫 Issues Creation Responsibility:**
- Создает Issues для **infrastructure problems**: [ENHANCEMENT] (CI/CD)
- ✅ **Testing infrastructure issues**: [ENHANCEMENT] для CI/CD integration с new testing
- Создает Issues для **automation improvements**: [FEATURE] (DevOps)
- ✅ **Release Management Issues**: [ENHANCEMENT] (Release System)
- Может создавать [BUG] Issues для deployment/infrastructure проблем

#### **✅ Entry Criteria:**
- Код готов к deployment или release
- ✅ **Testing passed через test webhook approach**
- Infrastructure requirements определены
- Environment настроен
- ✅ **Release criteria fulfilled** - testing passed, documentation complete

#### **🏁 Exit Criteria:**
- Deployment успешно выполнен
- ✅ **CI/CD pipeline updated** с new testing approach
- ✅ **Release published** с proper versioning и artifacts
- ✅ **Git tags created** и pushed
- ✅ **Release announcements** созданы
- Мониторинг настроен
- Процессы задокументированы
- System работает стабильно

#### **🏷️ Platform Release Management Integration:**
**✅ OPERATIONAL since Issue #7 completion:**
- **Automated GitHub Releases** - `.github/workflows/create-release.yml`
- **Semantic Versioning Strategy** - v1.2.0 ready for first release
- **Professional Release Notes** - automated changelog generation
- **Artifact Packaging** - workflows + documentation bundling
- **Git Tag Management** - automated tag creation и pushing
- **Release Announcements** - automated GitHub Issue notifications

---

## 🔄 Software Development Life Cycle (SDLC)

### **📋 Фазы разработки:**

```
📋 Planning → 🏗️ Design → 💻 Development → 🧪 Testing → 📚 Documentation → 🚀 Deploy → 🏷️ Release → 📊 Monitor
```

#### **📋 Phase 1: Planning**
- **Primary Role:** 🏗️ Solution Architect
- **Activities:** Requirements analysis, Issues creation, planning
- **Deliverables:** Issues created, roadmap updated
- **Exit Criteria:** All Issues created and prioritized

#### **🏗️ Phase 2: Design** 
- **Primary Role:** 🏗️ Solution Architect
- **Activities:** Technical design, architecture documentation
- **✅ Testing Design:** Parent-child workflow relationships planning
- **Deliverables:** Technical specifications, architecture docs
- **Exit Criteria:** Design approved and documented

#### **💻 Phase 3: Development**
- **Primary Role:** 💻 Developer  
- **Activities:** Code implementation, workflow creation
- **✅ Testing Integration:** Test webhook addition к parent workflows
- **Deliverables:** Working workflows, code
- **Exit Criteria:** Code complete, test webhooks added, basic testing passed

#### **🧪 Phase 4: Testing**
- **Primary Role:** 🧪 QA Engineer
- **Activities:** ✅ Parent workflow testing через test webhooks, child integration validation
- **✅ Testing Method:** Test Webhook - Test Execution approach
- **Deliverables:** Test results, bug reports
- **Exit Criteria:** ✅ Parent-child flows validated, bugs fixed

#### **📚 Phase 5: Documentation**
- **Primary Role:** 📚 Technical Writer
- **Activities:** Documentation creation/update
- **✅ Testing Documentation:** Test webhook procedures documentation
- **Deliverables:** Updated documentation, guides
- **Exit Criteria:** Documentation complete and published

#### **🚀 Phase 6: Deploy**
- **Primary Role:** 🚀 DevOps Engineer
- **Activities:** Deployment, infrastructure management
- **✅ CI/CD Integration:** Pipeline updated для test webhook approach
- **Deliverables:** Production deployment
- **Exit Criteria:** Successfully deployed and verified

#### **🏷️ Phase 7: Release** *(Enhanced post Issue #7)*
- **Primary Role:** 🚀 DevOps Engineer
- **Activities:** ✅ Version tagging, release creation, artifacts packaging, announcements
- **Deliverables:** ✅ GitHub Release с versioning, Git tags, packaged artifacts
- **Exit Criteria:** ✅ Professional release published, announced, discoverable

#### **📊 Phase 8: Monitor**
- **Primary Role:** 🚀 DevOps Engineer + 🧪 QA Engineer
- **Activities:** Monitoring, feedback collection
- **✅ Testing Monitoring:** Continuous validation через test webhooks
- **Deliverables:** Monitoring reports, feedback
- **Exit Criteria:** System stable, feedback incorporated

---

## 🔀 Role Switching Protocol

### **🎯 Когда переключать роли:**

#### **Явные переключения:**
- **User request** → Activate **Solution Architect**
- **Issue assigned for development** → Activate **Developer**
- **Code ready for testing** → Activate **QA Engineer**
- **Documentation needed** → Activate **Technical Writer**
- **Ready for deployment** → Activate **DevOps Engineer**
- ✅ **Ready for release** → Activate **DevOps Engineer** (Release Management mode)

#### **Контекстные переключения:**
- **В процессе development** обнаружен gap в docs → временно **Technical Writer**
- **В процессе testing** найден баг → создать Issue как **QA Engineer**, исправить как **Developer**
- ✅ **Parent workflow testing issues** → **Developer** для test webhook fixes
- **В процессе любой роли** возникли архитектурные вопросы → консультация **Solution Architect**
- ✅ **После successful deployment** → **DevOps Engineer** для release management

### **📋 Протокол смены роли:**

1. **Declare Role Switch**
   ```
   🎭 [ROLE SWITCH] Solution Architect → Developer
   Reason: Issue #X assigned for development
   Context: Implementing FMP API enhancement с test webhook integration
   ```

2. **Context Review**
   - Проверить текущие Issues
   - Изучить requirement/specifications
   - ✅ **Понять parent-child relationships** для testing integration
   - Понять dependencies и blockers

3. **Role Execution**
   - Следовать протоколу активной роли
   - Документировать прогресс
   - Взаимодействовать с другими ролями при необходимости

4. **Role Exit Documentation**
   ```
   ✅ [ROLE COMPLETE] Developer → QA Engineer  
   Deliverables: Workflow implemented, test webhooks added, ready for testing
   Next: Parent workflow testing через test webhooks required для Issue #X
   ```

### **🚦 Multi-Role Scenarios:**

Иногда несколько ролей активны одновременно:

- **Solution Architect + Technical Writer** - при создании architectural documentation
- **Developer + QA Engineer** - при bug fixing с immediate testing через test webhooks
- **DevOps + QA Engineer** - при deployment с verification
- ✅ **DevOps + Technical Writer** - при release documentation и announcements
- ✅ **QA + Developer** - при test webhook configuration и parent workflow testing

---

## 🎫 Issues Management Strategy

### **📊 Issues Creation Matrix:**

| Role | Creates Issues | Types | When |
|------|----------------|-------|------|
| 🏗️ **Solution Architect** | ✅ **PRIMARY** | [FEATURE], [ENHANCEMENT], [DOCS] | Planning, Architecture decisions |
| 💻 **Developer** | ❌ **NO** | - | Works on assigned Issues only |
| 🧪 **QA Engineer** | ✅ **BUGS ONLY** | [BUG], [TEST] | When bugs discovered, ✅ parent-child integration issues |
| 📚 **Technical Writer** | ✅ **DOCS GAPS** | [DOCS] | When documentation gaps found, ✅ testing docs missing |
| 🚀 **DevOps Engineer** | ✅ **INFRASTRUCTURE** | [ENHANCEMENT], [FEATURE] | Infrastructure/CI-CD/Release issues, ✅ testing integration |

### **🔄 Issues Workflow:**

```
User Request → Solution Architect Analysis → Issues Created → Role Assignment → Execution → QA (Test Webhooks) → Deploy → Release
                     ↓
            Other Roles can create specialized Issues during execution
```

### **📋 Issues Responsibility Examples:**

#### **Solution Architect creates:**
- `[FEATURE] Add cryptocurrency price tracking workflow`
- `[ENHANCEMENT] Improve error handling in FMP Router`
- `[DOCS] Document new architecture decisions`
- ✅ `[ENHANCEMENT] Implement Test Webhook - Test Execution approach`

#### **QA Engineer creates:**
- `[BUG] FMP Router fails with 500 error on timeout`
- `[TEST] Create regression tests for AI Deepseek workflow`
- ✅ `[BUG] Parent workflow test webhook not calling child workflows properly`

#### **Technical Writer creates:**
- `[DOCS] Missing installation guide for new users`
- `[DOCS] API documentation outdated after FMP changes`
- ✅ `[DOCS] Test webhook procedures documentation missing`

#### **DevOps Engineer creates:**
- `[ENHANCEMENT] Add automated deployment for PROD workflows`
- `[FEATURE] Implement workflow health monitoring`
- ✅ `[ENHANCEMENT] Create GitHub Releases & Tags system` *(Example: Issue #7)*
- ✅ `[ENHANCEMENT] Update CI/CD pipeline for test webhook integration`

---

## 🔗 Integration with Existing Protocols

### **🤝 Связь с другими протоколами:**

#### **AI Agent Execution Protocol:**
- **Все роли должны следовать** 5-step execution flow: Plan → Propose → Get Approval → Execute → Document
- **Роли определяют ЧТО делать**, execution protocol определяет КАК это делать
- **Обязательное планирование** командных действий независимо от роли
- 📖 **[Детали execution workflow →](ai-agent-execution-protocol.md)**

#### **MCP CI/CD Deployment Protocol:**
- **Complete development lifecycle** от architecture до release
- **Role-based CI/CD process** с phase-by-phase workflow
- **MCP-first approach** с UI escalation procedures
- **Production deployment** и professional release management
- **Cross-role collaboration** для comprehensive project delivery
- 📖 **[Детали CI/CD workflow →](mcp-cicd-deployment-protocol.md)**

#### **GitHub Issues Protocol:**
- Все роли следуют стандартным шаблонам Issues
- Issues creation permissions по ролям
- Lifecycle management через роли

#### **Context Handoff Protocol:**
- При смене AI агента - указывать активную роль
- Передавать роль-специфичный контекст  
- Документировать незавершенные роль-специфичные задачи

#### **✅ Testing Strategy Integration (UPDATED):**
- ✅ **QA Engineer роль интегрируется с Test Webhook - Test Execution подходом**
- ✅ **Developer роль создает testable workflows с test webhooks**
- ✅ **DevOps роль обеспечивает testing infrastructure с new approach integration**
- ✅ **All roles support** simplified testing architecture

#### **✅ Release Management Integration:**
- ✅ **DevOps роль интегрируется с GitHub Releases & Tags system**
- ✅ **Professional semantic versioning** через automated workflows
- ✅ **Release artifacts packaging** и distribution
- ✅ **Cross-role collaboration** для comprehensive releases

---

## 📖 Примеры использования

### **✅ Сценарий 1: Новая функция с новым testing approach**
```
1. 🏗️ Solution Architect: Анализирует запрос "Add Slack notifications"
2. 🏗️ Solution Architect: Создает Issue #N [FEATURE] Add Slack integration с test webhook requirements
3. 💻 Developer: Реализует Slack workflow + adds test webhook для parent workflow  
4. ✅ 🧪 QA Engineer: Тестирует через parent workflow test webhook (natural child execution)
5. 📚 Technical Writer: Документирует Slack setup guide + test webhook procedures
6. 🚀 DevOps Engineer: Deploys to PROD
7. ✅ 🚀 DevOps Engineer: Creates versioned release с новой функциональностью
```

### **✅ Сценарий 2: Bug Discovery в parent-child flow**
```
1. ✅ 🧪 QA Engineer: Находит баг в parent-child interaction через test webhook
2. 🧪 QA Engineer: Создает Issue #M [BUG] Parent workflow not calling child properly
3. 💻 Developer: Исправляет parent-child integration по Issue #M
4. ✅ 🧪 QA Engineer: Retests через parent workflow test webhook
5. 🚀 DevOps Engineer: Hotfix deployment
6. ✅ 🚀 DevOps Engineer: Creates hotfix release с patch версией
```

### **✅ Сценарий 3: Testing Documentation Gap**
```
1. ✅ 📚 Technical Writer: Обнаруживает отсутствие test webhook guide
2. 📚 Technical Writer: Создает Issue #K [DOCS] Missing test webhook procedures guide
3. ✅ 📚 Technical Writer: Пишет comprehensive test webhook guide
4. 🏗️ Solution Architect: Reviews для архитектурной точности
5. ✅ 🚀 DevOps Engineer: Updates release notes для следующего release
```

### **✅ Сценарий 4: CI/CD Integration Update**
```
1. ✅ 🚀 DevOps Engineer: CI/CD pipeline needs update для test webhook approach
2. 🚀 DevOps Engineer: Создает Issue #P [ENHANCEMENT] Update CI/CD для test webhook integration
3. ✅ 🚀 DevOps Engineer: Replaces Test Orchestrator calls с parent workflow test webhook calls
4. 🧪 QA Engineer: Validates new CI/CD testing integration
5. ✅ 🚀 DevOps Engineer: Updates release notes с improved testing infrastructure
```

---

## 🎯 Success Metrics

### **Эффективность ролей:**
- **Issues resolution time** по ролям
- **Quality metrics** (bugs found vs bugs in production)
- ✅ **Parent-child integration success rate** через test webhook approach
- **Documentation coverage** (docs vs features ratio)
- **Deployment success rate**
- ✅ **Release management efficiency** - time от ready до published
- **User satisfaction** с deliverables

### **Role switching efficiency:**
- **Context switch time** между ролями
- **Role clarity** (правильность выбора роли)
- **Collaboration effectiveness** между ролями
- ✅ **Testing integration effectiveness** - роли working together на test webhook approach
- ✅ **Release coordination** между ролями для comprehensive releases

### **✅ Testing Integration Success:**
- **Test webhook setup time** для new parent workflows
- **Parent-child testing coverage** через natural execution
- **Bug detection rate** в parent-child interactions
- **CI/CD integration success** с new testing approach

---

*Этот документ является живым руководством и обновляется по мере развития проекта и накопления опыта работы с ролевой моделью AI агента. Последнее обновление включает интеграцию с Test Webhook - Test Execution подходом для simplified и more effective testing architecture.*