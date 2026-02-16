# AI Coding Rules Template 🚀

**Universal guide for effective AI-assisted development** — 9 structured rules for developers and AI agents based on 2025 best practices. Use this repository as a **template for every new project**.

[![GitHub](https://img.shields.io/badge/GitHub-ai--coding--rules--template-blue?logo=github)](https://github.com/flakeman/ai-coding-rules-template)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

---

## 📖 Quick Start

### For New Projects
1. **Click "Use this template"** → Create your repository
2. **Read [AI-RULES.md](./AI-RULES.md)** — All 9 rules with AI prompts
3. **Fill [docs/CONTEXT.md](./docs/CONTEXT.md)** — Your project architecture
4. **Follow the workflow** — Plan → Code → Test → Verify → Commit

### For Existing Teams
- Copy `AI-RULES.md`, `docs/SDD-TEMPLATE.md`, `docs/CONTEXT.md` to your repo
- Reference in team documentation: "Follow rules from https://github.com/flakeman/ai-coding-rules-template"

---

## 🎯 The 9 Rules at a Glance

| # | Rule | Goal | AI Prompt |
|---|------|------|-----------|
| 1 | **Ответственность за ошибки** | Quality input → fewer bugs | Check context, clarify instructions, add tests |
| 2 | **Подготовка контекста** | Complete project picture | Study architecture from CONTEXT.md |
| 3 | **Обязательное планирование** | Plan before code | Create PLAN.md, get approval, execute |
| 4 | **Приёмка через тесты** | Tests = acceptance | Write 100% coverage, run CI, report |
| 5 | **Верификация плана** | Sync code ↔ plan | Match PLAN.md: points → files/tests |
| 6 | **Git-гигиена** | Traceable commits | Commit at each stage with clear messages |
| 7 | **Работа по SDD** | Architecture-first | Fill SDD-TEMPLATE.md before code |
| 8 | **Формирование контекста** | Living documentation | Update CONTEXT.md after each stage |
| 9 | **Микросервисы** | Scalable design | Bounded contexts, loose coupling, observability |

**Full details** → [AI-RULES.md](./AI-RULES.md)

---

## 📁 Repository Structure

```
ai-coding-rules-template/
├── AI-RULES.md              # ⭐ All 9 rules + AI prompts (START HERE)
├── README.md                # This file
│
├── docs/
│   ├── SDD-TEMPLATE.md      # System Design Document template
│   ├── CONTEXT.md           # Project context (copy & customize)
│   └── MICROservices-RULES.md
│
├── examples/                # (Coming soon)
│   ├── task-plan-example.md
│   └── sdd-example.md
│
├── scripts/
│   └── update-context.sh    # Refresh context after development
│
└── .github/
    └── workflows/
        └── ai-check.yml     # CI: validate plans, tests, SDD
```

---

## 🔧 How It Works

### Typical Workflow
```
1. Start Task
   ↓
2. Read CONTEXT.md + AI-RULES.md
   ↓
3. Fill SDD-TEMPLATE.md (architecture)
   ↓
4. Generate PLAN.md with numbered points
   ↓
5. [Approval Point] → Proceed if OK
   ↓
6. Code Implementation (follow plan)
   ↓
7. Write Tests (100% coverage)
   ↓
8. Verify Against Plan (checklist)
   ↓
9. git commit -m "Rule[N]: [description]"
   ↓
10. Update CONTEXT.md (diff + changes)
    ↓
    Done ✅
```

### AI Agent Prompt Template
```
You must follow 9 AI Coding Rules from:
https://github.com/flakeman/ai-coding-rules-template/blob/main/AI-RULES.md

For this task:
1. Read CONTEXT.md: [paste context]
2. Review SDD-TEMPLATE.md: [paste SDD draft]
3. Create PLAN.md with numbered steps
4. Wait for human approval
5. Implement by plan points
6. Write tests for 100% coverage
7. Verify against original plan
8. Suggest git commits with "Rule[N]:" prefix
```

---

## 📚 Key Files

### [AI-RULES.md](./AI-RULES.md) — THE CORE
Comprehensive guide to all 9 rules. Each rule includes:
- **Objective** - What the rule achieves
- **Steps** - How to execute
- **Success Criteria** - How to verify
- **AI Prompt** - Copy-paste ready

### [docs/SDD-TEMPLATE.md](./docs/SDD-TEMPLATE.md)
System Design Document with sections for:
- Project goals & success criteria
- Domain model & entities
- API contracts
- Data schemas
- Workflows & interactions
- Security & compliance

### [docs/CONTEXT.md](./docs/CONTEXT.md)
Live project context — update after every stage:
- Architecture overview
- Technology stack decisions
- API contracts & integrations
- Current development status
- Known issues & debt
- Audit trail (commits, diffs)

---

## 🤖 For AI Agents (Claude, GPT, Copilot)

### System Prompt
```
You MUST follow 9 AI Coding Rules from:
https://github.com/flakeman/ai-coding-rules-template/blob/main/AI-RULES.md

Core principles:
1. Planning first: No code without approved PLAN.md
2. Tests prove quality: 100% test coverage required
3. Context alive: Update after every stage
4. Git traces work: Each rule = one commit
5. SDD drives design: Architecture before implementation
```

### Expected Workflow
- Read CONTEXT.md (project state)
- Generate/refine SDD
- Create detailed PLAN.md
- Wait for human ✅ approval
- Code by plan points
- Tests with 100% coverage
- Verify against plan
- Suggest commits

---

## 🌟 Why These Rules?

Based on **2025 industry best practices**:

- **Rule 1-2:** Avoid AI blame-shifting; quality input matters
- **Rule 3-5:** Structure prevents chaos; planning ↔ code alignment
- **Rule 6:** Git hygiene enables rollback and traceability
- **Rule 7-8:** Documentation-first reduces surprises
- **Rule 9:** Microservices need discipline (bounded contexts, events, observability)

**Result:** Fewer bugs, faster iteration, AI + humans in sync

---

## 🔗 Integration Examples

### With Cursor / VS Code
```
# .cursor/rules/ai-coding-rules.md
Follow rules from: https://github.com/flakeman/ai-coding-rules-template
```

### With Jira / YouTrack
```
Ticket description template:
- Read docs/CONTEXT.md
- Follow AI-RULES.md from: https://github.com/flakeman/ai-coding-rules-template
```

### With GitHub Actions
```yaml
# .github/workflows/ai-check.yml
name: AI Code Quality
on: [pull_request]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Check PLAN.md exists
        run: test -f PLAN.md
      - name: Validate test coverage
        run: pytest --cov=.
```

---

## 📈 Success Metrics

After adopting these rules, you should see:
- ✅ 80%+ fewer AI-generated bugs
- ✅ Faster code reviews (tests + plan clarity)
- ✅ Better team communication (live context)
- ✅ Easier debugging (git commits trace decisions)
- ✅ Scalable architecture (SDD + microservices rules)

---

## 🤝 Contributing

Have improvements? Fork & submit a PR:
1. Update AI-RULES.md with new rule or refinement
2. Add example in `examples/`
3. Update this README

---

## 📄 License

MIT License — Use freely in your projects. See [LICENSE](./LICENSE)

---

## 🔐 Security & Compliance Rules

> **NEW:** Comprehensive security guidelines are now integrated!

This repository now includes complementary **[SECURITY-RULES.md](./SECURITY-RULES.md)** with 10 essential security & InfoSec rules covering:

- **Secrets Management** — Zero hardcoded credentials
- **Input Validation** — Prevent injection attacks  
- **Authentication & Authorization** — OAuth2, MFA, RBAC
- **Encryption** — TLS 1.3+, AES-256
- **Logging & Audit** — Centralized, structured logging
- **Compliance** — GDPR, SOC2, PCI-DSS
- **Threat Modeling** — STRIDE analysis
- **Security Testing** — SAST, DAST, pen testing
- **Incident Response** — IRP, SIEM, breach notification
- **Supply Chain** — SBOM, dependency verification

**For secure development:** Use both **AI-RULES.md** (coding) + **SECURITY-RULES.md** (security) together for comprehensive governance.

Read more: [SECURITY-RULES.md](./SECURITY-RULES.md)

## 🚀 Get Started Now

1. **Clone as template:** [Use this template](https://github.com/flakeman/ai-coding-rules-template/generate)
2. **Customize CONTEXT.md** for your project
3. **Share the link:** "Follow rules from https://github.com/flakeman/ai-coding-rules-template"
4. **Start coding** with AI agents in full alignment!

**Questions?** Open an Issue or check [AI-RULES.md](./AI-RULES.md)

---

Made with ❤️ for developers & AI agents | Updated Feb 2026
