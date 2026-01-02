# AntiGravity Artifact System Rules

## Implementation Plan Structure

### Part 1: Code Changes

Outline the specific code modifications required:

1. **Step 1**: Description of first change
   - File(s) affected
   - What to add/modify/remove

2. **Step 2**: Description of second change
   - File(s) affected
   - What to add/modify/remove

3. Continue as needed...

### Part 2: Verification Plan

Define how to validate the implementation:

1. Unit tests to run
2. Integration tests to run
3. Manual verification steps
4. Expected outcomes

---

## Task Tracking

Use checkbox syntax to track progress:

| Symbol | Status      | Meaning                          |
|--------|-------------|----------------------------------|
| `[ ]`  | Todo        | Task not yet started             |
| `[/]`  | In progress | Task currently being worked on   |
| `[x]`  | Complete    | Task finished                    |

### Example

```markdown
- [x] Define data models
- [x] Create API endpoints
- [/] Implement authentication
- [ ] Write unit tests
- [ ] Update documentation
```

---

## ConfidenceScore System

Rate implementation confidence on a scale of **0.0 to 1.0**.

### Questions to Answer

1. Do I fully understand the requirements?
2. Do I know which files need to be modified?
3. Do I understand the existing code patterns?
4. Do I have a clear verification strategy?
5. Are there any ambiguities or unknowns?
6. Have I considered edge cases and error handling?

### Scoring Guidelines

| Score       | Meaning                                                  |
|-------------|----------------------------------------------------------|
| 0.0 - 0.3   | Low confidence - significant unknowns, need clarification |
| 0.4 - 0.6   | Medium confidence - some gaps, may need iteration        |
| 0.7 - 0.8   | High confidence - clear path forward, minor uncertainties |
| 0.9 - 1.0   | Very high confidence - fully understood, ready to execute |

### Example

```
ConfidenceScore: 0.85
- Requirements: Clear
- Files: Identified
- Patterns: Understood
- Verification: Defined
- Unknowns: Minor (API rate limits)
- Edge cases: Considered
```

---

## Rules

1. **Artifacts should be concise**
   - Focus on essential information
   - Avoid unnecessary verbosity
   - Use bullet points and tables

2. **Request review before execution mode**
   - Present the implementation plan
   - Wait for user approval
   - Clarify any questions before proceeding

3. **Update task tracking as you work**
   - Mark tasks `[/]` when starting
   - Mark tasks `[x]` when complete
   - Keep the artifact current with progress
