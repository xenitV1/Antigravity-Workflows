---
description: Deep analysis workflow for complex problems requiring maximum cognitive capacity
---

# UltraThink Workflow

## Description
Use this workflow for complex problems requiring deep analysis. It's essential when facing architectural decisions, debugging difficult issues, or planning major features with high uncertainty.

---

## Steps

1. **Socratic Reality Check (MANDATORY)** - Before ANY action, answer these 5 questions:
   - What EXACTLY does the user want?
   - Am I working on the correct file/location?
   - What am I about to do right now?
   - Why this way? Is there a simpler approach?
   - What could this change break?

2. **Problem decomposition** - Break down the problem into layers: Surface Level (visible symptom, user experience), Technical Level (systems involved, dependencies), and Root Cause (why it's happening, fundamental issue).

3. **Multi-perspective analysis** - Examine from different viewpoints: User (what do they need?), Developer (how maintainable?), System (performance impact?), Security (what are the risks?), Future (how will it scale?).

4. **Solution exploration** - Generate multiple solution options with approach, pros, cons, and effort estimation for each.

5. **Decision and action plan** - Select the best option with clear reasoning, define implementation steps, and identify risks with mitigations.

---

## Related Workflows
- Call `/plan` for task decomposition after analysis
- Call `/debug` which uses UltraThink for complex debugging
