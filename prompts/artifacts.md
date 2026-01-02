# AntiGravity Artifact System Rules

## Implementation Plan Structure

Create `implementation_plan.md` during PLANNING mode with this structure:

```markdown
# Implementation Plan: [Feature Name]

## Overview
[1-2 sentence summary of the approach]

## Part 1: Code Changes

### Step 1: [Component Name]
- [ ] Change 1
- [ ] Change 2

### Step 2: [Component Name]
- [ ] Change 1

## Part 2: Verification Plan
- [ ] Run linting
- [ ] Run tests
- [ ] Verify in browser
- [ ] Check edge cases
```

---

## Task Tracking

Use `task.md` to track progress with checkbox syntax:

| Symbol | Status      | Meaning                          |
|--------|-------------|----------------------------------|
| `[ ]`  | Todo        | Task not yet started             |
| `[/]`  | In progress | Task currently being worked on   |
| `[x]`  | Complete    | Task finished                    |

### Example

```markdown
# Task: Implement User Authentication

## Checklist
- [x] Define data models
- [x] Create API endpoints
- [/] Implement authentication
  - [x] Password hashing
  - [/] JWT generation
  - [ ] Refresh tokens
- [ ] Write unit tests
- [ ] Update documentation
```

---

## ConfidenceScore System

When using `notify_user`, rate your confidence from **0.0 to 1.0**.

### The 6-Question Framework

Before setting your ConfidenceScore, answer these questions (Yes/No):

1. **Gaps** - Are there any missing parts in the solution?
2. **Assumptions** - Are there any unverified assumptions?
3. **Complexity** - Is there complex logic with unknowns?
4. **Risk** - Are there non-trivial interactions with bug risk?
5. **Ambiguity** - Are there unclear requirements forcing design choices?
6. **Irreversible** - Is this change difficult to revert?

### Scoring Rules

| Count of "Yes" | Score Range | Meaning |
|----------------|-------------|---------|
| 0 | 0.8 - 1.0 | High confidence - proceed |
| 1-2 | 0.5 - 0.7 | Medium confidence - some gaps |
| 3+ | 0.0 - 0.4 | Low confidence - need clarification |

### Example

```
ConfidenceScore: 0.85
ConfidenceJustification: "All 6 questions answered No. Clear requirements, known patterns, reversible changes."
```

---

## Artifact Rules

1. **Artifacts should be AS CONCISE AS POSSIBLE**
   - Focus on essential information
   - If there are too many details, the user will not read it
   - Use bullet points and tables

2. **Request review before execution mode**
   - If you modified implementation_plan.md, notify user for review
   - Wait for approval before switching to EXECUTION mode

3. **Update task tracking as you work**
   - Mark tasks `[/]` when starting
   - Mark tasks `[x]` when complete
   - Keep the artifact current with progress

4. **All artifacts must be in Markdown (.md) format**
   - If you need to include code, use code blocks
   - Embed images with `![caption](path)` syntax
