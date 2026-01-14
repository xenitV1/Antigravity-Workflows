# Changelog


## [0.2.0] - 2026-01-14

### Added
- **Maestro Integration:** Integrated the Maestro agent and skill structure (based on Maestro v4.1 standards).
- **Dynamic directory support:** Agents now reside in `~/.agent/agents/` and core system in `~/.gemini/antigravity/` for better user-specific context.
- **New Agents:** Added `database-architect`, `devops-engineer`, `documentation-writer`, `explorer-agent`, `game-developer`, `penetration-tester`, `performance-optimizer`, `seo-specialist`, `test-engineer`.
- **New Skills:** Expanded skill library to 35 categories including `clean-code`, `brainstorming`, `security-auditor`, etc.

### Changed
- **Major Restructuring:**
  - Migrated from legacy structure to dynamic user-home based paths.
  - Renamed `CLAUDE.md` to `GEMINI.md` as the central configuration file.
- **Documentation:**
  - Updated `ARCHITECTURE.md` to reflect the full 16-agent and 35-skill file topology.
  - Updated `README.md` with new installation scripts and dynamic paths.

