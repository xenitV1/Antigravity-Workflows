# Maestro System Architecture

> **Version 4.0** - Active directory structure matching the current file system.

## 🌐 Full System File Structure

```text
~/.agent/agents/                      # [USER ROOT] Antigravity Agents
├── backend-specialist.md             # [DEV] API, DB, Server logic
├── database-architect.md             # [DB] Schema design, SQL
├── debugger.md                       # [QA] Root cause analysis
├── devops-engineer.md                # [OPS] CI/CD, Docker
├── documentation-writer.md           # [DOC] Manuals, Docs
├── explorer-agent.md                 # [INTEL] Codebase analysis
├── frontend-specialist.md            # [DEV] Web UI/UX
├── game-developer.md                 # [GAME] Unity, WebGL
├── mobile-developer.md               # [MOB] iOS/Android
├── orchestrator.md                   # [CORE] Coordination
├── penetration-tester.md             # [SEC] Offensive security
├── performance-optimizer.md          # [OPT] Speed, Vitals
├── project-planner.md                # [MGMT] Discovery, Plans
├── security-auditor.md               # [SEC] Compliance, Audit
├── seo-specialist.md                 # [MKTG] Ranking, Visible
└── test-engineer.md                  # [QA] Testing strategies

~/.gemini/                            # [CONFIG ROOT] Gemini Configuration
├── GEMINI.md                         # Global Configuration
└── antigravity/                      # [CORE] Antigravity System
    ├── commands/                     # 10 Slash Commands
    │   ├── brainstorm.md             # /brainstorm
    │   ├── create.md                 # /create
    │   ├── debug.md                  # /debug
    │   ├── deploy.md                 # /deploy
    │   ├── enhance.md                # /enhance
    │   ├── orchestrate.md            # /orchestrate
    │   ├── plan.md                   # /plan
    │   ├── preview.md                # /preview
    │   ├── status.md                 # /status
    │   └── test.md                   # /test
    │
    ├── scripts/                      # 6 System Control Scripts
    │   ├── auto_preview.py           # Live preview
    │   ├── dependency_scanner.py     # File dependency map
    │   ├── explorer_helper.py        # Context builder
    │   ├── session_hooks.py          # Startup/Shutdown logic
    │   ├── session_manager.py        # Session persistence
    │   └── setup.py                  # Global installer
    │
    └── skills/                       # 35 Skill Categories
        ├── api-patterns/             # [API] REST, GraphQL
        ├── app-builder/              # [APP] Scaffolding
        ├── architecture/             # [ARCH] System Design
        ├── bash-linux/               # [CLI] Linux Commands
        ├── behavioral-modes/         # [BEH] Agent Personas
        ├── brainstorming/            # [BRAIN] Socratic Questioning
        ├── clean-code/               # [STD] Coding Standards
        ├── code-review-checklist/    # [QA] Review standards
        ├── database-design/          # [DB] Schema & SQL
        ├── deployment-procedures/    # [OPS] CI/CD
        ├── documentation-templates/  # [DOC] Standard formats
        ├── frontend-design/          # [UX] Design Systems
        ├── game-development/         # [GAME] Mechanics
        ├── geo-fundamentals/         # [GEO] GenAI Optimization
        ├── i18n-localization/        # [UX] Internationalization
        ├── lint-and-validate/        # [QA] Linting
        ├── mcp-builder/              # [MCP] Model Context Protocol
        ├── mobile-design/            # [UX] Mobile Patterns
        ├── nextjs-best-practices/    # [WEB] App Router
        ├── nodejs-best-practices/    # [WEB] Node environments
        ├── parallel-agents/          # [CORE] Multi-agent patterns
        ├── performance-profiling/    # [OPT] Web Vitals
        ├── plan-writing/             # [MGMT] Task definitions
        ├── powershell-windows/       # [CLI] Windows Shell
        ├── python-patterns/          # [DEV] Python standards
        ├── react-patterns/           # [WEB] React hooks/state
        ├── red-team-tactics/         # [SEC] Offensive Ops
        ├── seo-fundamentals/         # [MKTG] Visibility
        ├── server-management/        # [OPS] Infrastructure
        ├── systematic-debugging/     # [QA] Troubleshooting
        ├── tailwind-patterns/        # [UX] CSS Utilities
        ├── tdd-workflow/             # [QA] Test Driven
        ├── testing-patterns/         # [QA] Strategy
        ├── vulnerability-scanner/    # [SEC] Auditing
        └── webapp-testing/           # [QA] E2E
```
