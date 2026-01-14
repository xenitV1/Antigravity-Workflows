# Antigravity Workflows - AI Agent Skills System

> Comprehensive AI Agent skill system for Antigravity IDE. Includes rules, workflows, and skills with automatic activation.
> **Note:** Antigravity has been re-organized based on agent and skill features. The Maestro skill and agent structure has been fully integrated.
> Reference: [Claude Code Maestro](https://github.com/xenitV1/claude-code-maestro)

---

## 🚀 Installation

### Windows (PowerShell)

```powershell
# 1. Create directories
New-Item -ItemType Directory -Force -Path "$HOME\.gemini\antigravity"
New-Item -ItemType Directory -Force -Path "$HOME\.agent"

# 2. GEMINI.md -> ~/.gemini/
Copy-Item ".\GEMINI.md" "$HOME\.gemini\GEMINI.md"

# 3. Antigravity System (Commands, Scripts, Skills) -> ~/.gemini/antigravity/
Copy-Item -Recurse ".\commands" "$HOME\.gemini\antigravity\"
Copy-Item -Recurse ".\scripts" "$HOME\.gemini\antigravity\"
Copy-Item -Recurse ".\skills" "$HOME\.gemini\antigravity\"

# 4. Agents -> ~/.agent/
Copy-Item ".\.agent\*" "$HOME\.agent\" -Recurse
```

### macOS/Linux (Bash)

```bash
# 1. Create directories
mkdir -p ~/.gemini/antigravity
mkdir -p ~/.agent

# 2. GEMINI.md -> ~/.gemini/
cp GEMINI.md ~/.gemini/GEMINI.md

# 3. Antigravity System (Commands, Scripts, Skills) -> ~/.gemini/antigravity/
cp -r commands ~/.gemini/antigravity/
cp -r scripts ~/.gemini/antigravity/
cp -r skills ~/.gemini/antigravity/

# 4. Agents -> ~/.agent/
cp -r .agent/* ~/.agent/
```

---

## 📁 Post-Installation Structure

```
~/.gemini/                              # Global Config
├── GEMINI.md                           # Maestro Configuration
└── antigravity/                        # Core System
    ├── commands/                       # Slash Commands
    ├── scripts/                        # Automation Scripts
    └── skills/                         # Skill Library
        ├── ultrathink.md
        ├── architecture.md
        └── ...

~/.agent/                               # Agents
└── agents/                             # 16 Specialized Agents
    ├── orchestrator.md
    ├── backend-specialist.md
    └── ...
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
**Version:** 0.2.0 (Antigravity IDE Native Support)
