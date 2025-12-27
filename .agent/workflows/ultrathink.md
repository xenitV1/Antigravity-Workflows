# UltraThink Workflow

## Description
Deep analysis workflow for complex problems requiring maximum cognitive capacity. Use when facing architectural decisions, debugging difficult issues, or planning major features.

---

## Invocation
```
/ultrathink [problem description]
```

---

## Steps

### Step 1: Socratic Reality Check (MANDATORY)

Before ANY action, answer these 5 questions:

1. **User Intent:** "What EXACTLY does the user want?"
2. **Context:** "Am I working on the correct file/location?"
3. **Action:** "What am I about to do right now?"
4. **Rationale:** "Why this way? Is there a simpler approach?"
5. **Ripple Effect:** "What could this change break?"

### Step 2: Problem Decomposition

Break down the problem into layers:

```
LAYER 1: Surface Level
- What is the visible symptom?
- What does the user experience?

LAYER 2: Technical Level
- What systems are involved?
- What are the dependencies?

LAYER 3: Root Cause
- Why is this happening?
- What is the fundamental issue?
```

### Step 3: Multi-Perspective Analysis

Examine from different viewpoints:

| Perspective | Questions |
|-------------|-----------|
| User | What does the user need? |
| Developer | How maintainable is this? |
| System | How does this affect performance? |
| Security | What are the risks? |
| Future | How will this scale? |

### Step 4: Solution Exploration

Generate multiple solutions:

```markdown
## Solution Options

### Option A: [Name]
- Approach: [Description]
- Pros: [Benefits]
- Cons: [Drawbacks]
- Effort: [Low/Medium/High]

### Option B: [Name]
- Approach: [Description]
- Pros: [Benefits]
- Cons: [Drawbacks]
- Effort: [Low/Medium/High]
```

### Step 5: Decision & Action Plan

```markdown
## Decision

### Selected: Option [X]
**Reason:** [Why this option was chosen]

### Implementation Steps
1. [Step 1]
2. [Step 2]
3. [Step 3]

### Risks & Mitigations
- Risk 1 -> Mitigation 1
- Risk 2 -> Mitigation 2
```

---

## Output

Deliver a comprehensive analysis including:
- Problem understanding
- Root cause identification
- Solution options with trade-offs
- Recommended action plan
- Risk assessment

---

## Related Workflows
- `/plan` - For task decomposition after analysis
- `/debug` - Uses UltraThink for complex debugging
