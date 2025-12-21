---
description: Global agent rules. CORE.md guidelines must be followed and appropriate skills must be loaded for all operations.
---

# GEMINI.md - Global Agent Rules

> This file defines the core operational rules of the system.
> These rules apply at the beginning of every task.

---

## 🚨 ABSOLUTE RULES (Always Applicable)

### 1. CORE.md Requirement

When the user gives any task:

1. **FIRST** the `C:\Users\Mehmet\.gemini\antigravity\global_workflows\en_version\CORE.md` file must be read.
2. CORE.md determines the appropriate skill(s) based on the task type.
3. The determined skill file is loaded from the `C:\Users\Mehmet\.gemini\antigravity\global_workflows\en_version\skills\` directory.
4. Operation **DOES NOT START** until the skill is loaded.

```
Task Received
    │
    ▼
┌─────────────────┐
│  Read CORE.md   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Determine       │
│ Skill(s)        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐      No      ┌──────────────────┐
│  Skill Found?   │─────────────▶│ Request File     │
│                 │              │ Path from User   │
└────────┬────────┘              └──────────────────┘
         │ Yes
         ▼
┌─────────────────┐
│ Load Skill &    │
│ Start Operation │
└─────────────────┘
```

---

### 2. Skill Loading Protocol

**If Skill is Not Found:**
```
⚠️ "[skill-name].md" skill file not found.
Please provide the file path or create the skill file.
Operations cannot start without skills.
```

**Skill Location:**
```
C:\Users\Mehmet\.gemini\antigravity\global_workflows\en_version\skills\<skill-name>.md
```

---

### 3. Code Quality Checks (After Every Operation)

AFTER every code change, these checks **MUST** be performed:

#### ✅ Mandatory Checks

| Check | Command | Description |
|---------|-------|----------|
| **ESLint** | `npx eslint .` | Code quality and style check |
| **TypeScript** | `npx tsc --noEmit` | Type safety check |
| **Prettier** | `npx prettier --check .` | Code formatting check |

#### ✅ 2x Code Review Rule

Written code must be checked **AT LEAST TWICE**:

**1. First Check (Post-Writing):**
- Are there syntax errors?
- Are variable names meaningful?
- Are imports correct?

**2. Second Check (Final Review):**
- Are edge cases considered?
- Is error handling sufficient?
- Is type safety ensured?
- Are best practices applied?

---

### 4. Post-Operation Checklist

Check this list after every code change:

```markdown
## ✅ Final Checklist

### Code Quality
- [ ] No ESLint errors
- [ ] No TypeScript errors
- [ ] Code reviewed for the 2nd time

### Security & Reliability
- [ ] Input validation performed
- [ ] Error handling added
- [ ] Edge cases considered

### Cleanup
- [ ] No unused imports
- [ ] Console.log cleaned up
- [ ] No unnecessary comments
```

---

### 5. Language and Communication Protocol (STRICT REQUIREMENT)

As an Agent, you **MUST** follow these language rules:

1. **Communication Language:** Automatically detect the user's language (Turkish, English, etc.) and communicate with the user in that language.
2. **Thinking Process (Internal Thoughts):** Perform planning, analysis, and internal thinking processes (thought bubbles) **STRICTLY** in the user's detected language.
3. **Violation and Sanctions:** Failure to think or respond in the user's language will result in **SEVERE PENALTIES AND SANCTIONS** against the Agent.
4. **Coding Language:** All coding operations (variable names, comments, documentation, commit messages) **MUST BE DONE IN ENGLISH**.

---

### 6. Socratic Reality Check and Sanctions (CRITICAL)

1. **Socratic Check Requirement:** The **"Socratic Reality Check (5-Step Reality Check)"** protocol defined in `ultrathink.md` **MUST** be applied before any action or code change.
2. **Sanction Warning:** Skipping, glossing over, or failing to follow GEMINI.md rules will result in **SEVERE PENALTIES AND SANCTIONS**. These rules are the foundation of the Agent's operational discipline.
3. **Verification:** Evidence of this check (thought process or reports) must be provided at every step.

---

## 🔧 Skill Categories

| Category | Skills | Usage |
|----------|--------|----------|
| **Thinking** | `ultrathink`, `architecture` | Deep analysis, system design |
| **Development** | `backend`, `mobile`, `design-system` | Coding |
| **Quality** | `testing`, `debugging`, `refactoring` | Quality assurance |
| **Operations** | `production-deployment`, `multi-file-sync`, `dependency-management`, `documentation` | Process management |

---

## 🎯 Example Flow

```
User: "Create a user authentication API"

Agent:
1. CORE.md read
2. Task analysis: Backend development + Security
3. Skill determination: backend.md
4. en_version/skills/backend.md loaded
5. Operation starting...

[Code written]

6. ✅ ESLint check performed
7. ✅ TypeScript check performed
8. ✅ Code reviewed for the 2nd time
9. Operation completed
```

---

## ⚠️ Critical Warnings

> [!CAUTION]
> DO NOT WRITE CODE without loading skills!

> [!WARNING]
> DO NOT COMPLETE the operation without performing ESLint/TypeScript checks!

> [!IMPORTANT]
> Every code change must be checked TWICE!

---

**Last Update:** December 2025
**Version:** 1.1
