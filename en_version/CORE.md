---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> This file is the central routing point for all tasks.
> Appropriate skill(s) are determined and loaded based on the task type.

---

## 🔧 DYNAMIC PATH DETECTION (Automatic)

> [!NOTE]
> **For AI Agent:** When reading this file, **automatically detect** the paths.
> Determine directory structure based on user's home directory.

### Installation Structure

```
~/.gemini/
├── GEMINI.md                    # Global rules
└── antigravity/
    ├── CORE.md                  # This file (Central orchestrator)
    └── global_workflows/
        └── skills/              # Skill files

~/.agent/                        # Antigravity IDE Rules & Workflows
├── rules/                       # 15 workspace rules (Model Decision/Glob/Always On)
└── workflows/                   # 8 slash commands (/ultrathink, /plan, etc.)
```

**Placeholder Definitions:**
| Placeholder | Meaning |
|-------------|---------|
| `{ANTIGRAVITY_DIR}` | `~/.gemini/antigravity/` directory |
| `{SKILLS_DIR}` | `~/.gemini/antigravity/global_workflows/skills/` directory |
| `{AGENT_DIR}` | `~/.agent/` directory |
| `{RULES_DIR}` | `~/.agent/rules/` directory |
| `{WORKFLOWS_DIR}` | `~/.agent/workflows/` directory |

---

# 📋 Contents

