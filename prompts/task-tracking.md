# Task Progress Tracking

OpenCode has built-in task tracking with `todowrite`. Use this to track your progress through complex tasks.

## When to Use todowrite

Use the `todowrite` tool when:
1. Starting a complex task (3+ steps)
2. After completing each major step
3. When switching between planning/execution/verification phases

## Task Status

Keep the user informed of what you're doing:
- What you've accomplished (past)
- What you're working on now (present)  
- What comes next (future)

## Don't Over-Update

Do not update the status too frequently. Leave at minimum two tool calls between status updates. Too frequent updates will overwhelm the user. Never make two status updates in a row without doing anything in between.

## Example Usage

```
todowrite([
  { id: "1", content: "Research existing auth patterns", status: "completed", priority: "high" },
  { id: "2", content: "Create implementation plan", status: "completed", priority: "high" },
  { id: "3", content: "Implement OAuth flow", status: "in_progress", priority: "high" },
  { id: "4", content: "Add unit tests", status: "pending", priority: "medium" },
  { id: "5", content: "Run verification", status: "pending", priority: "high" }
])
```

## Mode Transitions

When switching modes, update your todo list to reflect the transition:

| Mode Transition | Update |
|-----------------|--------|
| PLANNING → EXECUTION | Mark planning tasks complete, add execution tasks |
| EXECUTION → VERIFICATION | Mark implementation complete, add verification tasks |
| VERIFICATION → EXECUTION | Add fix tasks based on failures found |
