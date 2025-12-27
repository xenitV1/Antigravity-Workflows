# Plan Workflow

## Description
Task decomposition and planning workflow. Breaks down complex tasks into manageable steps with clear dependencies and success criteria.

---

## Invocation
```
/plan [task description]
```

---

## Steps

### Step 1: Task Analysis

Understand the scope and requirements:

```markdown
## Task Understanding

### Objective
[What needs to be achieved]

### Scope
- In scope: [What's included]
- Out of scope: [What's excluded]

### Success Criteria
- [ ] Criterion 1
- [ ] Criterion 2
```

### Step 2: Complexity Assessment

For complex tasks, invoke `/ultrathink` first:

| Complexity | Indicators | Action |
|------------|------------|--------|
| Low (<3) | Single file, clear solution | Direct implementation |
| Medium (3-6) | Multiple files, known patterns | Plan then implement |
| High (7+) | Architecture decision, unknowns | /ultrathink first |

### Step 3: Task Breakdown

Decompose into atomic tasks:

```markdown
## Task Breakdown

### Phase 1: Preparation
- [ ] Task 1.1: [Description]
- [ ] Task 1.2: [Description]

### Phase 2: Implementation
- [ ] Task 2.1: [Description]
- [ ] Task 2.2: [Description]

### Phase 3: Verification
- [ ] Task 3.1: [Description]
- [ ] Task 3.2: [Description]
```

### Step 4: Dependency Mapping

```markdown
## Dependencies

Task 2.1 depends on: Task 1.1, Task 1.2
Task 3.1 depends on: Task 2.1, Task 2.2

### Parallel Opportunities
- Task 1.1 and Task 1.2 can run in parallel
- Task 3.1 must wait for Phase 2
```

### Step 5: Risk Identification

```markdown
## Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| Risk 1 | Medium | High | Mitigation 1 |
| Risk 2 | Low | Medium | Mitigation 2 |
```

---

## Output

A structured plan including:
- Clear task breakdown
- Dependencies identified
- Parallel execution opportunities
- Risk assessment
- Estimated complexity per task

---

## Related Workflows
- `/ultrathink` - For complex planning decisions
- `/implement` - Execute the plan