1. [Skills Reference - Which Skill When?](#1-skills-reference---which-skill-when)
    - [1.1 🧠 UltraThink](#11-🧠-ultrathink---deep-thinking-protocol)
    - [1.2 🏗️ Architecture](#12-🏗️-architecture---system-design)
    - [1.3 🎨 Design System](#13-🎨-design-system---uiux-guide)
    - [1.4 💻 Backend](#14-💻-backend---server-side-development)
    - [1.5 📱 Mobile](#15-📱-mobile---cross-platform-app)
    - [1.6 🧪 Testing](#16-🧪-testing---tdd-and-test-strategies)
    - [1.7 🔍 Debugging](#17-🔍-debugging---troubleshooting)
    - [1.8 ♻️ Refactoring](#18-♻️-refactoring---code-improvement)
    - [1.9 🚀 Production Deployment](#19-🚀-production-deployment---devops)
    - [1.10 📁 Multi-File Sync](#110-📁-multi-file-sync---multi-file-changes)
    - [1.11 📦 Dependency Management](#111-📦-dependency-management---package-management)
    - [1.12 📝 Documentation](#112-📝-documentation---documentation)
    - [1.13 ⚡ Optimization](#113-⚡-optimization---system--flow-optimization)
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
| **Socratic Reality Check** | "What does the user want? What am I doing?" | [**Section 3:** Socratic Reality Check](skills/ultrathink.md#socratic-reality-check-5-step-reality-check) |
| **Meta-Planning** | "How should we break down this complex task?" | [**Section 3:** Phase 0 - Meta-Planning](skills/ultrathink.md#3-phase-0-meta-planning) |
| **Problem Analysis** | "What is the root cause of the problem?" | [**Section 4:** Phase 1 - Problem Understanding](skills/ultrathink.md#4-phase-1-problem-understanding) |
| **Hypothesis Calibration** | "How sure are we of the solution? (Confidence %)" | [**Section 5.2:** Confidence Calibration](skills/ultrathink.md#52-hypothesis-confidence-calibration) |
| **Solution Generation** | "What are the alternative solutions?" | [**Section 6:** Phase 3 - Solution Space](skills/ultrathink.md#6-phase-3-solution-space-exploration) |
| **Trade-off Analysis** | "Prepare a comparison matrix" | [**Section 6.2:** Comparison Matrix](skills/ultrathink.md#62-comparison-matrix) |
| **Critical Evaluation** | "Let's do a pre-mortem (Risk analysis)" | [**Section 7:** Phase 4 - Critical Evaluation](skills/ultrathink.md#7-phase-4-critical-evaluation) |
| **Devil's Advocate** | "Try to disprove the solution" | [**Section 7.1:** Devil's Advocate](skills/ultrathink.md#71-devils-advocate) |
| **Edge Case Analysis** | "What are the boundary conditions?" | [**Section 8:** Phase 5 - Edge Case Matrix](skills/ultrathink.md#8-phase-5-edge-case-analysi) |
| **Bias Control** | "Are we thinking with bias?" | [**Section 9.2:** Bias Detection](skills/ultrathink.md#92-bias-detection-and-correction) |
| **Synthesis and Decision** | "Make the final decision and document it" | [**Section 10:** Phase 7 - Synthesis and Decision](skills/ultrathink.md#10-phase-7-synthesis-and-decision) |

---

## 1.2 🏗️ Architecture - System Design
**File:** [skills/architecture.md](skills/architecture.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Process Management** | "How does the architectural decision process work?" | [**Section 1:** Decision Process](skills/architecture.md#1-architectural-decision-process) |
| **Requirements Analysis** | "What are the non-functional requirements?" | [**Section 2:** Requirements (Func vs Non-Func)](skills/architecture.md#2-functional-vs-non-functional-requirements) |
| **Architecture Selection** | "Monolith vs Microservices?" | [**Section 3.1:** Monolith vs Microservices](skills/architecture.md#31-monolith-vs-microservices) |
| **Layered Architecture** | "Apply layered architecture" | [**Section 3.2:** Layered Architecture](skills/architecture.md#32-layered-architecture) |
| **Event-Driven** | "Setup Async/Event-driven structure" | [**Section 3.3:** Event-Driven Architecture](skills/architecture.md#33-event-driven-architecture) |
| **CQRS** | "Separate Command and Query" | [**Section 3.4:** CQRS](skills/architecture.md#34-cqrs-command-query-responsibility-segregation) |
| **Scaling** | "Scale the system (Horizontal/Vertical)" | [**Section 4.1:** Horizontal vs Vertical Scaling](skills/architecture.md#41-horizontal-vs-vertical-scaling) |
| **Load Balancing** | "Load balancer strategy" | [**Section 4.2:** Load Balancing](skills/architecture.md#42-load-balancing) |
| **Caching** | "Setup cache mechanism" | [**Section 4.3:** Caching Strategy](skills/architecture.md#43-caching-strategy) |
| **Database Selection** | "SQL vs NoSQL decision" | [**Section 5:** Database Selection](skills/architecture.md#5-database-selection) |
| **Validation** | "Validate with POC" | [**Section 1 (Step 6):** Validate](skills/architecture.md#1-architectural-decision-process) |

---

## 1.3 🎨 Design System - UI/UX Guide
**File:** [skills/design-system.md](skills/design-system.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Design Process** | "Design step-by-step (CoT)" | [**Section 15:** Chain-of-Thought Prompt](skills/design-system.md#15-chain-of-thought-prompt-adım-adım-düşünme) |
| **Dynamic Decision** | "Adapt based on project type" | [**Section 16:** Contextual Flexibility](skills/design-system.md#16-dinamik-karar-alma---bağlamsal-esneklik) |
| **Component Design** | "Create Button/Card" | [**Section 5:** Component Sizing](skills/design-system.md#5-component-sizing) |
| **Spacing & Layout** | "8-point grid and container structure" | [**Section 1:** Spacing](skills/design-system.md#1-spacing-system-8-point-grid) / [**Section 2:** Layout](skills/design-system.md#2-layout--grid-system) |
| **Visual Hierarchy** | "Adjust Shadow and Z-index" | [**Section 7:** Visual Hierarchy](skills/design-system.md#7-visual-hierarchy) |
| **Micro-interactions** | "Hover and Loading states" | [**Section 10:** Micro-interactions](skills/design-system.md#10-micro-interactions) |
| **Modern CSS** | "Use Container Query" | [**Section 11:** Modern CSS (2025)](skills/design-system.md#11-modern-css-features-2025) |
| **Typography** | "Apply fluid typography" | [**Section 3:** Typography / Fluid Scale](skills/design-system.md#3-typography-scale-type-scale) |
| **Color & Theme** | "Dark mode and contrast" | [**Section 4:** Color System](skills/design-system.md#4-color-system) |
| **Responsive** | "Make mobile compatible" | [**Section 6:** Breakpoints](skills/design-system.md#6-responsive-breakpoints) |
| **Animation** | "Add transition effects" | [**Section 8:** Animation](skills/design-system.md#8-animation--transitions) |
| **Accessibility** | "Make accessible (a11y)" | [**Section 12:** Accessibility](skills/design-system.md#12-accessibility-standards) |

---

## 1.4 💻 Backend - Server-Side Development
**File:** [skills/backend.md](skills/backend.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **API Design** | "REST standards route" | [**Section 4:** API Design Best Practices](skills/backend.md#4-api-design-best-practices) |
| **Response Format** | "Standard API response" | [**Section 4.2:** Response Format Standard](skills/backend.md#42-response-format-standardı) |
| **Validation** | "Zod input validation" | [**Section 5:** Input Validation (Zod)](skills/backend.md#5-input-validation-zod) |
| **Security** | "Rate limit and Helmet" | [**Section 6:** Security Best Practices](skills/backend.md#6-security-best-practices) |
| **Authentication** | "JWT and Role-based auth" | [**Section 6:** Auth Middleware](skills/backend.md#6-security-best-practices) |
| **Database Patterns** | "Repository pattern" | [**Section 7.1:** Repository Pattern](skills/backend.md#71-repository-pattern) |
| **Transactions** | "Atomic transaction management" | [**Section 7.2:** Transaction Handling](skills/backend.md#72-transaction-handling) |
| **Performance** | "Redis caching integration" | [**Section 8.2:** Caching (Redis)](skills/backend.md#82-caching-redis) |
| **Error Handling** | "Global error handler" | [**Section 9:** Error Handling](skills/backend.md#9-error-handling) |
| **Folder Structure** | "Domain-driven file structure" | [**Section 3:** Project Structure](skills/backend.md#3-project-structure) |
| **Tech Stack** | "Hono.js / Modern Stack" | [**Section 1:** Tech Stack & Tools](skills/backend.md#1-tech-stack--tools) |

---

## 1.5 📱 Mobile - Cross-Platform App
**File:** [skills/mobile.md](skills/mobile.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Setup & Project** | "Setup RN or Flutter project" | [**Section 2.1 / 3.1:** Project Structure](skills/mobile.md#2-react-native-best-practices) |
| **Component Standard** | "Write modern component" | [**Section 2.2 / 3.2:** Best Practices](skills/mobile.md#22-functional-components--hooks) |
| **Performance** | "Use FlashList" | [**Section 2.3 / 3.3:** Performance Optimization](skills/mobile.md#23-performance-optimization) |
| **State Management** | "Zustand integration" | [**Section 2.4 / 3.4:** State Management](skills/mobile.md#24-state-management-zustand) |
| **Navigation** | "Setup Stack/Tab navigation" | [**Section 2.6 / 3.5:** Navigation](skills/mobile.md#26-navigation-react-navigation) |
| **Security** | "Store tokens securely" | [**Section 4.1:** Secure Storage](skills/mobile.md#41-secure-storage) |
| **API Security** | "Certificate pinning" | [**Section 4.2:** API Security](skills/mobile.md#42-api-security) |
| **Platform Features** | "Camera/Location logic" | [**Section 5:** Platform-Specific Code](skills/mobile.md#5-platform-specific-code) |
| **Offline First** | "Strategy for offline work" | [**Section 4:** Mobile Security & Storage](skills/mobile.md#4-mobile-security) |

---

## 1.6 🧪 Testing - TDD and Test Strategies
**File:** [skills/testing.md](skills/testing.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Strategy Setup** | "How should the test pyramid be?" | [**Section 1:** Test Pyramid](skills/testing.md#1-test-piramidi) |
| **Unit Test** | "Test component with Jest" | [**Section 2:** Unit Testing (Jest)](skills/testing.md#2-unit-testing-jest) |
| **Mocking** | "Mock the API call" | [**Section 2.2:** Mocking](skills/testing.md#22-mocking) |
| **Integration Test** | "API endpoint test" | [**Section 3:** Integration Testing](skills/testing.md#3-integration-testing) |
| **E2E Test** | "Test login with Playwright" | [**Section 4:** E2E Testing (Playwright)](skills/testing.md#4-e2e-testing-playwright) |
| **Visual Test** | "Catch UI regressions" | [**Section 5:** Visual Regression Testing](skills/testing.md#5-visual-regression-testing) |
| **TDD Workflow** | "Red-Green-Refactor" | [**Section 6:** TDD](skills/testing.md#6-tdd-test-driven-development) |
| **Best Practices** | "AAA pattern" | [**Section 7:** Test Writing Rules](skills/testing.md#7-test-yazım-kuralları) |
| **Quality Control** | "Analyze coverage" | [**Section 8:** Checklist](skills/testing.md#8-kontrol-listesi) |

---

## 1.7 🔍 Debugging - troubleshooting
**File:** [skills/debugging.md](skills/debugging.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Reproduce** | "Reproduce error" | [**Section 2:** Phase 1 - Reproduce](skills/debugging.md#2-faz-1-reproduce-tekrarla) |
| **Root Cause (RCA)** | "Why did it occur?" | [**Section 3/5:** Root Cause Analysis](skills/debugging.md#3-faz-2-understand-anla) |
| **Isolation** | "Narrow down with Binary search" | [**Section 4:** Phase 3 - Isolate](skills/debugging.md#4-faz-3-isolate-izolasyon) |
| **Hypothesis Testing** | "Test likely cause" | [**Section 5:** Phase 4 - Hypothesize](skills/debugging.md#5-faz-4-hypothesize-hipotez) |
| **Network Debugging** | "Inspect API requests" | [**Section 6.3:** Network Debugging](skills/debugging.md#63-network-debugging) |
| **Logging** | "Add structured log" | [**Section 9.2:** Structured Logging](skills/debugging.md#92-structured-logging) |
| **Common Patterns** | "Race condition" | [**Section 5.2:** Common Bug Patterns](skills/debugging.md#52-common-bug-patterns) |
| **Post-Mortem** | "Write incident report" | [**Section 8:** Phase 7 - Reflect](skills/debugging.md#8-faz-7-reflect-yansıtma) |
| **Tools** | "Use VS Code debugger" | [**Section 6:** Phase 5 - Fix & Tools](skills/debugging.md#6-faz-5-fix--tools) |

---

## 1.8 ♻️ Refactoring - Code Improvement
**File:** [skills/refactoring.md](skills/refactoring.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Timing** | "Should I refactor?" | [**Section 2:** When to Refactor?](skills/refactoring.md#2-ne-zaman-refactor) |
| **Code Smells** | "Long method" | [**Section 5:** Code Smells](skills/refactoring.md#5-code-smells) |
| **Process** | "Small steps" | [**Section 3:** Refactoring Process](skills/refactoring.md#3-refactoring-süreci-küçük-adımlar) |
| **Extract Patterns** | "Extract Method" | [**Section 4.1:** Extract Function](skills/refactoring.md#41-extract-function) |
| **Rename & Simplify** | "Rename symbol" | [**Section 4.2:** Rename Variable](skills/refactoring.md#4-common-refactoring-patterns) |
| **DRY** | "Clean up duplicates" | [**Section 4.5:** Remove Duplication](skills/refactoring.md#45-remove-duplication-dry) |
| **Magic Numbers** | "Make constants" | [**Section 4.3:** Replace Magic Numbers](skills/refactoring.md#43-replace-magic-numbers-with-constants) |
| **Legacy Code** | "Safely change old code" | [**Section 7:** Incremental Refactoring](skills/refactoring.md#7-incremental-refactoring-strategy) |
| **Safe Checklist** | "Type safety check" | [**Section 6 / 8:** Checklist](skills/refactoring.md#8-kontrol-listesi) |

---

## 1.9 🚀 Production Deployment - DevOps
**File:** [skills/production-deployment.md](skills/production-deployment.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Preparation** | "Check Deployment Checklist" | [**Section 2:** Pre-Deployment Checklist](skills/production-deployment.md#2-pre-deployment-checklist) |
| **Pipeline Setup** | "GitHub Actions CI/CD" | [**Section 3:** CI/CD Pipeline](skills/production-deployment.md#3-cicd-pipeline) |
| **Secrets** | "Manage env vars" | [**Section 3.2:** Pipeline Security](skills/production-deployment.md#32-pipeline-security) |
| **Strategy Selection** | "Blue-Green or Canary" | [**Section 4:** Deployment Strategies](skills/production-deployment.md#4-deployment-stratejileri-deployment-strategies) |
| **Feature Flags** | "A/B testing" | [**Section 4.3:** Feature Flags](skills/production-deployment.md#43-feature-flags) |
| **Monitoring** | "Grafana metrics" | [**Section 5:** Monitoring & Observability](skills/production-deployment.md#5-monitoring--observability) |
| **Alerting** | "Alert on error rate" | [**Section 5.3:** Alert Rules](skills/production-deployment.md#53-alert-rules) |
| **Rollback** | "Revert emergency" | [**Section 6:** Rollback Strategy](skills/production-deployment.md#6-rollback-strategy) |
| **Security** | "Security scan" | [**Section 7:** Security & Compliance](skills/production-deployment.md#7-security--compliance) |

---

## 1.10 📁 Multi-File Sync - Multi-File Changes
**File:** [skills/multi-file-sync.md](skills/multi-file-sync.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Planning** | "Affects 20 files" | [**Section 2:** Change Process](skills/multi-file-sync.md#2-multi-file-değişiklik-süreci) |
| **Global Rename** | "Rename symbol globally" | [**Section 3.1:** IDE Refactoring](skills/multi-file-sync.md#31-ide-refactoring-rename-symbol) |
| **Grep Check** | "Find references" | [**Section 3.2:** Grep check](skills/multi-file-sync.md#32-grep-ile-kontrol) |
| **Context** | "Preserve context" | [**Section 4:** Context Preservation](skills/multi-file-sync.md#42-git-stash-kullanımı) |
| **Dangerous Situations** | "Interface changed" | [**Section 5:** Dangerous Situations](skills/multi-file-sync.md#5-tehlikeli-durumlar) |
| **Rollback** | "Revert major change" | [**Section 6:** Rollback Strategies](skills/multi-file-sync.md#6-rollback-stratejileri) |
| **Checklist** | "Did I miss anything?" | [**Section 7:** Checklist](skills/multi-file-sync.md#7-kontrol-listesi) |

---

## 1.11 📦 Dependency Management - Package Management
**File:** [skills/dependency-management.md](skills/dependency-management.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Package Selection** | "Should I use this?" | [**Section 2:** Addition Decision](skills/dependency-management.md#2-paket-ekleme-kararı) |
| **Audit** | "Scan security" | [**Section 3:** Security Auditing](skills/dependency-management.md#3-security-auditing) |
| **Versioning** | "Tilde vs Caret" | [**Section 4:** Version Management](skills/dependency-management.md#4-version-management) |
| **Upgrade** | "Safely upgrade" | [**Section 5:** Upgrade Strategy](skills/dependency-management.md#5-upgrade-stratejisi) |
| **Lock File** | "Lock file conflict" | [**Section 6:** Lock File Management](skills/dependency-management.md#6-lock-file-yönetimi) |
| **Cleanup** | "Remove unused" | [**Section 7:** Dependency Cleanup](skills/dependency-management.md#7-dependency-cleanup) |
| **Monitoring** | "Setup Dependabot" | [**Section 8:** Dependency Monitoring](skills/dependency-management.md#8-dependency-monitoring) |

---

## 1.12 📝 Documentation - Documentation
**File:** [skills/documentation.md](skills/documentation.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **README** | "Prepare project entry" | [**Section 2:** README Best Practices](skills/documentation.md#2-readme-best-practices) |
| **Code Comments** | "Write TSDoc" | [**Section 3:** Code Documentation](skills/documentation.md#3-code-documentation) |
| **API Docs** | "Create Swagger spec" | [**Section 4:** API Documentation](skills/documentation.md#4-api-documentation) |
| **Changelog** | "Keep history" | [**Section 5:** Changelog & Versioning](skills/documentation.md#5-changelog--versioning) |
| **ADR** | "Record decision" | [**Section 6.1:** ADR](skills/documentation.md#61-architecture-decision-records-adr) |
| **Diagrams** | "Draw Mermaid diagram" | [**Section 6.2:** Architecture Diagrams](skills/documentation.md#62-architecture-diagrams-c4-model) |
| **Technical Writing** | "Write clearly" | [**Section 7:** Technical Writing Style](skills/documentation.md#7-technical-writing-best-practices) |

---

## 1.13 ⚡ Optimization - System & Flow Optimization
**File:** [skills/optimization.md](skills/optimization.md)

| Scenario | Example | Relevant Section |
|---------|-------|--------------|
| **Bottleneck Detection** | "Why slow?" | [**Section 2:** Bottleneck Identification](skills/optimization.md#2-darboğaz-tespiti-bottleneck-identification) |
| **AI Analysis** | "Analyze with AI" | [**Section 3:** AI-Driven Optimization](skills/optimization.md#3-ai-driven-optimizasyon) |
| **Observability** | "Measure LCP/INP" | [**Section 5:** Frontend & UX](skills/optimization.md#5-frontend--kullanıcı-deneyimi-optimizasyonu) |
| **Backend Tuning** | "N+1 query problem" | [**Section 6:** Backend & DB Tuning](skills/optimization.md#6-backend--veritabanı-optimizasyonu) |
| **Improvement Cycle** | "Measure -> Analyze -> Improve" | [**Section 7:** Improvement Cycle](skills/optimization.md#7-sistematik-iyileştirme-döngüsü) |
| **Principles** | "Avoid premature optimization" | [**Section 1:** Optimization Principles](skills/optimization.md#1-optimizasyon-prensipleri-2025) |
| **Observability Tools** | "OpenTelemetry setup" | [**Section 4:** Modern Observability](skills/optimization.md#4-modern-gözlemlenebilirlik) |

---

# 2. Skill Loading Protocol

## 2.1 Step 1: Precise Task Analysis
```
Analyze user task
    │
    ▼
Find SKILL and RELEVANT SECTION from CORE.md tables
    │
    ▼
DO NOT READ the skill file completely ❌
Only read the relevant section and rules ✅
```

## 2.2 Step 2: Selective Reading Protocol

**Instead of reading the entire file:**

1. **Identify Target:** Determine the relevant section header (e.g., `# 5. Component Sizing`).
2. **Find Location:** Locate the line number of this header in the file (e.g., using `view_file_outline` or `grep_search`).
3. **Partial Read:** Read only the range containing that section and its subsections (e.g., using `view_file` with startLine-endLine).

> [!TIP]
> This method preserves context limits and increases focus.

## 2.3 Step 3: If Skill Not Found
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

{WORKFLOWS_ROOT}/
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
**Version:** 1.3
