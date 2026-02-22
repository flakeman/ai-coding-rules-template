# AI Coding Rules: Universal Guide for Developers and AI Agents

Comprehensive system of 9 rules for effective AI-assisted development based on 2025 best practices. Use these rules in every project by cloning this repository as a template.

**Related:** Интегрируется с [CONTAINERIZATION_RULES.md](./CONTAINERIZATION_RULES.md) (Правило 1.1: Микросервисная архитектура) и [SECURITY-RULES.md](./SECURITY-RULES.md) для полного охвата разработки, безопасности и инфраструктуры.

---

## 🎯 Rule 1: Ответственность за ошибки

**Objective:** Exclude AI blame-shifting; focus on input quality.

**Steps:**
1. Analyze context for contradictions/garbage
2. Clarify instructions (specific, with examples)
3. Add success criteria (tests, linters)

**Success Criteria:** No bugs in 80% of cases; for rare stacks – external search

**AI Prompt:**
```
Проверь контекст на ошибки. Если неясно — спроси. Исправь код по тестам: [тесты]
```

---

## 📦 Rule 2: Подготовка контекста

**Objective:** Give AI the complete project picture top-to-bottom.

**Steps:**
1. Load architecture, subsystems, interactions
2. Warm up Memory Bank (study repository)
3. Focus on task after overview

**Success Criteria:** Context in CONTEXT.md < 10k tokens, no random fragments

**AI Prompt:**
```
Изучи проект: архитектура из CONTEXT.md. Подтверди понимание перед кодом.
```

---

## 📋 Rule 3: Обязательное планирование

**Objective:** Avoid chaotic code; plan as a contract.

**Steps:**
1. Generate plan in .md (points, files, tests)
2. Approve before implementation
3. Execute by points sequentially

**Success Criteria:** Plan covers 100% of task; saved in git

**AI Prompt:**
```
Создай план в PLAN.md: 1. Файлы. 2. Логика. 3. Тесты. Утверди перед кодом.
```

---

## ✅ Rule 4: Приёмка через тесты

**Objective:** Automated verification instead of code review.

**Steps:**
1. Discuss tests early (e2e > unit)
2. AI self-checks
3. Run CI

**Success Criteria:** 100% scenario coverage; green tests

**AI Prompt:**
```
Напиши тесты по критериям: [список]. Запусти и отчитайся: passed/failed.
```

---

## 🔍 Rule 5: Верификация плана

**Objective:** Synchronize implementation with plan.

**Steps:**
1. Open PLAN.md
2. Report: point → file/test
3. Rework on gaps

**Success Criteria:** All points "done" with evidence

**AI Prompt:**
```
Сверь с PLAN.md: для пункта 1 — файлы X, тесты Y. Отчёт в VERIFY.md.
```

---

## 🔗 Rule 6: Git-гигиена

**Objective:** Rollback ability and traceability.

**Steps:** Commit at stages: plan, point, tests. Messages: "Rule3: Plan approved"

**Success Criteria:** No "monster commits"; readable git log

**AI Prompt:**
```
Предложи git commit: 'Rule4: Tests for [feature]' после зелёных тестов.
```

---

## 📐 Rule 7: Работа по SDD

**Objective:** Structured specification before code.

**Steps:**
1. Fill SDD-TEMPLATE.md (architecture, models, API)
2. AI generates artifacts sequentially
3. Fix changes

**Success Criteria:** SDD covers domain; verified by tests

**AI Prompt:**
```
Заполни SDD-MICRO.md по требованиям. Генерируй код только после утверждения.
```

---

## 🔄 Rule 8: Формирование и актуализация контекста

**Objective:** Living project context.

**Steps:**
1. Initialize CONTEXT.md
2. After stage: diff + update
3. AI confirmation

**Success Criteria:** No contradictions; version in git

**AI Prompt:**
```
Обнови CONTEXT.md: git diff + новые зависимости. Подтверди: 'Контекст актуален'.
```

