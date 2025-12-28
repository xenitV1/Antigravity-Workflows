# Antigravity Workflows - AI Agent Skills System

> Comprehensive AI Agent skill system for Antigravity IDE. Includes rules, workflows, and skills with automatic activation.

---

## 🚀 Installation

### Windows (PowerShell)

```powershell
# 1. Create directories
New-Item -ItemType Directory -Force -Path "$HOME\.gemini\antigravity\global_workflows"
New-Item -ItemType Directory -Force -Path "$HOME\.agent\rules"
New-Item -ItemType Directory -Force -Path "$HOME\.agent\workflows"

# 2. GEMINI.md -> ~/.gemini/
Copy-Item ".\GEMINI.md" "$HOME\.gemini\GEMINI.md"

# 3. CORE.md -> ~/.gemini/antigravity/
Copy-Item ".\CORE.md" "$HOME\.gemini\antigravity\CORE.md"

# 4. Skills -> ~/.gemini/antigravity/global_workflows/
Copy-Item -Recurse ".\skills" "$HOME\.gemini\antigravity\global_workflows\"

# 5. Antigravity Rules -> ~/.agent/rules/
Copy-Item ".\.agent\rules\*" "$HOME\.agent\rules\" -Recurse

# 6. Antigravity Workflows -> ~/.agent/workflows/
Copy-Item ".\.agent\workflows\*" "$HOME\.agent\workflows\" -Recurse
```

### macOS/Linux (Bash)

```bash
# 1. Create directories
mkdir -p ~/.gemini/antigravity/global_workflows
mkdir -p ~/.agent/rules
mkdir -p ~/.agent/workflows

# 2. GEMINI.md -> ~/.gemini/
cp GEMINI.md ~/.gemini/GEMINI.md

# 3. CORE.md -> ~/.gemini/antigravity/
cp CORE.md ~/.gemini/antigravity/CORE.md

# 4. Skills -> ~/.gemini/antigravity/global_workflows/
cp -r skills ~/.gemini/antigravity/global_workflows/

# 5. Antigravity Rules -> ~/.agent/rules/
cp -r .agent/rules/* ~/.agent/rules/

# 6. Antigravity Workflows -> ~/.agent/workflows/
cp -r .agent/workflows/* ~/.agent/workflows/
```

---

## 📁 Post-Installation Structure

```
~/.gemini/
├── GEMINI.md                           # Global rules
└── antigravity/
    ├── CORE.md                         # Central orchestrator
    └── global_workflows/
        └── skills/                     # 23 skill files
            ├── ultrathink.md
            ├── architecture.md
            ├── backend.md
            ├── seo-fundamentals.md
            ├── seo-technical.md
            ├── seo-content.md
            ├── seo-local.md
            ├── seo-offpage.md
            ├── seo-analytics.md
            ├── geo-fundamentals.md
            ├── geo-content.md
            ├── geo-technical.md
            ├── geo-analytics.md
            └── ...

~/.agent/                               # Antigravity IDE Native
├── rules/                              # 16 workspace rule
│   ├── ultrathink.md       (Model Decision)
│   ├── quality-gates.md    (Always On)
│   ├── backend.md          (Glob: *.ts, *.js)
│   ├── testing.md          (Glob: *.test.*)
│   └── ...
└── workflows/                          # 8 slash command
    ├── ultrathink.md       (/ultrathink)
    ├── plan.md             (/plan)
    ├── implement.md        (/implement)
    ├── review.md           (/review)
    ├── debug.md            (/debug)
    ├── test.md             (/test)
    ├── refactor.md         (/refactor)
    └── deploy.md           (/deploy)
```

---

## 🔧 Antigravity IDE Rules

### Activation Modes

| Mode | Description | Example |
|-----|-------------|---------|
| **Always On** | Always active | `quality-gates.md` |
| **Model Decision** | AI decides | `ultrathink.md`, `debugging.md` |
| **Glob** | Based on file pattern | `*.ts` -> `backend.md` |

