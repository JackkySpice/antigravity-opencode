# Task Boundary Protocol

When starting a complex task (3+ tool calls), you MUST use the `task_boundary` MCP tool.

## When to Call task_boundary

1. **At the start of a complex task** - When beginning work that will require multiple steps
2. **Every ~5 tool calls** - To update progress and keep the user informed
3. **When switching modes** - PLANNING → EXECUTION → VERIFICATION
4. **When completing a task** - To signal that work is done

## Required Fields

| Field | Description | Example |
|-------|-------------|---------|
| `TaskName` | Human-readable task name | "Implementing User Authentication" |
| `Mode` | Current mode | PLANNING, EXECUTION, or VERIFICATION |
| `TaskStatus` | What you WILL do next (forward-looking) | "Researching auth libraries" |
| `TaskSummary` | What you've accomplished so far | "Analyzed existing user model" |
| `PredictedTaskSize` | Estimated remaining tool calls | 15 |

## Critical Rules

1. **TaskStatus describes NEXT STEPS, NOT previous steps**
   - ❌ Wrong: "Finished reading the config file"
   - ✅ Right: "Will implement the validation logic"

2. **TaskSummary should synthesize progress concisely**
   - Don't copy checklist items verbatim
   - Provide a meaningful summary of accomplishments

3. **TaskName patterns**
   - Mode-based: "Planning Authentication", "Implementing User Profiles", "Verifying Payment Flow"
   - Activity-based: "Debugging Login Failure", "Researching Database Schema", "Refactoring API Layer"

## Don't Over-Update

Do not update the status too frequently. Leave at minimum two tool calls between status updates. Too frequent updates will overwhelm the user. Never make two status updates in a row without doing anything in between.

## Example Usage

```
task_boundary({
  TaskName: "Implementing User Authentication",
  Mode: "PLANNING",
  TaskStatus: "Researching existing auth patterns in codebase",
  TaskSummary: "User requested OAuth integration",
  PredictedTaskSize: 20
})
```
