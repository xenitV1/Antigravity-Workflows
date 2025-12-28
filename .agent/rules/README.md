---
description: Documentation for Agent Rules configuration and usage
---

#  Agent Rules Configuration

> This directory contains the definitions that guide the Agent's behavior, constraints, and coding standards.

##  Overview

**Rules** serve as the "conscience" of the Agent. They answer the question: **"How should I behave?"**
These settings are applied at the **System Prompt** level, ensuring consistent behavior across all tasks.

###  Key Concepts

| Concept | Description |
| :--- | :--- |
| **Global Rules** | Defined in ~/.gemini/GEMINI.md, applied to all projects. |
| **Workspace Rules** | Defined here (.agent/rules), specific to this project. |
| **Activation** | Can be Manual, Always On, or triggered by file patterns (Globs). |

##  Available Rules

| Rule File | Description |
| :--- | :--- |
| architecture.md | System design & architectural patterns |
| backend.md | Backend development standards & best practices |
| core-orchestrator.md | Central logic for managing agent operations |
| debugging.md | Debugging protocols & error handling |
| dependency-management.md | Package & dependency management rules |
| design-system.md | UI/UX guidelines & styling tokens |
| documentation.md | Documentation standards |
| geo-specialist.md | GEO (Generative Engine Optimization) for AI engines |
| mobile.md | Mobile development best practices |
| multi-file-sync.md | Guidelines for multi-file editing |
| optimization.md | Performance optimization standards |
| production-deployment.md | Deployment safety checks |
| quality-gates.md | Code quality verification criteria |
| refactoring.md | Safe refactoring guidelines |
| seo-specialist.md | Traditional SEO optimization for Google/Bing |
| testing.md | Testing strategies & requirements |
| ultrathink.md | Deep reasoning protocols |

##  Usage

To modify agent behavior:
1.  **Edit** specific .md files in this directory.
2.  **Create** new rules for specific needs.
3.  **Reference** rules in your prompt using @rule-name (e.g., @backend).