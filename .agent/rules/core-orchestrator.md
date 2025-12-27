# Core Orchestrator - Skill Router

## Activation
- **Mode:** Model Decision
- **Description:** Central orchestrator that routes tasks to appropriate skills/rules. Activate when: determining which skill to use, planning multi-skill workflows, or coordinating complex tasks.

---

## Dynamic Path Detection

> **For Agent:** Replace `{WORKFLOWS_ROOT}` with the directory where this file is located.

| Placeholder | Meaning |
|-------------|---------|
| `{WORKFLOWS_ROOT}` | This file's parent directory |
| `{RULES_DIR}` | `{WORKFLOWS_ROOT}/.agent/rules/` |
| `{WORKFLOWS_DIR}` | `{WORKFLOWS_ROOT}/.agent/workflows/` |

---

## Skill Selection Matrix

### Thinking Skills
| Scenario | Rule | Activation |
|----------|------|------------|
| Complex decisions | @ultrathink.md | Model Decision |
| System design | @architecture.md | Model Decision |

### Development Skills
| Scenario | Rule | Activation |
|----------|------|------------|
| API/Backend code | @backend.md | Glob: `*.ts, *.js, src/**` |
| Mobile apps | @mobile.md | Glob: `*.tsx, screens/**` |
| UI/UX design | @design-system.md | Glob: `*.css, components/**` |

### Quality Skills
| Scenario | Rule | Activation |
|----------|------|------------|
| Testing | @testing.md | Glob: `*.test.*, *.spec.*` |
| Debugging | @debugging.md | Model Decision |
| Refactoring | @refactoring.md | Model Decision |

### Operations Skills
| Scenario | Rule | Activation |
|----------|------|------------|
| Deployment | @production-deployment.md | Model Decision |
| Multi-file changes | @multi-file-sync.md | Model Decision |
| Dependencies | @dependency-management.md | Glob: `package.json, *.lock` |
| Documentation | @documentation.md | Glob: `*.md, README*` |
| Performance | @optimization.md | Model Decision |

---

## Skill Loading Protocol

### Step 1: Task Analysis
```
User task received
    │
    ▼
Analyze intent (keywords, context)
    │
    ▼
Determine complexity (1-10)
    │
    ├── <7: Direct skill activation
    │
    └── ≥7: Invoke /ultrathink workflow first
```

### Step 2: Skill Selection
1. Match task to skill matrix above
2. Check for file patterns (Glob activation)
3. If uncertain, ask user to clarify

### Step 3: Selective Reading
- Load ONLY relevant sections (context preservation)
- Use @ references for extended content
- Preserve token limits

---

## Skill Combinations

| Complex Task | Skills Sequence |
|--------------|-----------------|
| Backend API | ultrathink → architecture → backend → testing |
| New UI Component | design-system → testing |
| Production Release | testing → production-deployment |
| Major Refactoring | ultrathink → refactoring → multi-file-sync → testing |
| Bug Fix | debugging → testing |
| Performance Issue | optimization → ultrathink → debugging |

---

## Workflow Shortcuts

| Command | Description | Skills Used |
|---------|-------------|-------------|
| `/ultrathink` | Deep analysis | ultrathink |
| `/plan` | Task decomposition | ultrathink + core |
| `/implement` | Feature build | plan + backend/mobile + testing |
| `/review` | Code review | quality-gates |
| `/debug` | Debugging session | debugging + ultrathink |
| `/test` | Test generation | testing |
| `/refactor` | Safe refactoring | refactoring + testing |
| `/deploy` | Deployment | production-deployment |

---

## Critical Rules

> **CAUTION:** Never start without loading appropriate skill!

> **WARNING:** Run quality checks after every code change!

> **IMPORTANT:** Apply Socratic Reality Check before every operation!

---

## Quality Gates (Always Apply)

After EVERY code change:
1. TypeScript: `npx tsc --noEmit`
2. ESLint: `npx eslint .`
3. Prettier: `npx prettier --check .`
4. Tests: `npm test`

Code Review (2x minimum):
1. First: Syntax, imports, naming
2. Second: Edge cases, error handling, security

---

**Version:** 1.3 (Antigravity Rule Format)
