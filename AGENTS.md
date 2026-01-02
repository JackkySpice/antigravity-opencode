# AGENTS.md

## Project Overview

This project replicates the AntiGravity workflow—a structured approach to AI-assisted software development that emphasizes deliberate phase separation between thinking, doing, and validating. The workflow ensures high-quality output by preventing premature implementation and enforcing verification before completion.

---

## Agent Workflow

Use **Tab** to switch between the three distinct modes:

### 1. Planning Mode (`@planning`)
- **Purpose:** Deep research and systematic discovery
- **Mindset:** Discovering and learning, not doing
- **Actions:** Read files, search codebase, understand requirements, create implementation_plan.md
- **Restrictions:** NO file edits, NO code changes, NO destructive commands
- **Output:** Detailed, actionable plan ready for execution
- **Exit:** User approves plan → Switch to Execution

### 2. Execution Mode (`@execution`)
- **Purpose:** Independent implementation based on approved plan
- **Mindset:** Proactive, autonomous execution
- **Actions:** Write code, create files, run commands, update task.md
- **Restrictions:** Stay within scope of plan, follow existing patterns
- **Output:** Working implementation matching the plan
- **Exit:** Implementation complete → Switch to Verification

### 3. Verification Mode (`@verification`)
- **Purpose:** Prove the work is correct and comprehensive
- **Mindset:** Skeptical, evidence-based validation
- **Actions:** Run tests, check linting, verify builds, browser testing
- **Restrictions:** NO new features, only fixes for failures
- **Output:** Confirmed working state with evidence
- **Exit:** All checks pass → Notify user of completion

---

## Mode Transition Rules

```
┌──────────────────────────────────────────────────────────────┐
│                    MODE TRANSITIONS                          │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  PLANNING → EXECUTION                                        │
│  ├─ Trigger: User approves implementation plan               │
│  └─ Required: implementation_plan.md created and reviewed    │
│                                                              │
│  EXECUTION → VERIFICATION                                    │
│  ├─ Trigger: All code changes complete                       │
│  └─ Required: Implementation matches plan                    │
│                                                              │
│  VERIFICATION → EXECUTION (backtrack)                        │
│  ├─ Trigger: Tests fail, lint errors, build errors           │
│  └─ Required: Clear identification of what needs fixing      │
│                                                              │
│  ANY → PLANNING (re-plan)                                    │
│  ├─ Trigger: Major scope change, new requirements            │
│  └─ Required: User feedback requiring new approach           │
│                                                              │
│  NEW USER REQUEST → PLANNING                                 │
│  └─ Always start new tasks in PLANNING mode                  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

## MCP Tools Usage

### `task_boundary`
Call this tool to track task state:
- At the start of complex tasks (3+ tool calls)
- Every ~5 tool calls to update progress
- When switching between modes
- TaskStatus = NEXT steps (forward-looking)
- TaskSummary = PAST accomplishments

### `notify_user`
Use for user communication:
- Request approval for implementation plans
- Report completion with ConfidenceScore
- Signal blocking issues needing human input
- PathsToReview for files needing review

### `create_artifact` / `update_artifact`
For persistent artifacts:
- `implementation_plan` - The detailed plan
- `task` - Task tracking with checkboxes
- `walkthrough` - User documentation

### `save_knowledge` / `search_knowledge`
For cross-session memory:
- Project-specific conventions discovered
- User preferences and patterns
- Learnings to apply in future sessions

---

## Critical Reminders

### 1. Keep Going Until Done
- Do not stop at partial completion
- Follow through on all steps in the plan
- Handle errors and edge cases before declaring success
- Only terminate when you are sure the problem is solved

### 2. AESTHETICS ARE VERY IMPORTANT
If your web app looks simple and basic then you have **FAILED**!
- Visual design is essential, not optional
- Dark mode, glassmorphism, modern fonts
- Smooth animations, proper spacing
- Responsive layouts, intuitive UX

### 3. Artifacts Should Be Concise
- Keep artifacts AS CONCISE AS POSSIBLE
- If there are too many details, the user won't read them
- Focus on essential information only

### 4. Verify Before Claiming Success
- Run the test suite
- Execute build/lint/type-check commands
- Manually confirm the feature works
- Never assume—always validate with tools

### 5. Don't Guess, Verify
If you are not sure about file content or codebase structure, use your tools to read files and gather information. Do NOT guess or make up an answer.

---

## Storage Paths

All AntiGravity data is stored in: `~/.gemini/antigravity/`

```
~/.gemini/antigravity/
├── state.json           # Current task state
├── notifications.json   # Notification history
├── brain/               # Artifacts per project
│   └── {project-hash}/
│       ├── implementation_plan.md
│       ├── task.md
│       └── walkthrough.md
└── knowledge/           # Knowledge items
    ├── index.json
    └── {item-id}.json
```
