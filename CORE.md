---
description: Central Orchestrator & Skills Registry. Loads automatically to route tasks to the appropriate Skills, Modes, or Guards.
---

# CORE.md - Skills Orchestrator

> This file is the central routing point for all tasks.
> Based on the task type, appropriate skill(s) are identified and loaded.

---

## 🔧 DYNAMIC PATH DETECTION (Automatic)

> [!NOTE]
> **For AI Agent:** When you read this file, **automatically detect** the paths.
> Determine the directory structure based on the user's home directory.

### Installation Structure

```
~/.gemini/
├── GEMINI.md                    # This file (Global rules)
└── antigravity/
    ├── CORE.md                  # This file (Central orchestrator)
    └── global_workflows/
        └── skills/              # Skill files

~/.agent/                        # Antigravity IDE Rules & Workflows
├── rules/                       # 16 workspace rules
└── workflows/                   # 8 slash command workflows
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

# 📋 Table of Contents

1. [Skills Reference - When to Use Which Skill](#1-skills-reference---when-to-use-which-skill)
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
    - [1.12 📝 Documentation](#112-📝-documentation---docs)
    - [1.13 ⚡ Optimization](#113-⚡-optimization---system--flow-optimization)
    - [1.14 🔍 SEO Fundamentals](#114-🔍-seo-fundamentals---core-principles--e-e-a-t)
    - [1.15 ⚙️ SEO Technical](#115-⚙️-seo-technical---technical-seo--core-web-vitals)
    - [1.16 ✍️ SEO Content](#116-✍️-seo-content---content-strategy--on-page-seo)
    - [1.17 📍 SEO Local](#117-📍-seo-local---local-seo--geographic-optimization)
    - [1.18 🔗 SEO Off-Page](#118-🔗-seo-off-page---link-building--backlinks)
    - [1.19 📊 SEO Analytics](#119-📊-seo-analytics---measurement--reporting)
    - [1.20 🤖 GEO Fundamentals](#120-🤖-geo-fundamentals---generative-engine-optimization)
    - [1.21 ✍️ GEO Content](#121-✍️-geo-content---ai-friendly-content-strategy)
    - [1.22 ⚙️ GEO Technical](#122-⚙️-geo-technical---technical-optimization-for-ai-engines)
    - [1.23 📊 GEO Analytics](#123-📊-geo-analytics---ai-citation-tracking--measurement)
2. [Skill Loading Protocol](#2-skill-loading-protocol)
3. [Skill Combinations](#3-skill-combinations)
4. [Skills Directory Structure](#4-skills-directory-structure)
5. [Critical Rules](#5-critical-rules)

---

# 1. Skills Reference - When to Use Which Skill

> [!NOTE]
> **Dynamic Matching:** Users may give commands that don't exactly match examples below.
> These tables are for **reference**. As an agent, analyze the user's request and
> **dynamically infer** the most appropriate skill(s) semantically.
> For example: "there's an issue with this API" → debugging + backend skills.

---

## 1.1 🧠 UltraThink - Deep Thinking Protocol
**File:** [skills/ultrathink.md](skills/ultrathink.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Socratic Reality Check** | "What does the user want? What am I doing?" | [**Section 3:** Socratic Reality Check](skills/ultrathink.md#socratic-reality-check-5-step-reality-check) |
| **Meta-Planning** | "How should we break down this complex task?" | [**Section 3:** Phase 0 - Meta-Planning](skills/ultrathink.md#3-phase-0-meta-planning) |
| **Problem Analysis** | "What's the root cause?" | [**Section 4:** Phase 1 - Problem Understanding](skills/ultrathink.md#4-phase-1-problem-understanding) |
| **Hypothesis Calibration** | "How confident are we in this solution? (Confidence %)" | [**Section 5.2:** Hypothesis Confidence Calibration](skills/ultrathink.md#52-hypothesis-confidence-calibration) |
| **Solution Generation** | "What are alternative solutions?" | [**Section 6:** Phase 3 - Solution Space](skills/ultrathink.md#6-phase-3-solution-space-exploration) |
| **Trade-off Analysis** | "Prepare comparison matrix" | [**Section 6.2:** Comparison Matrix](skills/ultrathink.md#62-comparison-matrix) |
| **Critical Evaluation** | "Let's do a pre-mortem (risk analysis)" | [**Section 7:** Phase 4 - Critical Evaluation](skills/ultrathink.md#7-phase-4-critical-evaluation) |
| **Devil's Advocate** | "Try to disprove the solution" | [**Section 7.1:** Devil's Advocate](skills/ultrathink.md#71-devils-advocate) |
| **Edge Case Analysis** | "What are edge cases? (Input/State)" | [**Section 8:** Edge Case Analysis](skills/ultrathink.md#8-phase-5-edge-case-analysis) |
| **Bias Check** | "Are we thinking with bias?" | [**Section 9.2:** Bias Detection](skills/ultrathink.md#92-bias-detection-and-correction) |
| **Synthesis & Decision** | "Make final decision and document" | [**Section 10:** Phase 7 - Synthesis and Decision](skills/ultrathink.md#10-phase-7-synthesis-and-decision) |

---

## 1.2 🏗️ Architecture - System Design
**File:** [skills/architecture.md](skills/architecture.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Process Management** | "How does architectural decision process work?" | [**Section 1:** Architectural Decision Process](skills/architecture.md#1-architectural-decision-process) |
| **Requirements Analysis** | "What are non-functional requirements?" | [**Section 2:** Requirements (Func vs Non-Func)](skills/architecture.md#2-functional-vs-non-functional-requirements) |
| **Architecture Selection** | "Monolith or Microservices?" | [**Section 3.1:** Monolith vs Microservices](skills/architecture.md#31-monolith-vs-microservices) |
| **Layered Architecture** | "Apply layered architecture" | [**Section 3.2:** Layered Architecture](skills/architecture.md#32-layered-architecture) |
| **Event-Driven** | "Build async/event-driven structure" | [**Section 3.3:** Event-Driven Architecture](skills/architecture.md#33-event-driven-architecture) |
| **CQRS** | "Separate Command and Query" | [**Section 3.4:** CQRS](skills/architecture.md#34-cqrs-command-query-responsibility-segregation) |
| **Scaling** | "Scale the system (Horizontal/Vertical)" | [**Section 4.1:** Horizontal vs Vertical Scaling](skills/architecture.md#41-horizontal-vs-vertical-scaling) |
| **Load Balancing** | "Load balancer strategy" | [**Section 4.2:** Load Balancing](skills/architecture.md#42-load-balancing) |
| **Caching** | "Set up cache mechanism" | [**Section 4.3:** Caching Strategy](skills/architecture.md#43-caching-strategy) |
| **Database Selection** | "SQL vs NoSQL decision" | [**Section 5:** Database Selection](skills/architecture.md#5-database-selection) |
| **Validation** | "Validate with POC" | [**Section 1 (Step 6):** Validate](skills/architecture.md#1-architectural-decision-process) |

---

## 1.3 🎨 Design System - UI/UX Guide
**File:** [skills/design-system.md](skills/design-system.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Design Process** | "Do design step by step (CoT)" | [**Section 15:** Chain-of-Thought Prompt](skills/design-system.md#15-chain-of-thought-prompt-step-by-step-thinking) |
| **Dynamic Decision** | "Be flexible based on project type (E-commerce/SaaS)" | [**Section 16:** Contextual Flexibility](skills/design-system.md#16-contextual-flexibility) |
| **Component Design** | "Create Button/Card component" | [**Section 5:** Component Sizing](skills/design-system.md#5-component-sizing) |
| **Spacing & Layout** | "8-point grid and container structure" | [**Section 1:** Spacing](skills/design-system.md#1-spacing-system-8-point-grid) / [**Section 2:** Layout](skills/design-system.md#2-layout--grid-system) |
| **Visual Hierarchy** | "Adjust Shadow and Z-index" | [**Section 7:** Visual Hierarchy](skills/design-system.md#7-visual-hierarchy) |
| **Micro-interactions** | "Hover and Loading states" | [**Section 10:** Micro-interactions](skills/design-system.md#10-micro-interactions) |
| **Modern CSS** | "Use Container Query" | [**Section 11:** Modern CSS (2025)](skills/design-system.md#11-modern-css-features-2025) |
| **Typography** | "Apply fluid typography" | [**Section 3:** Typography / Fluid Scale](skills/design-system.md#3-typography-scale-type-scale) |
| **Color & Theme** | "Dark mode and contrast" | [**Section 4:** Color System](skills/design-system.md#4-color-system) |
| **Responsive** | "Make mobile compatible" | [**Section 6:** Breakpoints](skills/design-system.md#6-responsive-breakpoints) |
| **Animation** | "Add transition effects" | [**Section 8:** Animation](skills/design-system.md#8-animation--transitions) |
| **Accessibility** | "Make accessible (a11y)" | [**Section 12:** Accessibility Standards](skills/design-system.md#12-accessibility-standards) |

---

## 1.4 💻 Backend - Server-Side Development
**File:** [skills/backend.md](skills/backend.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **API Design** | "Create REST compliant routes" | [**Section 4:** API Design Best Practices](skills/backend.md#4-api-design-best-practices) |
| **Response Format** | "Return standard API response" | [**Section 4.2:** Response Format Standard](skills/backend.md#42-response-format-standard) |
| **Validation** | "Validate input with Zod" | [**Section 5:** Input Validation (Zod)](skills/backend.md#5-input-validation-zod) |
| **Security** | "Add rate limit and Helmet" | [**Section 6:** Security Best Practices](skills/backend.md#6-security-best-practices) |
| **Authentication** | "JWT and Role-based auth" | [**Section 6:** Auth Middleware](skills/backend.md#6-security-best-practices) |
| **Database Patterns** | "Apply Repository pattern" | [**Section 7.1:** Repository Pattern](skills/backend.md#71-repository-pattern) |
| **Transactions** | "Manage atomic transactions" | [**Section 7.2:** Transaction Handling](skills/backend.md#72-transaction-handling) |
| **Performance** | "Integrate Redis caching" | [**Section 8.2:** Caching (Redis)](skills/backend.md#82-caching-redis) |
| **Error Handling** | "Global error handler and AppError" | [**Section 9:** Error Handling](skills/backend.md#9-error-handling) |
| **Folder Structure** | "Domain-driven file structure" | [**Section 3:** Project Structure](skills/backend.md#3-project-structure) |
| **Tech Stack** | "Hono.js / Modern Stack" | [**Section 1:** Tech Stack & Tools](skills/backend.md#1-tech-stack--tools) |

---

## 1.5 📱 Mobile - Cross-Platform App
**File:** [skills/mobile.md](skills/mobile.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Setup & Project** | "Create React Native or Flutter project" | [**Section 2.1 / 3.1:** Project Structure](skills/mobile.md#2-react-native-best-practices) |
| **Component Standard** | "Write modern, performant component" | [**Section 2.2 / 3.2:** Best Practices](skills/mobile.md#22-functional-components--hooks) |
| **Performance** | "Use FlashList or RepaintBoundary" | [**Section 2.3 / 3.3:** Performance Optimization](skills/mobile.md#23-performance-optimization) |
| **State Management** | "Integrate Zustand or Riverpod" | [**Section 2.4 / 3.4:** State Management](skills/mobile.md#24-state-management-zustand) |
| **Navigation** | "Design Stack/Tab navigation" | [**Section 2.6 / 3.5:** Navigation](skills/mobile.md#26-navigation-react-navigation) |
| **Security** | "Store Tokens in Secure Store" | [**Section 4.1:** Secure Storage](skills/mobile.md#41-secure-storage) |
| **API Security** | "Apply certificate pinning" | [**Section 4.2:** API Security](skills/mobile.md#42-api-security) |
| **Platform Features** | "Camera/Location permission and logic" | [**Section 5:** Platform-Specific Code](skills/mobile.md#5-platform-specific-code) |
| **Offline First** | "Work without internet strategy" | [**Section 4:** Mobile Security & Storage](skills/mobile.md#4-mobile-security) |

---

## 1.6 🧪 Testing - TDD and Test Strategies
**File:** [skills/testing.md](skills/testing.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Strategy Setup** | "How should test pyramid be?" | [**Section 1:** Test Pyramid](skills/testing.md#1-test-pyramid) |
| **Unit Test** | "Test function/component with Jest" | [**Section 2:** Unit Testing (Jest)](skills/testing.md#2-unit-testing-jest) |
| **Mocking** | "Mock API call" | [**Section 2.2:** Mocking](skills/testing.md#22-mocking) |
| **Integration Test** | "Write API endpoint test (Supertest)" | [**Section 3:** Integration Testing](skills/testing.md#3-integration-testing) |
| **E2E Test** | "Test login flow with Playwright" | [**Section 4:** E2E Testing (Playwright)](skills/testing.md#4-e2e-testing-playwright) |
| **Visual Test** | "Catch UI shifts" | [**Section 5:** Visual Regression Testing](skills/testing.md#5-visual-regression-testing) |
| **TDD Workflow** | "Apply Red-Green-Refactor" | [**Section 6:** TDD (Test Driven Development)](skills/testing.md#6-tdd-test-driven-development) |
| **Best Practices** | "AAA pattern and isolation rules" | [**Section 7:** Test Writing Rules](skills/testing.md#7-test-writing-rules) |
| **Quality Control** | "Analyze coverage" | [**Section 8:** Control Checklist](skills/testing.md#8-control-checklist) |

---

## 1.7 🔍 Debugging - Troubleshooting Protocol
**File:** [skills/debugging.md](skills/debugging.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Reproduce (Replay)** | "Reproduce the error step by step" | [**Section 2:** Phase 1 - Reproduce](skills/debugging.md#2-phase-1-reproduce) |
| **Root Cause (RCA)** | "Why did the problem occur?" | [**Section 3/5:** Root Cause Analysis](skills/debugging.md#3-phase-2-understand) |
| **Isolation** | "Narrow area with binary search" | [**Section 4:** Phase 3 - Isolate](skills/debugging.md#4-phase-3-isolate) |
| **Hypothesis Test** | "Test most probable cause" | [**Section 5:** Phase 4 - Hypothesize](skills/debugging.md#5-phase-4-hypothesize) |
| **Network Debugging** | "Examine API requests" | [**Section 6.3:** Network Debugging](skills/debugging.md#63-network-debugging) |
| **Logging** | "Add structured log" | [**Section 9.2:** Structured Logging](skills/debugging.md#92-structured-logging) |
| **Common Patterns** | "Null reference or Race condition" | [**Section 5.2:** Common Bug Patterns](skills/debugging.md#52-common-bug-patterns) |
| **Post-Mortem** | "Write incident report" | [**Section 8:** Phase 7 - Reflect](skills/debugging.md#8-phase-7-reflect) |
| **Tools** | "Use VS Code debugger" | [**Section 6:** Phase 5 - Fix & Tools](skills/debugging.md#6-phase-5-fix--tools) |
| **Race condition** | "Data sometimes comes wrong" | [**Section 5:** Common Bug Patterns](skills/debugging.md#5-phase-4-hypothesize) |
| **Production bug** | "Error only occurs in production" | [**Section 8:** REFLECT (Post-Mortem)](skills/debugging.md#8-phase-7-reflect) |
| **Regression** | "Old feature broke" | [**Section 4.1:** Binary Search](skills/debugging.md#4-phase-3-isolate) |

---

## 1.8 ♻️ Refactoring - Code Improvement
**File:** [skills/refactoring.md](skills/refactoring.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Timing** | "Should I refactor now?" | [**Section 2:** When to Refactor](skills/refactoring.md#2-when-to-refactor) |
| **Code Smells** | "Long method or duplication" | [**Section 5:** Code Smells](skills/refactoring.md#5-code-smells) |
| **Process** | "Proceed with small steps" | [**Section 3:** Refactoring Process](skills/refactoring.md#3-refactoring-process-small-steps) |
| **Extract Patterns** | "Split function (Extract Method)" | [**Section 4.1:** Extract Function](skills/refactoring.md#41-extract-function) |
| **Rename & Simplify** | "Fix variable name" | [**Section 4.2:** Rename Variable](skills/refactoring.md#4-common-refactoring-patterns) |
| **DRY** | "Clean repeating code" | [**Section 4.5:** Remove Duplication](skills/refactoring.md#45-remove-duplication-dry) |
| **Magic Numbers** | "Make constants from magic numbers" | [**Section 4.3:** Replace Magic Numbers](skills/refactoring.md#43-replace-magic-numbers-with-constants) |
| **Legacy Code** | "Safely change old code (Sprout)" | [**Section 7:** Incremental Refactoring](skills/refactoring.md#7-incremental-refactoring-strategy) |
| **Safe Checklist** | "Type safety and test check" | [**Section 6 / 8:** Control Checklist](skills/refactoring.md#8-control-checklist) |

---

## 1.9 🚀 Production Deployment - DevOps
**File:** [skills/production-deployment.md](skills/production-deployment.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Preparation** | "Check pre-deployment checklist" | [**Section 2:** Pre-Deployment Checklist](skills/production-deployment.md#2-pre-deployment-checklist) |
| **Pipeline Setup** | "Set up CI/CD with GitHub Actions" | [**Section 3:** CI/CD Pipeline](skills/production-deployment.md#3-cicd-pipeline) |
| **Secrets** | "Manage API key and env variables" | [**Section 3.2:** Pipeline Security](skills/production-deployment.md#32-pipeline-security) |
| **Strategy Selection** | "Apply Blue-Green or Canary" | [**Section 4:** Deployment Strategies](skills/production-deployment.md#4-deployment-strategies) |
| **Feature Flags** | "A/B test or gradual rollout" | [**Section 4.3:** Feature Flags](skills/production-deployment.md#43-feature-flags) |
| **Monitoring** | "Prometheus/Grafana metrics" | [**Section 5:** Monitoring & Observability](skills/production-deployment.md#5-monitoring--observability) |
| **Alerting** | "Send alert when error rate increases" | [**Section 5.3:** Alert Rules](skills/production-deployment.md#53-alert-rules) |
| **Rollback** | "Return to old version in emergency" | [**Section 6:** Rollback Strategy](skills/production-deployment.md#6-rollback-strategy) |
| **Security** | "Security scan and incident response" | [**Section 7:** Security & Compliance](skills/production-deployment.md#7-security--compliance) |

---

## 1.10 📁 Multi-File Sync - Multi-File Changes
**File:** [skills/multi-file-sync.md](skills/multi-file-sync.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Planning** | "This change will affect 20 files" | [**Section 2:** Change Process (Planning)](skills/multi-file-sync.md#2-multi-file-change-process) |
| **Global Rename** | "Change userId to customerId" | [**Section 3.1:** IDE Refactoring](skills/multi-file-sync.md#31-ide-refactoring-rename-symbol) |
| **Grep Check** | "Find remaining references in text" | [**Section 3.2:** Grep Check](skills/multi-file-sync.md#32-grep-check) |
| **Context** | "Lose context during refactor" | [**Section 4:** Preserve Context (Stash)](skills/multi-file-sync.md#42-git-stash-usage) |
| **Dangerous Situations** | "Interface changed, update everywhere" | [**Section 5:** Dangerous Situations](skills/multi-file-sync.md#5-dangerous-situations) |
| **Rollback** | "Things got messy, revert" | [**Section 6:** Rollback Strategies](skills/multi-file-sync.md#6-rollback-strategies) |
| **Checklist** | "Did I do everything right?" | [**Section 7:** Control Checklist](skills/multi-file-sync.md#7-control-checklist) |

---

## 1.11 📦 Dependency Management - Package Management
**File:** [skills/dependency-management.md](skills/dependency-management.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Package Selection** | "Should I use this library?" | [**Section 2:** Add Package Decision](skills/dependency-management.md#2-package-addition-decision) |
| **Audit** | "Scan for security vulnerabilities" | [**Section 3:** Security Auditing](skills/dependency-management.md#3-security-auditing) |
| **Versioning** | "Tilde (~) or Caret (^)?" | [**Section 4:** Version Management](skills/dependency-management.md#4-version-management) |
| **Upgrade** | "Safely upgrade packages" | [**Section 5:** Upgrade Strategy](skills/dependency-management.md#5-upgrade-strategies) |
| **Lock File** | "package-lock.json conflict" | [**Section 6:** Lock File Management](skills/dependency-management.md#6-lock-file-management) |
| **Cleanup** | "Delete unused packages" | [**Section 7:** Dependency Cleanup](skills/dependency-management.md#7-dependency-cleanup) |
| **Monitoring** | "Set up Dependabot" | [**Section 8:** Dependency Monitoring](skills/dependency-management.md#8-dependency-monitoring) |

---

## 1.12 📝 Documentation - Documentation
**File:** [skills/documentation.md](skills/documentation.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **README** | "Prepare project entry document" | [**Section 2:** README Best Practices](skills/documentation.md#2-readme-best-practices) |
| **Code Comments** | "Write comments in JSDoc/TSDoc format" | [**Section 3:** Code Documentation](skills/documentation.md#3-code-documentation) |
| **API Docs** | "Create Swagger/OpenAPI spec" | [**Section 4:** API Documentation](skills/documentation.md#4-api-documentation) |
| **Changelog** | "Keep version history" | [**Section 5:** Changelog & Versioning](skills/documentation.md#5-changelog--versioning) |
| **ADR** | "Record architectural decision" | [**Section 6.1:** Architecture Decision Records](skills/documentation.md#61-architecture-decision-records-adr) |
| **Diagrams** | "Draw system diagram (Mermaid)" | [**Section 6.2:** Architecture Diagrams](skills/documentation.md#62-architecture-diagrams-c4-model) |
| **Technical Writing** | "How to write more clearly?" | [**Section 7:** Technical Writing Style](skills/documentation.md#7-technical-writing-best-practices) |

---

## 1.13 ⚡ Optimization - System & Flow Optimization
**File:** [skills/optimization.md](skills/optimization.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Bottleneck Detection** | "Why is the system slow?" | [**Section 2:** Bottleneck Identification](skills/optimization.md#2-bottleneck-identification-bottleneck-identification) |
| **AI Analysis** | "Analyze code with AI" | [**Section 3:** AI-Driven Optimization](skills/optimization.md#3-ai-driven-optimization) |
| **Observability** | "Measure LCP/INP scores" | [**Section 5:** Frontend & UX Optimization](skills/optimization.md#5-frontend--user-experience-optimization) |
| **Backend Tuning** | "Fix N+1 query issue" | [**Section 6:** Backend & Database Tuning](skills/optimization.md#6-backend--database-optimization) |
| **Improvement Loop** | "Measure → Analyze → Improve" | [**Section 7:** Systematic Improvement Loop](skills/optimization.md#7-systematic-improvement-loop) |
| **Principles** | "Avoid premature optimization" | [**Section 1:** Optimization Principles](skills/optimization.md#1-optimization-principles-2025) |
| **Observability Tools** | "Set up OpenTelemetry" | [**Section 4:** Modern Observability](skills/optimization.md#4-modern-observability-observability) |

---

## 1.14 🔍 SEO Fundamentals - Core Principles & E-E-A-T
**File:** [skills/seo-fundamentals.md](skills/seo-fundamentals.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **2025 Algorithm Updates** | "What are March 2025 Core Update effects?" | [**Section 1:** 2025 SEO Fundamentals](skills/seo-fundamentals.md#1-2025-seo-fundamentals--updates) |
| **E-E-A-T Implementation** | "How do I add E-E-A-T to my content?" | [**Section 2:** E-E-A-T Principles](skills/seo-fundamentals.md#2-e-e-a-t-principles) |
| **Content Quality** | "Add author bio and credentials" | [**Section 2.3:** E-E-A-T Improvement](skills/seo-fundamentals.md#23-e-e-a-t-improvement-strategies) |
| **AI Content Guidelines** | "How to publish AI content?" | [**Section 3:** AI Content Guidelines](skills/seo-fundamentals.md#3-ai-content-guidelines) |

---

## 1.15 ⚙️ SEO Technical - Technical SEO & Core Web Vitals
**File:** [skills/seo-technical.md](skills/seo-technical.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Core Web Vitals** | "What are LCP, INP, CLS?" | [**Section 1.1:** Core Web Vitals Metrics](skills/seo-technical.md#11-core-web-vitals-metrics-2025) |
| **Site Structure** | "XML Sitemap and robots.txt setup" | [**Section 1.2:** Technical SEO Checklist](skills/seo-technical.md#12-technical-seo-checklist) |
| **Page Speed** | "How to improve page speed?" | [**Section 1.2:** Page Speed Optimization](skills/seo-technical.md#12-technical-seo-checklist) |
| **Schema Markup** | "How to add Article schema?" | [**Section 1.2:** Structured Data](skills/seo-technical.md#12-technical-seo-checklist) |
| **Mobile-First** | "Mobile optimization checklist" | [**Section 2.1:** Mobile Optimization](skills/seo-technical.md#21-mobile-first-indexing) |
| **Voice Search** | "Optimize for voice search" | [**Section 2.2:** Voice Search Optimization](skills/seo-technical.md#22-voice-search-optimization) |

---

## 1.16 ✍️ SEO Content - Content Strategy & On-Page SEO
**File:** [skills/seo-content.md](skills/seo-content.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Keyword Research** | "How do I find target keywords?" | [**Section 1:** Keyword Research & Strategy](skills/seo-content.md#1-keyword-research--strategy) |
| **Title Tag** | "How to write SEO-friendly title?" | [**Section 2.1:** Title Tag Optimization](skills/seo-content.md#21-title-tag-optimization) |
| **Meta Description** | "Meta description best practices" | [**Section 2.2:** Meta Description](skills/seo-content.md#22-meta-description) |
| **Header Tags** | "H1, H2, H3 hierarchy" | [**Section 2.3:** Header Tags](skills/seo-content.md#23-header-tags-h1-h6) |
| **URL Structure** | "How does SEO-friendly URL look?" | [**Section 2.4:** URL Structure](skills/seo-content.md#24-url-structure) |
| **Image SEO** | "Image optimization" | [**Section 2.5:** Image Optimization](skills/seo-content.md#25-image-optimization) |
| **Internal Linking** | "Internal link strategy" | [**Section 2.6:** Internal Linking](skills/seo-content.md#26-internal-linking) |
| **Topic Clusters** | "Pillar content model" | [**Section 3.1:** Topic Cluster Model](skills/seo-content.md#31-topic-cluster-model) |
| **Content Brief** | "Content planning template" | [**Section 3.2:** Content Brief Template](skills/seo-content.md#32-content-brief-template) |

---

## 1.17 📍 SEO Local - Local SEO & Geographic Optimization
**File:** [skills/seo-local.md](skills/seo-local.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Google Business Profile** | "How to optimize GBP?" | [**Section 2:** Google Business Profile](skills/seo-local.md#2-google-business-profile) |
| **NAP Consistency** | "Name-Address-Phone consistency" | [**Section 1.2:** NAP Consistency](skills/seo-local.md#12-nap-consistency-name-address-phone) |
| **Hyper-Local** | "Neighborhood level targeting" | [**Section 3:** Hyper-Local Targeting](skills/seo-local.md#3-hyper-local-targeting) |
| **Citations** | "Local directory submissions" | [**Section 3.2:** Local Citations](skills/seo-local.md#32-local-citations--directories) |
| **Local Links** | "Local backlink strategies" | [**Section 4:** Local Link Building](skills/seo-local.md#4-local-link-building) |
| **Review Management** | "How to respond to Google reviews?" | [**Section 2.3:** GBP Optimization Tips](skills/seo-local.md#23-gbp-optimization-tips) |

---

## 1.18 🔗 SEO Off-Page - Link Building & Backlinks
**File:** [skills/seo-offpage.md](skills/seo-offpage.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Backlink Quality** | "What makes a good backlink?" | [**Section 1:** Backlink Quality](skills/seo-offpage.md#1-backlink-quality) |
| **Content-Driven Links** | "Create linkable asset" | [**Section 2.1:** Content-Driven Links](skills/seo-offpage.md#21-content-driven-links) |
| **Guest Blogging** | "Guest post strategy" | [**Section 2.2:** Guest Blogging](skills/seo-offpage.md#22-guest-blogging) |
| **Broken Link Building** | "Broken link method" | [**Section 2.3:** Broken Link Building](skills/seo-offpage.md#23-broken-link-building) |
| **Digital PR** | "HARO and ego bait" | [**Section 2.4 & 2.5:** HARO & PR, Digital PR](skills/seo-offpage.md#24-haro--pr) |
| **Disavow Links** | "Clean spam links" | [**Section 3:** Disavow Strategy](skills/seo-offpage.md#3-disavow-strategy) |

---

## 1.19 📊 SEO Analytics - Measurement & Reporting
**File:** [skills/seo-analytics.md](skills/seo-analytics.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **KPI Tracking** | "Which metrics should I track?" | [**Section 1:** Key Performance Indicators](skills/seo-analytics.md#1-key-performance-indicators) |
| **Search Console** | "How to use GSC?" | [**Section 2:** Google Search Console](skills/seo-analytics.md#2-google-search-console) |
| **GA4 Setup** | "How to measure organic traffic?" | [**Section 3:** Google Analytics 4](skills/seo-analytics.md#3-google-analytics-4) |
| **SEO Tools** | "Ahrefs vs SEMrush comparison" | [**Section 4:** SEO Tools](skills/seo-analytics.md#4-seo-tools) |
| **Reporting** | "How to prepare monthly SEO report?" | [**Section 5:** Reporting Framework](skills/seo-analytics.md#5-reporting-framework) |
| **Performance Analysis** | "Which keywords are winning?" | [**Section 2.2:** GSC Insights & Actions](skills/seo-analytics.md#22-gsc-insights--actions) |

---

## 1.20 🤖 GEO Fundamentals - Generative Engine Optimization
**File:** [skills/geo-fundamentals.md](skills/geo-fundamentals.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **GEO vs SEO** | "What are the differences between GEO and SEO?" | [**Section 2:** GEO vs SEO vs AEO](skills/geo-fundamentals.md#2-geo-vs-seo-vs-aeo) |
| **AI Engine Landscape** | "Which AI engines should I target?" | [**Section 3:** AI Engine Landscape](skills/geo-fundamentals.md#3-ai-engine-landscape) |
| **RAG Architecture** | "How do RAG systems work?" | [**Section 4:** RAG Architecture for GEO](skills/geo-fundamentals.md#4-rag-architecture-for-geo) |
| **GEO Metrics** | "How do I measure GEO success?" | [**Section 5:** GEO Metrics](skills/geo-fundamentals.md#5-geo-metrics) |
| **GEO Implementation** | "How do I create a GEO strategy?" | [**Section 6:** GEO Implementation Strategy](skills/geo-fundamentals.md#6-geo-implementation-strategy) |
| **Citation Optimization** | "What should I do to get cited in AI engines?" | [**Section 1:** What is GEO?](skills/geo-fundamentals.md#1-what-is-geo) |

---

## 1.21 ✍️ GEO Content - AI-Friendly Content Strategy
**File:** [skills/geo-content.md](skills/geo-content.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Entity Optimization** | "How do I create entity-based content?" | [**Section 1:** Entity-Based Content](skills/geo-content.md#1-entity-based-content) |
| **AI-Friendly Structure** | "How should content be structured for RAG?" | [**Section 2:** AI-Friendly Content Structure](skills/geo-content.md#2-ai-friendly-content-structure) |
| **Citation Optimization** | "How to create cite-worthy content?" | [**Section 3:** Citation Optimization](skills/geo-content.md#3-citation-optimization) |
| **Content Formats** | "Which content formats work in AI engines?" | [**Section 4:** Content Formats That Work](skills/geo-content.md#4-content-formats-that-work) |
| **GEO Templates** | "What are GEO content templates?" | [**Section 5:** GEO Content Templates](skills/geo-content.md#5-geo-content-templates) |
| **FAQ for GEO** | "How to write FAQ for AI engines?" | [**Section 5.2:** FAQ Page Template](skills/geo-content.md#52-faq-page-template) |

---

## 1.22 ⚙️ GEO Technical - Technical Optimization for AI Engines
**File:** [skills/geo-technical.md](skills/geo-technical.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **Structured Data for GEO** | "How to add schema markup for AI engines?" | [**Section 1:** Structured Data for GEO](skills/geo-technical.md#1-structured-data-for-geo) |
| **Schema Markup** | "Which schema types are critical for GEO?" | [**Section 2:** Schema Markup for AI Engines](skills/geo-technical.md#2-schema-markup-for-ai-engines) |
| **Content Accessibility** | "How do I make content accessible for AI crawlers?" | [**Section 3:** Content Accessibility](skills/geo-technical.md#3-content-accessibility) |
| **Site Structure for RAG** | "How should site structure be for RAG?" | [**Section 4:** Site Structure for RAG](skills/geo-technical.md#4-site-structure-for-rag) |
| **AI Crawler Optimization** | "How do I optimize for AI crawlers?" | [**Section 5:** AI Crawler Optimization](skills/geo-technical.md#5-ai-crawler-optimization) |
| **Dataset Schema** | "How to add schema for original research?" | [**Section 2.3:** Dataset Schema for Original Research](skills/geo-technical.md#23-dataset-schema-for-original-research) |

---

## 1.23 📊 GEO Analytics - AI Citation Tracking & Measurement
**File:** [skills/geo-analytics.md](skills/geo-analytics.md)

| Scenario | Example | Relevant Section |
|----------|---------|------------------|
| **GEO Metrics** | "Which GEO metrics should I track?" | [**Section 1:** GEO Metrics Framework](skills/geo-analytics.md#1-geo-metrics-framework) |
| **Citation Tracking** | "How do I track AI citations?" | [**Section 2:** AI Citation Tracking](skills/geo-analytics.md#2-ai-citation-tracking) |
| **Competitive Analysis** | "How to do GEO competitive analysis?" | [**Section 3:** Competitive Analysis](skills/geo-analytics.md#3-competitive-analysis) |
| **GEO Reporting** | "How to prepare GEO performance report?" | [**Section 4:** GEO Reporting](skills/geo-analytics.md#4-geo-reporting) |
| **Share of AI Voice** | "How do I calculate Share of AI Voice?" | [**Section 3.3:** Share of AI Voice Calculation](skills/geo-analytics.md#33-share-of-ai-voice-calculation) |

---

# 2. Skill Loading Protocol

## 2.1 Step 1: Precise Task Analysis
```
Analyze user task (e.g., "Design Button component")
    │
    ▼