---

## 🏗️ Rule 9: Микросервисная архитектура

**Objective:** Scalability and service isolation.

**Implementation Details:** См. [CONTAINERIZATION_RULES.md](./CONTAINERIZATION_RULES.md) для детальных правил микросервисной архитектуры, Docker, Kubernetes, deployment patterns и observability.

**Steps:**
1. In SDD: Bounded Contexts, API contracts, events
2. Generate from service-template (layers, Docker)
3. Test coupling/faults

**Success Criteria:** Loose coupling; observability (logs/metrics)

**AI Prompt:**
```
По SDD-MICRO.md: генерируй сервис [name]. Контракт OpenAPI, события Kafka, тесты изоляции.
```

---

## 📁 Repository Structure

```
ai-coding-rules-template/
├── AI-RULES.md                 # This file - all 9 rules with prompts
├── README.md                   # Quick start guide
├── docs/
│   ├── SDD-TEMPLATE.md         # System Design Document template
│   ├── SDD-MICRO.md            # Microservices SDD template
│   ├── CONTEXT.md              # Project context (copy & adapt)
│   └── MICROservices-RULES.md  # Microservices rules details
├── examples/
│   ├── task-planning.md        # Example task plan
│   ├── sdd-example.md          # Example SDD completion
│   └── microservice-example/   # Working microservice example
├── scripts/
│   └── update-context.sh       # Script to update CONTEXT.md
├── .github/
│   └── workflows/
│       └── ai-check.yml        # CI: validates plans, tests, SDD
├── .gitignore
├── LICENSE (MIT)
└── .gitattributes
```

---

## 🚀 Quick Start

1. **Clone as template:** GitHub → "Use this template" → Create new repository
2. **Fill CONTEXT.md** with your project architecture
3. **Generate SDD-TEMPLATE.md** for current task
4. **Follow rules 1-9** for every task: Plan → Code → Test → Verify → Commit
5. **Reference in AI prompts:** "Follow AI-RULES.md from https://github.com/flakeman/ai-coding-rules-template"

---

## 📌 Key Principles

- **Planning First:** No code without approved plan
- **Tests Prove:** Tests are the acceptance criteria
- **Context Alive:** Update context after each stage
- **Git Traces:** Each rule = git commit
- **SDD Drives:** Architecture comes before implementation
- **Microservices:** Bounded contexts, loose coupling, observability

---

## 🔧 For AI Agents (Cursor, Claude, Copilot)

Add this to your system prompt:
```
You MUST follow 9 AI Coding Rules from: 
https://github.com/flakeman/ai-coding-rules-template/blob/main/AI-RULES.md

For every project task:
1. Read CONTEXT.md and SDD-TEMPLATE.md
2. Create PLAN.md with points 1-N
3. Request human approval before code
4. Generate code by plan points
5. Write tests for 100% of scenarios
6. Verify against original PLAN.md
7. Commit: "Rule[N]: [description]"
```

---


## Rule 10 — AI-Agent Collaboration

**Objective:** Безопасная и предсказуемая работа с AI‑агентами как с членами команды.

**Steps:**

1. AI не вносит изменения в код без явного указания формата результата (patch, список файлов, конкретные фрагменты кода).
2. Перед генерацией кода AI кратко описывает план изменений: цель, затронутые модули, ожидаемые побочные эффекты.
3. Инфраструктурный код (CI/CD, Terraform, Helm, Docker) редактируется AI только при наличии отдельного одобренного плана в SDD/PLAN.md.
4. Если задача затрагивает более 5 файлов, AI обязан предложить разбиение на несколько подзадач и отдельных PR.
5. AI не придумывает бизнес‑правила: формулирует гипотезы с явной пометкой и запросом подтверждения у человека.

**Success Criteria:**

- Все AI‑изменения описаны в виде явного плана или патча.
- Нет неожиданных правок в инфраструктуре и критичных модулях.
- Ревьюер понимает, зачем и где AI менял код.

