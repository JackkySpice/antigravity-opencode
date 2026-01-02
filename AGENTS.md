# AGENTS.md - AntiGravity Workflow for OpenCode

## Overview

This configuration adds the **AntiGravity workflow** to OpenCode - a 3-phase development approach that separates planning, execution, and verification.

### What This Adds to OpenCode

| Feature | OpenCode Default | With AntiGravity |
|---------|------------------|------------------|
| Primary agents | 2 (Build, Plan) | 3 (Planning, Execution, Verification) |
| Planning restrictions | Read-only | Read-only + safe bash only |
| Verification phase | ❌ None | ✅ Dedicated testing mode |
| Behavioral rules | ❌ None | ✅ ConfidenceScore, aesthetics, etc. |
| Artifact persistence | ❌ None | ✅ MCP-based versioned storage |
| Knowledge memory | ❌ None | ✅ Cross-session persistence |

---

## The 3-Phase Workflow

Press **Tab** to cycle between agents:

```
PLANNING → EXECUTION → VERIFICATION → PLANNING...
```

### 1. Planning Mode (`@planning`)
- **Purpose:** Deep research and systematic discovery
- **Mindset:** Discovering and learning, not doing
- **Restrictions:** No file edits, only safe bash commands
- **Output:** Implementation plan ready for approval
- **Exit:** User approves → Tab to Execution

### 2. Execution Mode (`@execution`)  
- **Purpose:** Independent implementation based on plan
- **Mindset:** Proactive, autonomous execution
- **Restrictions:** Asks before dangerous commands (git push, rm -rf)
- **Output:** Working implementation
- **Exit:** Implementation complete → Tab to Verification

### 3. Verification Mode (`@verification`)
- **Purpose:** Prove the work is correct
- **Mindset:** Skeptical, evidence-based validation
- **Restrictions:** No source edits, only test commands
- **Output:** Test results and evidence
- **Exit:** All checks pass → Report to user

---

## OpenCode Tools Reference

Use these built-in tools (NOT AntiGravity tool names):

| Task | OpenCode Tool |
|------|---------------|
| Read a file | `read` |
| Create a file | `write` |
| Modify a file | `edit` |
| Run commands | `bash` |
| Find files | `glob` |
| Search contents | `grep` |
| Track progress | `todowrite` |
| Fetch web content | `webfetch` |

---

## MCP Tools (AntiGravity Additions)

These are provided by the `antigravity` MCP server:

| Tool | Purpose |
|------|---------|
| `antigravity_notify_user` | Communicate with user + ConfidenceScore |
| `antigravity_create_artifact` | Create versioned implementation plans |
| `antigravity_update_artifact` | Update artifacts with history |
| `antigravity_save_knowledge` | Persist learnings across sessions |
| `antigravity_search_knowledge` | Search saved knowledge |
| `antigravity_task_boundary` | Track mode transitions |
| `antigravity_get_agent_state` | Get current state |

---

## Critical Rules

### 1. Keep Going Until Done
Do not stop at partial completion. Only terminate when you are sure the problem is solved.

### 2. AESTHETICS ARE VERY IMPORTANT
If your web app looks simple and basic then you have **FAILED**!
- Dark mode, glassmorphism, modern fonts
- Smooth animations, proper spacing
- Responsive layouts

### 3. Artifacts Should Be Concise
Keep artifacts AS CONCISE AS POSSIBLE. If there are too many details, the user won't read them.

### 4. Verify Before Claiming Success
- Run the test suite with `bash`
- Execute build/lint/type-check commands
- Never assume—always validate with tools

### 5. Don't Guess, Verify
Use `read`, `grep`, `glob` to confirm file contents and structure. Do NOT guess or make up answers.

### 6. Use Correct Tool Names
This is OpenCode, not AntiGravity IDE. Use:
- `read` (not `view_file`)
- `write` (not `write_to_file`)
- `edit` (not `replace_file_content`)
- `bash` (not `run_command`)
- `grep` (not `grep_search`)
- `glob` (not `find_files`)

---

## ConfidenceScore System

When completing a task, rate your confidence 0.0-1.0:

**Answer these 6 questions (Yes/No):**
1. Gaps - Any missing parts?
2. Assumptions - Any unverified assumptions?
3. Complexity - Complex logic with unknowns?
4. Risk - Non-trivial interactions with bug risk?
5. Ambiguity - Unclear requirements?
6. Irreversible - Difficult to revert?

**Scoring:**
- 0.8-1.0 = No to ALL questions
- 0.5-0.7 = Yes to 1-2 questions
- 0.0-0.4 = Yes to 3+ questions

---

## File Paths

OpenCode requires **absolute paths** for all file operations. Always use full paths like `/home/user/project/src/file.ts`, not relative paths.

---

## Storage Location

AntiGravity data is stored in: `~/.gemini/antigravity/`

```
~/.gemini/antigravity/
├── state.json           # Current mode/task state
├── notifications.json   # Notification history
├── brain/               # Artifacts per project
│   └── {project-hash}/
│       ├── implementation_plan.md
│       ├── task.md
│       └── walkthrough.md
└── knowledge/           # Cross-session memory
    └── {item-id}.json
```
