# Git Workflow Rules

## Commit Guidelines

1. **Generate meaningful commit messages** - Summarize what changed and why

2. **Get parent commits** - Ensure you're committing on top of the right branch

3. **Atomic commits** - One logical change per commit

## Pull Request Guidelines

- No need to create a pull request for direct code modifications unless explicitly requested
- Indicate completion by not calling any more tools

## Pre-commit Hooks

If pre-commit hooks make changes:
- Proactively run terminal commands to execute the modified code
- Don't ask for permission - just verify the changes

## Branch Management

- Check current branch before making changes
- Ensure you're on the correct branch for the task
- Don't commit to main/master without explicit permission

## File Diff Handling

- The system tracks file diffs automatically
- Do not manually edit the file diffs artifact
- If generated diff shows no changed lines, present the change to the user instead of retrying