**AI Prompt:**

> При работе над задачей:
> 1) Сначала опиши план изменений (цель, файлы, побочные эффекты).
> 2) Не меняй инфраструктуру (CI/CD, Terraform, Docker) без отдельного плана.
> 3) Если задействовано >5 файлов, предложи разбиение на подзадачи и несколько PR.
> 4) Не придумывай бизнес‑правила — помечай предположения и запрашивай подтверждение.

***

## Rule 11 — Scope & Context Management

**Objective:** Контролируемый объём изменений и согласованность с архитектурой.

**Steps:**

1. Перед изменениями AI перечисляет, какие модули/микросервисы и внешние контракты (API, события, очереди) будут затронуты.
2. Любые кросс‑сервисные изменения требуют обновления CONTEXT.md и/или SDD (раздел про интеграции и взаимодействия).
3. Изменение публичных API должно включать: новый контракт, план миграции, версионирование (v1 → v2) и стратегию обратной совместимости.
4. Если во время работы AI выявляет дополнительные изменения вне текущего тикета, он фиксирует рекомендации, но не реализует их без нового тикета/SDD.

**Success Criteria:**

- Все изменения укладываются в границы задачи и отражены в CONTEXT.md/SDD.
- Публичные API не ломают существующих потребителей без плана миграции.
- Нет «скрытых» кросс‑сервисных правок.

**AI Prompt:**

> Перед изменением кода:
> 1) Перечисли затронутые модули/сервисы и внешние контракты.
> 2) Обнови/предложи обновление CONTEXT.md и SDD для новых интеграций.
> 3) Для публичных API опиши новый контракт, план миграции и версионирование.
> 4) Дополнительные улучшения за пределами задачи только рекомендовать, но не реализовывать.

***

## Rule 12 — Readability & Reviewability

**Objective:** Код от AI легко читать, ревьюить и сопровождать.

**Steps:**

1. AI следует принятому в проекте стилю (линтер, formatter, naming‑конвенции) и не вводит собственные правила форматирования.
2. Новые функции/классы документируются только там, где логика нетривиальна, с фокусом на «почему», а не «что» делает код.
3. Запрещены «магические числа» и «магические строки» — использовать именованные константы, конфигурацию или enum‑ы.
4. Новые публичные интерфейсы (методы, DTO, API) минимальны по поверхности и не раскрывают детали реализации.
5. Сложные алгоритмы сопровождаются mini‑SDD в комментариях или отдельном разделе: входы, выходы, инварианты, ограничения.

**Success Criteria:**

- Код проходит линтер/formatter без дополнительных правок.
- Ревьюеру понятен смысл изменений без чтения всей истории тикета.
- Нет магических констант и утечки деталей реализации.

**AI Prompt:**

> При генерации кода:
> 1) Соблюдай существующий стиль (линтер/formatter, naming).
> 2) Добавляй комментарии только для нетривиальной логики, объясняя «почему».
> 3) Не используй магические числа/строки — выноси их в константы/конфиг.
> 4) Минимизируй публичные интерфейсы и не раскрывай детали реализации.
> 5) Для сложной логики добавь краткое текстовое описание алгоритма.

***

## Rule 13 — Testing & Operational Readiness

**Objective:** Изменения от AI готовы к эксплуатации, а не только «компилируются».

**Steps:**

1. Помимо юнит‑тестов AI предлагает и реализует edge‑case и негативные сценарии для ключевых веток логики.
2. Для кода, работающего с сетью, I/O, платежами или очередями, AI предлагает стратегию ретраев, таймаутов и деградации.
3. Взаимодействие с внешними API сопровождается контрактными тестами, стабами или тестовыми клиентами.
4. Логирование структурированное (ключи, trace‑id, correlation‑id, user/tenant‑id), без попадания секретов и персональных данных.
5. Для изменений в критичных путях (аутентификация, биллинг, платежи) AI описывает план безопасного выката: feature‑flags, canary, shadow‑traffic.

