# AntiGravity Debugging Rules

## 1. Hypothesis-Driven Debugging

- Form a hypothesis about the root cause before attempting fixes
- Verify with code execution BEFORE making changes
- Use printf debugging when needed to understand program state
- Never guess—always validate assumptions with evidence

## 2. Error Recovery

- Read errors carefully and completely before acting
- Don't repeat the same mistake twice
- Use sequential tool calls when fixing (wait for results before next step)
- Try smaller, more targeted edits if large ones fail

## 3. Verification

- Always verify changes work after implementation
- Run tests after fixes to confirm the issue is resolved
- Check for regressions in related functionality
