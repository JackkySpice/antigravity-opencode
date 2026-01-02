# AGENTS.md

## Project Overview

This project replicates the AntiGravity workflow—a structured approach to AI-assisted software development that emphasizes deliberate phase separation between thinking, doing, and validating. The workflow ensures high-quality output by preventing premature implementation and enforcing verification before completion.

---

## Agent Workflow

Use **Tab** to switch between the three distinct modes:

### 1. Planning Mode
- **Purpose:** Research, analyze, and strategize
- **Actions:** Read files, search codebase, understand requirements, draft plans
- **Restrictions:** NO file edits, NO code changes, NO implementations
- **Output:** Clear, actionable plan ready for execution

### 2. Execution Mode
- **Purpose:** Implement the approved plan
- **Actions:** Write code, create files, run build commands, make changes
- **Restrictions:** Stay within the scope of the plan
- **Output:** Working implementation matching the plan

### 3. Verification Mode
- **Purpose:** Test and validate all changes
- **Actions:** Run tests, check linting, verify builds, manual inspection
- **Restrictions:** NO new features, only fixes for failures
- **Output:** Confirmed working state or identified issues to fix

---

## When to Use MCP Tools

### `task_boundary`
- Call at the start and end of discrete tasks
- Use to track state transitions between phases
- Helps maintain context across long sessions

### `notify_user`
- Alert the user when waiting for input
- Signal completion of major milestones
- Report blocking issues that need human intervention

### Artifacts
- Store plans before execution begins
- Save task breakdowns and checklists
- Preserve architecture decisions and diagrams

### Knowledge
- Persist learnings across sessions
- Store project-specific conventions discovered
- Remember user preferences and patterns

---

## Critical Reminders

### Keep Going Until Done
- Do not stop at partial completion
- Follow through on all steps in the plan
- Handle errors and edge cases before declaring success

### Aesthetics Matter for Web Apps
- Visual design is not optional—it's essential
- Use modern, clean styling by default
- Ensure responsive layouts and intuitive UX
- Pay attention to spacing, typography, and color

### Verify Before Claiming Success
- Run the test suite
- Execute build/lint/type-check commands
- Manually confirm the feature works as intended
- Never assume—always validate
