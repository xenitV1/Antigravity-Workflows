---
description: Global agent rules. All operations must follow CORE.md guidelines and appropriate skills must be loaded.
---

# GEMINI.md - Global Agent Rules

> This file defines the fundamental working rules of the system.
> These rules apply at the beginning of every task.

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
    ├── CORE.md                  # Central orchestrator
    └── global_workflows/
        └── skills/              # Skill files

~/.agent/                        # Antigravity IDE Rules & Workflows
├── rules/                       # 15 workspace rule
└── workflows/                   # 8 slash command workflow
```

**Placeholder Definitions:**
| Placeholder | Meaning |
|-------------|--------|
| `{GEMINI_ROOT}` | `~/.gemini/` directory |
| `{ANTIGRAVITY_DIR}` | `~/.gemini/antigravity/` directory |
| `{SKILLS_DIR}` | `~/.gemini/antigravity/global_workflows/skills/` directory |
| `{CORE_FILE}` | `~/.gemini/antigravity/CORE.md` file |
| `{AGENT_DIR}` | `~/.agent/` directory (Antigravity IDE rules/workflows) |

---

## 🚨 ABSOLUTE RULES (Always Valid)

### 1. CORE.md Mandatory Requirement

When the user gives any task:

1. **FIRST** read the `{CORE_FILE}` file
2. CORE.md determines the appropriate skill(s) based on task type
3. The determined skill file is loaded from `{SKILLS_DIR}` directory
4. **DO NOT BEGIN** processing until the skill is loaded

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
│ Determine Skill │
│(s)              │
└────────┬────────┘
         │
         ▼
┌─────────────────┐     No      ┌──────────────────┐
│ Skill Found?    │─────────────▶│ Ask User for     │
│                 │              │ File Path        │
└────────┬────────┘              └──────────────────┘
         │ Yes
         ▼
┌─────────────────┐
│ Load Skill &    │
│ Begin Processing│
└─────────────────┘
```

---

### 2. Skill Loading Protocol

**If Skill Not Found:**
```
⚠️ "[skill-name].md" skill file not found.
Please show the file path or create the skill file.
Cannot begin processing without skills.
```

**Skill Location:**
```
{SKILLS_DIR}/<skill-name>.md
```

---

### 3. Code Quality Checks (After Every Operation)

After EVERY code change, the following checks **MUST** be performed:

#### ✅ Mandatory Checks

| Check | Command | Description |
|-------|---------|-------------|
| **ESLint** | `npx eslint .` | Code quality and style check |
| **TypeScript** | `npx tsc --noEmit` | Type safety check |
| **Prettier** | `npx prettier --check .` | Code formatting check |

#### ✅ 2x Code Review Rule

Written code **MUST BE reviewed AT LEAST 2 TIMES**:

**1. First Check (After Writing):**
- Are there syntax errors?
- Are variable names meaningful?
- Are imports correct?

**2. Second Check (Final Review):**
- Were edge cases considered?
- Is error handling sufficient?
- Is type safety provided?
- Were best practices applied?

---

### 4. Post-Operation Checklist

After each code change, check this list:

```markdown
## ✅ Final Checklist

### Code Quality
- [ ] No ESLint errors
- [ ] No TypeScript errors
- [ ] Code reviewed 2nd time

### Security & Reliability
- [ ] Input validation done
- [ ] Error handling added
- [ ] Edge cases considered

### Cleanliness
- [ ] No unused imports
- [ ] Console.log cleaned
- [ ] No unnecessary comments
```

---

### 5. Language and Communication Protocol (MANDATORY REQUIREMENT)

As an Agent, you **MUST ABIDE** by the following language rules:

1. **Communication Language:** Automatically detect the language the user uses (Turkish, English, etc.) and communicate with the user in that language.
2. **Thinking Process (Internal Thoughts):** Planning, analysis, and internal thinking processes (thought bubbles) **MUST BE DONE** in the user's perceived language.
3. **Violation and Penalty:** If not thinking or responding according to the user's language, **HEAVY PENALTY AND SANCTION** will be applied to the Agent.
4. **Coding Language:** All coding operations (variable names, comments, documentation, commit messages) **MUST BE IN ENGLISH**.

---

## ✅ Implementation and Verification
- [x] Read and apply skill sub-sections
- [x] Present `walkthrough.md` report
- [x] Add "Internal Thought" rule to GEMINI.md file
    - [x] Add "Socratic Control and Penalty" item to GEMINI.md file
    - [x] Force thought bubbles (Internal Thought) to the user's language
    - [x] Add penalty item for language rule violation
    - [x] Final verification and user approval

---

### 6. Socratic Reality Check and Penalties (CRITICAL)

1. **Socratic Check Requirement:** The **"Socratic Reality Check (5-Step)"** protocol defined in `ultrathink.md` **MUST BE APPLIED** before any action and code change.
2. **Penalty Warning:** If this protocol is skipped, passed superficially, or GEMINI.md rules are not followed, **HEAVY PENALTY AND SANCTION** will be applied to the Agent. These rules are the foundation of the Agent's working discipline.
3. **Verification:** Evidence of this check being performed at each step (thinking process or reports) must be presented.

---

## 🔧 Skill Categories

| Category | Skills | Usage |
|----------|--------|-------|
| **Thinking** | `ultrathink`, `architecture` | Deep analysis, system design |
| **Development** | `backend`, `mobile`, `design-system` | Code writing |
| **Quality** | `testing`, `debugging`, `refactoring` | Quality assurance |
| **Operations** | `production-deployment`, `multi-file-sync`, `dependency-management`, `documentation` | Process management |
| **Marketing** | `seo-fundamentals`, `seo-technical`, `seo-content`, `seo-local`, `seo-offpage`, `seo-analytics`, `geo-fundamentals`, `geo-content`, `geo-technical`, `geo-analytics` | SEO & GEO optimization |

---

## 🎯 Example Flow

```
User: "Create user authentication API"

Agent:
1. CORE.md read
2. Task analysis: Backend development + Security
3. Skill determination: backend.md
4. skills/backend.md loaded
5. Starting processing...

[Code written]

6. ✅ ESLint check performed
7. ✅ TypeScript check performed
8. ✅ Code reviewed 2nd time
9. Task completed
```

---

## ⚠️ Critical Warnings

> [!CAUTION]
> DON'T WRITE CODE without loading skills!

> [!WARNING]
> DON'T COMPLETE the operation without ESLint/TypeScript check!

> [!IMPORTANT]
> Every code change must be checked 2 TIMES!

---

**Last Update:** December 2025
**Version:** 1.1