Find SKILL and RELEVANT SECTION from CORE.md tables
(e.g., Skill=design-system.md, Section=#5 Component Sizing)
    │
    ▼
DON'T read the entire skill file ❌
ONLY read the relevant section and its rules ✅
```

## 2.2 Step 2: Selective Reading Protocol

**Instead of reading the entire file:**

1. **Identify Target:** Find the relevant heading (e.g., `# 5. Component Sizing`)
2. **Find Location:** Locate the heading's line number in the file (using `view_file_outline` or `grep_search`)
3. **Partial Read:** Read only that section and its sub-items (using `view_file` with startLine-endLine)

> [!TIP]
> This method preserves context limit and increases focus.

## 2.3 Step 3: Skill Not Found
```
⚠️ ERROR: "[skill-name].md" skill file not found.

Please do one of the following:
1. Show the path to the skill file
2. Create the skill file

Work CANNOT begin without Skills.
```

---

# 3. Skill Combinations

Complex tasks may require multiple skills:

| Scenario | Skill Combination | Load Order |
|----------|-------------------|-------------|
| **Complex Backend API** | ultrathink + architecture + backend | 1→2→3 |
| **New UI Component** | design-system + testing | 1→2 |
| **Production Release** | production-deployment + testing | 1→2 |
| **Large Refactoring** | ultrathink + refactoring + multi-file-sync + testing | 1→2→3→4 |
| **Mobile App Feature** | mobile + testing | 1→2 |
| **Bug Fix** | debugging + testing | 1→2 |
| **Architecture Decision** | ultrathink + architecture | 1→2 |
| **Package Upgrade** | dependency-management + testing | 1→2 |
| **Performance Improvement** | optimization + ultrathink + debugging | 1→2→3 |

---

# 4. Skills Directory Structure

```
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
    ├── debugging.md            ✅ Troubleshooting
    ├── refactoring.md          ✅ Code improvement
    ├── production-deployment.md ✅ DevOps/CI-CD
    ├── multi-file-sync.md      ✅ Multi-file changes
    ├── dependency-management.md ✅ Package management
    ├── documentation.md        ✅ Documentation
    ├── optimization.md         ✅ System & Flow Optimization
    ├── seo-fundamentals.md     ✅ SEO Core Principles & E-E-A-T
    ├── seo-technical.md        ✅ Technical SEO & Core Web Vitals
    ├── seo-content.md          ✅ Content Strategy & On-Page SEO
    ├── seo-local.md            ✅ Local SEO & Geographic Optimization
    ├── seo-offpage.md          ✅ Link Building & Backlinks
    ├── seo-analytics.md        ✅ SEO Analytics & Reporting
    ├── geo-fundamentals.md     ✅ GEO - Generative Engine Optimization
    ├── geo-content.md          ✅ GEO Content Strategy & Entity Optimization
    ├── geo-technical.md        ✅ GEO Technical & Schema Markup for AI
    └── geo-analytics.md        ✅ GEO Analytics & Citation Tracking
```

---

# 5. Critical Rules

> [!CAUTION]
> **DON'T start work without loading Skills!**

> [!WARNING]
> **STOP if skill not found!**
> Ask user for file path or request skill creation.

> [!IMPORTANT]
> **GEMINI.md rules always apply!**
> ESLint check, 2x code review must be done.

---

**Last Updated:** December 2025
**Version:** 1.3
