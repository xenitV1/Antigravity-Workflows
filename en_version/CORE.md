---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> This file is the central routing point for all tasks.
> Appropriate skill(s) are determined and loaded based on the task type.

---

# 📋 Contents

1. [Skills Reference - Which Skill When?](#1-skills-reference---which-skill-when)
    - [1.1 🧠 UltraThink - Deep Thinking Protocol](#11-🧠-ultrathink---deep-thinking-protocol)
    - [1.2 🏗️ Architecture - System Design](#12-🏗️-architecture---system-design)
    - [1.3 🎨 Design System - UI/UX Guide](#13-🎨-design-system---uiux-guide)
    - [1.4 💻 Backend - Server-Side Development](#14-💻-backend---server-side-development)
    - [1.5 📱 Mobile - Cross-Platform App](#15-📱-mobile---cross-platform-app)
    - [1.6 🧪 Testing - TDD and Test Strategies](#16-🧪-testing---tdd-and-test-strategies)
    - [1.7 🔍 Debugging](#17-🔍-debugging)
    - [1.8 ♻️ Refactoring - Code Improvement](#18-♻️-refactoring---code-improvement)
    - [1.9 🚀 Production Deployment - DevOps](#19-🚀-production-deployment---devops)
    - [1.10 📁 Multi-File Sync - Multi-File Changes](#110-📁-multi-file-sync---multi-file-changes)
    - [1.11 📦 Dependency Management](#111-📦-dependency-management)
    - [1.12 📝 Documentation](#112-📝-documentation)
    - [1.13 ⚡ Optimization - System & Flow Optimization](#113-⚡-optimization---system--flow-optimization)
2. [Skill Loading Protocol](#2-skill-loading-protocol)
3. [Skill Combinations](#3-skill-combinations)
4. [Skills Directory Structure](#4-skills-directory-structure)
5. [Critical Rules](#5-critical-rules)

---

# 1. Skills Reference - Which Skill When?

> [!NOTE]
> **Dynamic Matching:** Users may give commands that do not exactly match the examples below.
> These tables are for **reference**. As an Agent, analyze the user's request and
> **determine the most semantically appropriate skill(s) through dynamic inference.**
> For example, "problem with this API" → might require debugging + backend skills.

---

## 1.1 🧠 UltraThink - Deep Thinking Protocol
**File:** [skills/ultrathink.md](skills/ultrathink.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Architectural decisions** | "Should we split the Monolith into microservices?" | [**Section 10:** Synthesis and Decision](skills/ultrathink.md#10-phase-7-synthesis-and-decision) |
| **Performance optimization** | "Why is this query slow?" | [**Section 4:** Problem Understanding](skills/ultrathink.md#4-phase-1-problem-understanding) / [**Section 5:** Hypothesis](skills/ultrathink.md#5-phase-2-hypothesis-generation) |
| **Complex bug analysis** | "Where is the race condition coming from?" | [**Section 4:** Problem Understanding](skills/ultrathink.md#4-phase-1-problem-understanding) |
| **Multi-step refactor** | "How should we refactor these 10 files?" | [**Section 3:** Meta-Planning](skills/ultrathink.md#3-phase-0-meta-planning) |
| **System design** | "Design a scalable auth system" | [**Section 6:** Solution Space Exploration](skills/ultrathink.md#6-phase-3-solution-space-exploration) |
| **Trade-off evaluation** | "SQL vs NoSQL, which is more suitable?" | [**Section 6.2:** Comparison Matrix](skills/ultrathink.md#62-comparison-matrix) |
| **Risk analysis** | "What are the potential impacts of this change?" | [**Section 7:** Critical Evaluation (Pre-Mortem)](skills/ultrathink.md#7-phase-4-critical-evaluation) |

---

## 1.2 🏗️ Architecture - System Design
**File:** [skills/architecture.md](skills/architecture.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **New system design** | "Create e-commerce platform architecture" | [**Section 1:** Architectural Decision Process](skills/architecture.md#1-architectural-decision-process) |
| **Microservices decision** | "Which services should we split into?" | [**Section 3.1:** Monolith vs Microservices](skills/architecture.md#31-monolith-vs-microservices) |
| **Database selection** | "PostgreSQL or MongoDB?" | [**Section 5:** Database Selection](skills/architecture.md#5-database-selection) |
| **Scaling strategy** | "How to scale to 10x users?" | [**Section 4:** Scalability Patterns](skills/architecture.md#4-scalability-patterns) |
| **API gateway design** | "How to implement gateway pattern?" | [**Section 3:** Architectural Patterns](skills/architecture.md#3-architectural-patterns) |
| **Event-driven architecture** | "Communicate asynchronously with Kafka" | [**Section 3.3:** Event-Driven Architecture](skills/architecture.md#33-event-driven-architecture) |

---

## 1.3 🎨 Design System - UI/UX Guide
**File:** [skills/design-system.md](skills/design-system.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Component design** | "Create Button component" | [**Section 5:** Component Sizing](skills/design-system.md#5-component-sizing) |
| **Responsive layout** | "Setup mobile-first grid system" | [**Section 2:** Grid System](skills/design-system.md#2-layout--grid-system) / [**Section 6:** Breakpoints](skills/design-system.md#6-responsive-breakpoints) |
| **Color system** | "Add dark mode support" | [**Section 4:** Color System](skills/design-system.md#4-color-system) |
| **Typography** | "Determine font hierarchy" | [**Section 3:** Typography Scale](skills/design-system.md#3-typography-scale-type-scale) |
| **Spacing system** | "Apply 8-point grid" | [**Section 1:** Spacing System](skills/design-system.md#1-spacing-system-8-point-grid) |
| **Animation** | "Add micro-interaction" | [**Section 8:** Animation & Transitions](skills/design-system.md#8-animation--transitions) |
| **Accessibility** | "Make form WCAG compliant" | [**Section 12:** Accessibility Standards](skills/design-system.md#12-accessibility-standards) |

---

## 1.4 💻 Backend - Server-Side Development
**File:** [skills/backend.md](skills/backend.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Creating REST API** | "Write User CRUD endpoints" | [**Section 4:** API Design Rules](skills/backend.md#4-api-design-rules) |
| **Authentication** | "Setup JWT based auth system" | [**Section 6:** Security](skills/backend.md#6-security-best-practices) / [**Section 1.1:** Tech Stack](skills/backend.md#11-tech-stack) |
| **Database integration** | "Connect PostgreSQL with Prisma" | [**Section 7:** Database Patterns](skills/backend.md#7-database-patterns) |
| **Validation** | "Input validation with Zod" | [**Section 5:** Input Validation (Zod)](skills/backend.md#5-input-validation-zod) |
| **Error handling** | "Create global error handler" | [**Section 9:** Error Handling](skills/backend.md#9-error-handling) |
| **Caching** | "Apply Redis cache strategy" | [**Section 8:** Performance Optimization](skills/backend.md#8-performance-optimization) |
| **API security** | "Configure Rate limiting and CORS" | [**Section 6:** Security Best Practices](skills/backend.md#6-security-best-practices) |

---

## 1.5 📱 Mobile - Cross-Platform App
**File:** [skills/mobile.md](skills/mobile.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **React Native app** | "Start new project with Expo" | [**Section 2:** React Native Best Practices](skills/mobile.md#2-react-native-best-practices) |
| **Flutter app** | "Apply Material 3 UI" | [**Section 3:** Flutter Best Practices](skills/mobile.md#3-flutter-best-practices) |
| **State management** | "Setup Zustand/Riverpod" | [**Section 2.4 / 3:** State Management](skills/mobile.md#2-react-native-best-practices) |
| **Navigation** | "Setup Stack/Tab navigator" | [**Section 2 / 3:** Navigation](skills/mobile.md#2-react-native-best-practices) |
| **Native features** | "Add camera/location access" | [**Section 5:** Platform-Specific Code](skills/mobile.md#5-platform-specific-code) |
| **Offline support** | "Local storage with SQLite" | [**Section 4.1:** Secure Data Storage](skills/mobile.md#4-mobile-security) |
| **Push notifications** | "Integrate Firebase notification" | [**Section 8:** Must Do List](skills/mobile.md#8-must-do-list) |

---

## 1.6 🧪 Testing - TDD and Test Strategies
**File:** [skills/testing.md](skills/testing.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Writing Unit tests** | "Write tests for UserService" | [**Section 2:** Unit Testing (Jest)](skills/testing.md#2-unit-testing-jest) |
| **Integration test** | "Create API endpoint tests" | [**Section 3:** Integration Testing](skills/testing.md#3-integration-testing) |
| **E2E testing** | "Write Playwright tests" | [**Section 4:** E2E Testing](skills/testing.md#4-e2e-testing-playwright) |
| **Coverage** | "Get test coverage report" | [**Section 1:** Test Pyramid (Strategy)](skills/testing.md#1-test-pyramid) |

---

## 1.7 🔍 Debugging
**File:** [skills/debugging.md](skills/debugging.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Runtime error** | "TypeError: Cannot read property" | [**Section 2:** REPRODUCE](skills/debugging.md#2-phase-1-reproduce) |
| **Intermittent bug** | "Sometimes works, sometimes doesn't" | [**Section 4:** ISOLATE](skills/debugging.md#4-phase-3-isolate) |
| **Performance issue** | "Page loads very slowly" | [**Section 2:** REPRODUCE (Observation)](skills/debugging.md#2-phase-1-reproduce) |
| **Memory leak** | "App slows down over time" | [**Section 5:** Hypothesis Generation](skills/debugging.md#5-phase-4-hypothesize) |
| **Race condition** | "Data comes in wrong sometimes" | [**Section 5:** Common Bug Patterns](skills/debugging.md#5-phase-4-hypothesize) |
| **Production bug** | "Error occurring only in production" | [**Section 8:** REFLECT (Post-Mortem)](skills/debugging.md#8-phase-7-reflect) |
| **Regression** | "Old feature broke" | [**Section 4.1:** Binary Search](skills/debugging.md#4-phase-3-isolate) |

---

## 1.8 ♻️ Refactoring - Code Improvement
**File:** [skills/refactoring.md](skills/refactoring.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Cleaning Code Smell** | "This function is too long" | [**Section 5:** Code Smells](skills/refactoring.md#5-code-smells) |
| **Applying DRY** | "Merge duplicate code" | [**Section 4:** Refactoring Patterns](skills/refactoring.md#4-common-refactoring-patterns) |
| **Extract function** | "Break down large function" | [**Section 4.1:** Extract Function](skills/refactoring.md#41-extract-function) |
| **Rename refactoring** | "Give more meaningful names" | [**Section 3:** Refactoring Process (Small Steps)](skills/refactoring.md#3-refactoring-process) |
| **Design pattern** | "Apply Strategy pattern" | [**Section 4:** Patterns](skills/refactoring.md#4-common-refactoring-patterns) |
| **Legacy code** | "Modernize old code" | [**Section 7:** Incremental Refactoring](skills/refactoring.md#7-incremental-refactoring-strategy) |
| **Type safety** | "Remove any's" | [**Section 6:** Safe Checklist](skills/refactoring.md#6-safe-refactoring-checklist) |

---

## 1.9 🚀 Production Deployment - DevOps
**File:** [skills/production-deployment.md](skills/production-deployment.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **CI/CD pipeline** | "Setup GitHub Actions workflow" | [**Section 3:** CI/CD Pipeline](skills/production-deployment.md#3-cicd-pipeline) |
| **Docker deployment** | "Containerize and deploy" | [**Section 4.3:** Deployment Strategies](skills/production-deployment.md#4-deployment-strategies) |
| **Environment setup** | "Separate Staging/production" | [**Section 3:** Pipeline (Environment)](skills/production-deployment.md#3-cicd-pipeline) |
| **Blue-green deploy** | "Zero-downtime deployment" | [**Section 4:** Deployment Strategies](skills/production-deployment.md#4-deployment-strategies) |
| **Monitoring setup** | "Install Prometheus/Grafana" | [**Section 5:** Monitoring & Observability](skills/production-deployment.md#5-monitoring--observability) |
| **Rollback** | "Revert to previous version" | [**Section 6:** Rollback Strategy](skills/production-deployment.md#6-rollback-strategy) |
| **Security scan** | "Add Snyk to pipeline" | [**Section 2:** Pre-Deployment](skills/production-deployment.md#2-pre-deployment-checklist) / [**Section 3:** Security](skills/production-deployment.md#3-cicd-pipeline) |

---

## 1.10 📁 Multi-File Sync - Multi-File Changes
**File:** [skills/multi-file-sync.md](skills/multi-file-sync.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Global rename** | "Change userId to customerId in entire project" | [**Section 2:** Change Process (Planning)](skills/multi-file-sync.md#2-multi-file-change-process) |
| **API versioning** | "Migrate from v1 to v2" | [**Section 7:** Checklist](skills/multi-file-sync.md#7-checklist) |
| **Folder restructure** | "Switch to Feature-first structure" | [**Section 4:** Context Preservation](skills/multi-file-sync.md#4-context-preservation) |
| **Import path update** | "Change alias" | [**Section 3:** Tools and Techniques](skills/multi-file-sync.md#3-tools-and-techniques) |
| **Type definition change** | "Extend Interface, update all usages" | [**Section 5:** Dangerous Situations](skills/multi-file-sync.md#5-dangerous-situations) |
| **Config migration** | "Rename ENV variables" | [**Section 6:** Rollback Strategies](skills/multi-file-sync.md#6-rollback-strategies) |

---

## 1.11 📦 Dependency Management
**File:** [skills/dependency-management.md](skills/dependency-management.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Security audit** | "Run npm audit and fix" | [**Section 3:** Security Auditing](skills/dependency-management.md#3-security-auditing) |
| **Major upgrade** | "Upgrade React 18 to 19" | [**Section 5:** Upgrade Strategy](skills/dependency-management.md#5-upgrade-strategy) |
| **Dependency cleanup** | "Remove unused packages" | [**Section 7:** Dependency Cleanup](skills/dependency-management.md#7-dependency-cleanup) |
| **Version conflict** | "Resolve peer dependency error" | [**Section 4:** Version Management](skills/dependency-management.md#4-version-management) |
| **Lock file issue** | "package-lock.json issue" | [**Section 6:** Lock File Management](skills/dependency-management.md#6-lock-file-management) |
| **Bundle size** | "Shrink bundle" | [**Section 8:** Dependency Monitoring](skills/dependency-management.md#8-dependency-monitoring) |
| **License check** | "Check license compliance" | [**Section 2:** Package Addition Decision](skills/dependency-management.md#2-package-addition-decision) |

---

## 1.12 📝 Documentation
**File:** [skills/documentation.md](skills/documentation.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Writing README** | "Create Project README" | [**Section 2:** README Best Practices](skills/documentation.md#2-readme-best-practices) |
| **API docs** | "OpenAPI/Swagger documentation" | [**Section 4:** API Documentation](skills/documentation.md#4-api-documentation) |
| **Code comments** | "Document functions with JSDoc" | [**Section 3:** Code Documentation](skills/documentation.md#3-code-documentation) |
| **Architecture docs** | "Create system diagrams" | [**Section 6:** Architecture Documentation](skills/documentation.md#6-architecture-documentation) |
| **Changelog** | "Update CHANGELOG.md" | [**Section 5:** Changelog](skills/documentation.md#5-changelog) |
| **Writing ADR** | "Document architectural decision" | [**Section 6.1:** ADR](skills/documentation.md#61-architecture-decision-records-adr) |
| **Onboarding guide** | "New developer guide" | [**Section 2:** README](skills/documentation.md#2-readme-best-practices) |

---

## 1.13 ⚡ Optimization - System & Flow Optimization
**File:** [skills/optimization.md](skills/optimization.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Bottleneck detection** | "Find slow steps in user flow" | [**Section 2:** Bottleneck Detection](skills/optimization.md#2-bottleneck-identification) |
| **User flow analysis** | "Identify friction points" | [**Section 5:** Frontend & UX Optimization](skills/optimization.md#5-frontend--ux-optimization) |
| **Performance tuning** | "AI powered system optimization" | [**Section 3:** AI-Driven Optimization](skills/optimization.md#3-ai-driven-optimization) |
| **Observability** | "Setup observability with OpenTelemetry" | [**Section 4:** Modern Observability](skills/optimization.md#4-modern-observability) |
| **RUM & Metrics** | "Integrate Real User Monitoring" | [**Section 5:** RUM & Metrics](skills/optimization.md#5-frontend--ux-optimization) |
| **Value Stream** | "Remove unnecessary steps in processes" | [**Section 7:** Systematic Improvement Cycle](skills/optimization.md#7-systematic-improvement-cycle) |

---

# 2. Skill Loading Protocol

## 2.1 Step 1: Task Analysis
```
Read user task
    │
    ▼
Determine appropriate skill(s) from tables above
    │
    ▼
Load skill file: skills/<skill-name>.md
```

## 2.2 Step 2: If Skill Not Found
```
⚠️ ERROR: "[skill-name].md" skill file not found.

Please do one of the following:
1. Show the path of the skill file
2. Create the skill file

Operations CANNOT START without Skills.
```

---

# 3. Skill Combinations

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
| **Performance Improvement** | optimization + ultrathink + debugging | 1→2→3 |

---

# 4. Skills Directory Structure

```
c:\Users\Mehmet\Desktop\global_workflows\en_version\
├── GEMINI.md           ← Global rules
├── CORE.md             ← This file (Central orchestrator)
└── skills/
    ├── ultrathink.md           ✅ Deep thinking
    ├── architecture.md         ✅ System design
    ├── design-system.md        ✅ UI/UX guide
    ├── backend.md              ✅ Server-side development
    ├── mobile.md               ✅ Cross-platform mobile
    ├── testing.md              ✅ TDD and test strategies
    ├── debugging.md            ✅ Debugging
    ├── refactoring.md          ✅ Code improvement
    ├── production-deployment.md ✅ DevOps/CI-CD
    ├── multi-file-sync.md      ✅ Multi-file change
    ├── dependency-management.md ✅ Package management
    ├── documentation.md        ✅ Documentation
    └── optimization.md         ✅ System & Flow Optimization
```

---

# 5. Critical Rules

> [!CAUTION]
> **DO NOT START operation without loading Skill!**
> Appropriate skill(s) MUST be loaded for every task.

> [!WARNING]
> **DO NOT STOP if Skill is not found!**
> Ask user for file path or suggest creating the skill.

> [!IMPORTANT]
> **GEMINI.md rules are always applicable!**
> ESLint check, 2x code review must be performed.

---

**Last Update:** December 2025
**Version:** 3.1
