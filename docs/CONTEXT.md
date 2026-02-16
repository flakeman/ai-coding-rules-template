# Project Context - [YOUR_PROJECT_NAME]

Live context document to be updated after every development stage. Used by AI agents to understand project state.

**Last Updated:** [Date]  
**AI Agent Name:** [Claude/GPT/etc]  
**Token Usage:** [Current tokens / Max]

---

## 1. Project Overview

### Business Context
- **Project Name:** [Name your project]
- **Purpose:** [What problem does it solve?]
- **Stakeholders:** [Who benefits from this?]
- **Timeline:** [Key dates]

### Technical Vision
- **Architecture Pattern:** [Microservices / Monolith / Serverless]
- **Primary Language:** [e.g., Python, Go]
- **Target Platforms:** [e.g., AWS, K8s, Cloud Run]

---

## 2. System Architecture Overview

```
[Update with your architecture diagram/description]

High-Level Flow:
1. Frontend/Client → API Gateway
2. API Gateway → Services (Auth, Business Logic, Data)
3. Services → Database / Cache / Message Queue
4. Async Jobs → Message Queue → Workers
```

### Core Services/Modules
- **Service A:** [Description]
- **Service B:** [Description]
- **Database:** [Technology + version]
- **Cache:** [Technology + version]

---

## 3. Key Technology Decisions

| Technology | Version | Decision Rationale |
|-----------|---------|------------------|
| Framework | [v] | [Why chosen] |
| Database | [v] | [Why chosen] |
| Message Queue | [v] | [Why chosen] |

**Constraints:** [Any hard constraints/requirements]

---

## 4. Current Development Status

### Completed Components
- [ ] Component A
- [ ] Component B

### In Progress
- Component C (Est. completion: [date])

### Planned
- Component D
- Component E

---

## 5. API Contracts & Integrations

### Internal APIs
```
GET  /api/v1/users/{id}
POST /api/v1/users
```

### External Dependencies
- **Service X API:** `https://api.service-x.com` (v2.0)
- **Payment Provider:** Stripe (webhook enabled)

### Events/Messaging
- **Queue:** Kafka topic: `order.created`
- **Consumer:** Order Service

---

## 6. Data Model Summary

### Key Entities
- User: id, email, created_at
- Order: id, user_id, total, status
- Product: id, name, price, inventory

### Relationships
- User 1 → Many Orders
- Order 1 → Many OrderItems
- OrderItem → Product

---

## 7. Security & Compliance

- **Authentication:** [OAuth2 / JWT / etc]
- **Authorization:** [RBAC / ABAC]
- **Data Encryption:** [At-rest / In-transit]
- **Compliance:** [GDPR / SOC2 / etc]

---

## 8. Known Issues & Debt

| Issue | Impact | Fix ETA |
|-------|--------|---------|
| [Issue 1] | [High/Medium/Low] | [Date] |
| [Issue 2] | [High/Medium/Low] | [Date] |

---

## 9. Recent Changes (Audit Trail)

### Last 3 Commits
1. `commit-hash`: Rule 3: Plan approved
2. `commit-hash`: Rule 4: Tests passing
3. `commit-hash`: Rule 7: SDD updated

### Context Diffs (if any)
- Updated Service B interface (backwards compatible)
- Added new database migration

---

## 10. AI Agent Instructions

**Ignore:** [Any outdated information]  
**Focus On:** [Priority areas for AI work]  
**Test Strategy:** [Unit / Integration / E2E]  
**Git Branch:** `main` (default)

**System Prompt:** "Follow AI Coding Rules from: https://github.com/flakeman/ai-coding-rules-template"

---

## 11. Quick Reference Links

- Jira/YouTrack Board: [URL]
- Slack Channel: [#channel]
- Documentation: [Wiki/Docs URL]
- Deployment Guide: [URL]
- Architecture Diagram: [Figma/Miro]

---

## Context Refresh Checklist

After each development stage, update:
- [ ] New API endpoints
- [ ] Database schema changes
- [ ] New dependencies added
- [ ] Completed issues
- [ ] Known blockers
- [ ] Test coverage improvements
- [ ] Security/compliance updates