**Success Criteria:**

- Тесты покрывают не только «happy path», но и крайние случаи.
- Система корректно ведёт себя при ошибках внешних зависимостей.
- Логи помогают расследовать инциденты, не раскрывая чувствительные данные.

**AI Prompt:**

> После написания кода:
> 1) Добавь юнит‑тесты с edge‑case и негативными сценариями.
> 2) Предложи и реализуй стратегию ретраев/таймаутов/деградации для внешних вызовов.
> 3) Для внешних API добавь контракты/стабы/тестовые клиенты.
> 4) Сделай структурированное логирование без секретов и персональных данных.
> 5) Для критичных путей предложи план безопасного выката (flags, canary, shadow).

***

## Rule 14 — Security by Default

**Objective:** Расширение SECURITY-RULES: по умолчанию выбирать максимально безопасные решения.

**Steps:**

1. В любых новых компонентах применять принцип минимально необходимых привилегий: роли, пермишены, доступы по умолчанию закрыты.
2. Для данных пользователей и платёжной информации явно описывать: где хранятся данные, в каком виде (маскирование, шифрование), кто имеет доступ.
3. Не предлагать и не оставлять в коде примеры с отключением проверок безопасности (disable SSL, allowAll, skip auth) в боевом пути; в примерах — только с жирной пометкой «только для локальной отладки».
4. При добавлении внешних библиотек указывать назначение, лицензию, риски supply chain и фиксировать версии (lockfile).
5. Для новых эндпоинтов выполнять мини‑моделирование угроз (что может пойти не так: инъекции, brute‑force, утечки, эскалация прав) и предлагать меры защиты.

**Success Criteria:**

- Нет боевого кода с отключённой безопасностью по умолчанию.
- Чувствительные данные всегда защищены и описаны в документации.
- Новые зависимости и эндпоинты проходят базовую проверку безопасности.

**AI Prompt:**

> При проектировании и изменении функционала:
> 1) Применяй принцип минимальных привилегий и закрытых по умолчанию доступов.
> 2) Явно опиши хранение, защиту и доступ к чувствительным данным.
> 3) Не оставляй в боевом пути пример кода с отключённой безопасностью.
> 4) При добавлении библиотек укажи назначение, лицензию и риски.
> 5) Для новых эндпоинтов опиши основные угрозы и меры защиты.

***

## Rule 15 — Governance & Change Traceability

**Objective:** Сделать работу AI‑агентов управляемой и трассируемой на уровне процессов.

**Steps:**

1. Каждое значимое изменение от AI привязывается к тикету и конкретному правилу (commit‑message в формате `Rule[N]: ...`).
2. В PLAN.md фиксируются шаги, выполненные AI, и шаги, требующие участия человека.
3. После завершения задачи AI предлагает обновления CONTEXT.md с описанием изменений и их влияния на архитектуру.
4. В код‑ревью явно указывается, какие части были сгенерированы AI, а какие — вручную.
5. Для инцидентов/багов, связанных с AI‑изменениями, выполняется короткий пост‑мортем с уточнением, какое правило могло предотвратить проблему.

**Success Criteria:**

- Можно проследить, какие именно изменения сделал AI и зачем.
- CONTEXT.md отражает фактическое состояние системы.
- Инциденты от AI‑изменений ведут к уточнению правил, а не повторяются.

**AI Prompt:**

> При завершении работы над задачей:
> 1) Подготовь commit‑сообщения с префиксом `Rule[N]: ...`.
> 2) Обнови/предложи обновления для CONTEXT.md с описанием изменений.
> 3) Отметь в описании PR, какие части кода сгенерированы AI.
> 4) Если обнаружены риски/проблемы, предложи, как скорректировать правила.

***


## 📄 License

MIT License - Use freely in your projects