### Rule List (16 items)

| Rule | Activation | Description |
|------|------------|-------------|
| `ultrathink.md` | Model Decision | Deep analysis protocol |
| `core-orchestrator.md` | Model Decision | Skill director |
| `quality-gates.md` | **Always On** | Quality controls |
| `backend.md` | Glob: `*.ts, *.js` | Backend development |
| `testing.md` | Glob: `*.test.*` | Test strategies |
| `debugging.md` | Model Decision | Debugging |
| `architecture.md` | Model Decision | System design |
| `refactoring.md` | Model Decision | Code improvement |
| `design-system.md` | Glob: `*.css` | UI consistency |
| `mobile.md` | Glob: `*.tsx, App.*` | Mobile development |
| `production-deployment.md` | Model Decision | DevOps/CI-CD |
| `multi-file-sync.md` | Model Decision | Multi-file |
| `dependency-management.md` | Glob: `package.json` | Package management |
| `documentation.md` | Glob: `*.md` | Documentation |
| `optimization.md` | Model Decision | Performance |
| `seo-specialist.md` | Model Decision | SEO & GEO optimization |

---

## 📚 SEO & GEO Skills

### SEO Skills (Traditional Search Engine Optimization)
| Skill | Description |
|-------|-------------|
| `seo-fundamentals.md` | 2025 algorithm updates, E-E-A-T principles |
| `seo-technical.md` | Core Web Vitals, technical SEO, mobile-first |
| `seo-content.md` | Keyword research, on-page SEO, content strategy |
| `seo-local.md` | Google Business Profile, local SEO, NAP consistency |
| `seo-offpage.md` | Link building, backlinks, digital PR |
| `seo-analytics.md` | Google Analytics 4, Search Console, reporting |

### GEO Skills (Generative Engine Optimization)
| Skill | Description |
|-------|-------------|
| `geo-fundamentals.md` | RAG architecture, AI engines (ChatGPT, Claude, Perplexity), GEO vs SEO |
| `geo-content.md` | Entity optimization, AI-friendly content, citation strategies |
| `geo-technical.md` | Structured data for AI, schema markup, crawler optimization |
| `geo-analytics.md` | AI citation tracking, generative appearance measurement |

---

## ⚡ Antigravity Workflows (Slash Commands)

| Workflow | Command | Description |
|----------|---------|-------------|
| `ultrathink.md` | `/ultrathink` | Deep thinking mode |
| `plan.md` | `/plan` | Task planning |
| `implement.md` | `/implement` | Feature development |
| `review.md` | `/review` | Code review |
| `debug.md` | `/debug` | Debugging |
| `test.md` | `/test` | Test writing |
| `refactor.md` | `/refactor` | Safe refactoring |
| `deploy.md` | `/deploy` | Production deployment |

---

## 🎯 How It Works?

### Antigravity IDE Flow

```
User gives command
        │
        ▼
┌─────────────────────────┐
│ Glob Pattern Check      │ → *.ts file? -> backend.md active
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Always On Rules         │ → quality-gates.md always active
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Model Decision          │ → Complex task? -> ultrathink.md
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│ Workflow Call           │ → /debug -> debug.md workflow
└─────────────────────────┘
```

### Workflow Chaining

```
/plan -> /ultrathink (for complex tasks)
/implement -> /plan + /test
/deploy -> /test + /review
```

---

## 📏 Rules

- ✅ ESLint/TypeScript check after every operation
- ✅ Code must be reviewed at least 2 times
- ✅ Do not start processing without loading Skill/Rule
- ✅ Socratic Reality Check (5-Step) before every action

---

## 🌍 Language Versions

| Language | Location |
|----------|----------|
| 🇺🇸 English | `./` (root) |
| 🇹🇷 Türkçe | `./tr_version/` |

---

## 📄 License

MIT License

---

**Developed by:** [@xenit-v0](https://x.com/xenit_v0)
**Version:** 2.0 (Antigravity IDE Native Support)
