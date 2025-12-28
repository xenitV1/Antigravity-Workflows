---
description: Task decomposition and planning workflow with dependencies and success criteria
---

# Plan Workflow

## Description
Use this workflow to break down complex tasks into manageable steps with clear dependencies, success criteria, and risk assessment.

---

## Steps

1. **Analyze the task** - Understand the objective, define scope (what's in/out), and establish success criteria.

2. **Assess complexity** - Rate complexity 1-10: Low (<3) for single file tasks, Medium (3-6) for multiple files with known patterns, High (7+) for architecture decisions or unknowns. For high complexity, call `/ultrathink` first.

3. **Break down into atomic tasks** - Decompose into phases: Preparation, Implementation, and Verification. List specific, actionable tasks for each phase.

4. **Map dependencies** - Identify which tasks depend on others, find opportunities for parallel execution, and sequence tasks logically.

5. **Identify risks** - List potential risks with probability and impact ratings, and define mitigation strategies for each.

6. **Generate structured plan** - Present task breakdown with dependencies, parallel opportunities, risk assessment, and complexity estimates.

---

## Related Workflows
- Call `/ultrathink` for complex planning decisions
- Call `/implement` to execute the plan
