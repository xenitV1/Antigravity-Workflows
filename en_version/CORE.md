---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> This file is the central routing point for all tasks.
> Appropriate skill(s) are determined and loaded based on the task type.

---

## 🎯 Skills Reference - When to Use Which Skill?

> [!NOTE]
> **Dynamic Matching:** Users may provide commands that do not exactly match the examples below.
> These tables are of **reference** nature. As an agent, analyze the user's request and
> **determine the semantically most appropriate skill(s) by making dynamic inferences**.
> For example, "there is a problem in this API" → may require debugging + backend skills.

---

### 🧠 UltraThink - Deep Thinking Protocol

**File:** `en_version/skills/ultrathink.md`

| Scenario | Example |
|---------|-------|
| **Architectural decisions** | "Should we split the monolith into microservices?" |
| **Performance optimization** | "Why is this query slow?" |
| **Complex bug analysis** | "Where is the race condition coming from?" |
| **Multi-step refactoring** | "How should we refactor these 10 files?" |
| **System design** | "Design a scalable auth system" |
| **Trade-off evaluation** | "SQL vs NoSQL which is more appropriate?" |
| **Risk analysis** | "What are the potential impacts of this change?" |

---

### 🏗️ Architecture - System Design

**File:** `en_version/skills/architecture.md`

| Scenario | Example |
|---------|-------|
| **New system design** | "Create e-commerce platform architecture" |
| **Microservices decision** | "Which services should we split into?" |
| **Database selection** | "PostgreSQL or MongoDB?" |
| **Scaling strategy** | "How do we scale for 10x users?" |
| **API gateway design** | "How should we apply the gateway pattern?" |
| **Event-driven architecture** | "Communicate asynchronously with Kafka" |

---

### 🎨 Design System - UI/UX Guide

**File:** `en_version/skills/design-system.md`

| Scenario | Example |
|---------|-------|
| **Component design** | "Create button component" |
| **Responsive layout** | "Set up mobile-first grid system" |
| **Color system** | "Add dark mode support" |
| **Typography** | "Determine font hierarchy" |
| **Spacing system** | "Apply 8-point grid" |
| **Animation** | "Add micro-interactions" |
| **Accessibility** | "Make WCAG compliant form" |

---

### 💻 Backend - Server-Side Development

**File:** `en_version/skills/backend.md`

| Scenario | Example |
|---------|-------|
| **REST API creation** | "Write User CRUD endpoints" |
| **Authentication** | "Set up JWT-based auth system" |
| **Database integration** | "Connect PostgreSQL with Prisma" |
| **Validation** | "Apply input validation with Zod" |
| **Error handling** | "Create global error handler" |
| **Caching** | "Apply Redis cache strategy" |
| **API security** | "Configure rate limiting and CORS" |

---

### 📱 Mobile - Cross-Platform Application

**File:** `en_version/skills/mobile.md`

| Scenario | Example |
|---------|-------|
| **React Native app** | "Start new project with Expo" |
| **Flutter app** | "Apply Material 3 UI" |
| **State management** | "Install Zustand/Riverpod" |
| **Navigation** | "Configure Stack/Tab navigator" |
| **Native features** | "Add camera/location access" |
| **Offline support** | "Local storage with SQLite" |
| **Push notifications** | "Integrate Firebase notifications" |

---

### 🧪 Testing - TDD and Test Strategies

**File:** `en_version/skills/testing.md`

| Scenario | Example |
|---------|-------|
| **Writing unit tests** | "Write tests for UserService" |
| **Integration test** | "Create API endpoint tests" |
| **E2E testing** | "Test login flow with Playwright" |
| **Test coverage** | "Increase coverage to 80%" |
| **Mocking** | "Mock external API" |
| **Applying TDD** | "Red-Green-Refactor cycle" |
| **React testing** | "Write component tests" |

---

### 🔍 Debugging - Troubleshooting

**File:** `en_version/skills/debugging.md`

| Scenario | Example |
|---------|-------|
| **Runtime error** | "TypeError: Cannot read property" |
| **Intermittent bug** | "It works sometimes and sometimes not" |
| **Performance issue** | "Page loads very slowly" |
| **Memory leak** | "Application slows down over time" |
| **Race condition** | "Data sometimes comes incorrect" |
| **Production bug** | "Bug appearing only in production" |
| **Regression** | "Old feature broken" |

---

### ♻️ Refactoring - Code Improvement

**File:** `en_version/skills/refactoring.md`

| Scenario | Example |
|---------|-------|
| **Code smell cleanup** | "This function is too long" |
| **Applying DRY** | "Merge duplicate code" |
| **Extract function** | "Break down large function" |
| **Rename refactoring** | "Give more meaningful names" |
| **Design pattern** | "Apply strategy pattern" |
| **Legacy code** | "Modernize old code" |
| **Type safety** | "Remove any's" |

---

### 🚀 Production Deployment - DevOps

**File:** `en_version/skills/production-deployment.md`

| Scenario | Example |
|---------|-------|
| **CI/CD pipeline** | "Set up GitHub Actions workflow" |
| **Docker deployment** | "Containerize and deploy" |
| **Environment setup** | "Separate staging/production" |
| **Blue-green deploy** | "Zero-downtime deployment" |
| **Monitoring setup** | "Install Prometheus/Grafana" |
| **Rollback** | "Return to previous version" |
| **Security scan** | "Add Snyk to pipeline" |

---

### 📁 Multi-File Sync - Cross-File Changes

**File:** `en_version/skills/multi-file-sync.md`

| Scenario | Example |
|---------|-------|
| **Global rename** | "Change userId to customerId project-wide" |
| **API versioning** | "Migrate from v1 to v2" |
| **Folder restructure** | "Switch to feature-first structure" |
| **Import path update** | "Perform alias change" |
| **Type definition change** | "Extend interface, update all usages" |
| **Config migration** | "Rename ENV variables" |

---

### 📦 Dependency Management - Package Management

**File:** `en_version/skills/dependency-management.md`

| Scenario | Example |
|---------|-------|
| **Security audit** | "Run npm audit and fix" |
| **Major upgrade** | "Switch from React 18 to 19" |
| **Dependency cleanup** | "Remove unused packages" |
| **Version conflict** | "Resolve peer dependency error" |
| **Lock file issue** | "package-lock.json issue" |
| **Bundle size** | "Reduce bundle size" |
| **License check** | "Check license compliance" |

---

### 📝 Documentation - Documentation

**File:** `en_version/skills/documentation.md`

| Scenario | Example |
|---------|-------|
| **README writing** | "Create project README" |
| **API docs** | "OpenAPI/Swagger documentation" |
| **Code comments** | "Document functions with JSDoc" |
| **Architecture docs** | "Create system diagrams" |
| **Changelog** | "Update CHANGELOG.md" |
| **ADR writing** | "Document architectural decision" |
| **Onboarding guide** | "New developer guide" |

---

## 🔄 Skill Loading Protocol

### Step 1: Task Analysis
```
Read the user task
    │
    ▼
Determine the appropriate skill(s) from the tables above
    │
    ▼
Load the skill file: en_version/skills/<skill-name>.md
```

### Step 2: If Skill is Not Found
```
⚠️ ERROR: "[skill-name].md" skill file not found.

Please do one of the following:
1. Provide the path for the skill file
2. Create the skill file

Operations CANNOT START without skills.
```

---

## 🔗 Skill Combinations

Complex tasks may require multiple skills:

| Scenario | Skill Combination | Loading Order |
|---------|-------------------|----------------|
| **Complex Backend API** | ultrathink + architecture + backend | 1→2→3 |
| **New UI Component** | design-system + testing | 1→2 |
| **Production Release** | production-deployment + testing | 1→2 |
| **Major Refactoring** | ultrathink + refactoring + multi-file-sync + testing | 1→2→3→4 |
| **Mobile App Feature** | mobile + testing | 1→2 |
| **Bug Fix** | debugging + testing | 1→2 |
| **Architectural Decision** | ultrathink + architecture | 1→2 |
| **Package Upgrade** | dependency-management + testing | 1→2 |

---

## 📂 Skills Directory Structure

```
c:\Users\Mehmet\Desktop\global_workflows\
├── GEMINI.md           ← Global rules (Should be copied to C:\Users\Mehmet\.gemini\)
├── CORE.md             ← Central orchestrator
└── en_version/
    ├── GEMINI.md       ← English version of global rules
    ├── CORE.md         ← English version of orchestrator
    └── skills/
        ├── ultrathink.md           ✅ Deep thinking
        ├── architecture.md         ✅ System design
        ├── design-system.md        ✅ UI/UX guide
        ├── backend.md              ✅ Server-side development
        ├── mobile.md               ✅ Cross-platform mobile
        ├── testing.md              ✅ TDD and test strategies
        ├── debugging.md            ✅ Troubleshooting
        ├── refactoring.md          ✅ Code improvement
        ├── production-deployment.md ✅ DevOps/CI-CD
        ├── multi-file-sync.md      ✅ Cross-file changes
        ├── dependency-management.md ✅ Package management
        └── documentation.md        ✅ Documentation
```

---

## ⚠️ Critical Rules

> [!CAUTION]
> **DO NOT START operation without loading a skill!**
> Appropriate skill(s) MUST be loaded for every task.

> [!WARNING]
> **DO NOT STOP if a skill is not found!**
> Request the file path from the user or suggest creating the skill.

> [!IMPORTANT]
> **GEMINI.md rules are always applicable!**
> ESLint check, 2x code review must be performed.

---

**Last Update:** December 2025
**Version:** 2.0
