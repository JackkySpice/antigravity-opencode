# AntiGravity Workflow for OpenCode

> Replicate Google AntiGravity IDE's agentic workflow in OpenCode

This package adds the **AntiGravity workflow** to OpenCode - a structured 3-phase approach to AI-assisted development.

## What This Adds

| Feature | OpenCode Default | With AntiGravity |
|---------|------------------|------------------|
| Primary agents | 2 (Build, Plan) | 3 (Planning, Execution, **Verification**) |
| Planning mode | Basic read-only | Read-only + restricted bash |
| Verification phase | ❌ None | ✅ Dedicated testing mode |
| Behavioral rules | ❌ None | ✅ ConfidenceScore, aesthetics, etc. |
| Artifact persistence | ❌ None | ✅ Versioned storage via MCP |
| Cross-session memory | ❌ None | ✅ Knowledge system via MCP |

## Quick Start

### 1. Copy to Your Project

```bash
git clone https://github.com/JackkySpice/antigravity-opencode
cd antigravity-opencode

# Copy config files
cp opencode.json /path/to/your/project/
cp -r prompts /path/to/your/project/
cp AGENTS.md /path/to/your/project/
```

### 2. Start OpenCode

```bash
cd /path/to/your/project
opencode
```

### 3. Use the Workflow

Press **Tab** to cycle between modes:
```
Planning → Execution → Verification → Planning...
```

Or use @mentions:
```
@planning analyze this codebase
@execution implement the plan
@verification run all tests
```

## The 3-Phase Workflow

### 1. Planning Mode
- Research the codebase
- Create implementation plan
- Ask clarifying questions
- **Cannot modify files**

### 2. Execution Mode
- Implement changes
- Follow the approved plan
- Fix errors as they arise
- **Full file access**

### 3. Verification Mode
- Run tests and linting
- Check build succeeds
- Verify changes work
- **Cannot modify source code**

## Files Included

```
antigravity-opencode/
├── opencode.json              # Main config (agents, MCP, permissions)
├── AGENTS.md                  # Workflow rules
├── prompts/
│   ├── identity.md            # Core agentic behavior
│   ├── task-tracking.md       # Progress tracking rules
│   ├── code-quality.md        # Code editing rules
│   ├── artifacts.md           # ConfidenceScore system
│   ├── debugging.md           # Debugging approach
│   ├── browser-automation.md  # Browser testing rules
│   ├── web-design.md          # UI aesthetics rules
│   ├── git-workflow.md        # Git/commit rules
│   ├── planning-agent.md      # Planning mode behavior
│   ├── execution-agent.md     # Execution mode behavior
│   └── verification-agent.md  # Verification mode behavior
└── .opencode/agent/           # Agent markdown definitions
```

## Optional: MCP Server

For additional features (versioned artifacts, cross-session knowledge), install the MCP server:

```bash
# Clone the MCP server
git clone https://github.com/JackkySpice/antigravity-mcp-server
cd antigravity-mcp-server
npm install
npm run build

# The opencode.json already references it at ./mcp-server/
# Copy it to your project or update the path
```

### MCP Tools Provided

| Tool | Purpose |
|------|---------|
| `notify_user` | User communication with ConfidenceScore |
| `create_artifact` | Versioned implementation plans |
| `save_knowledge` | Cross-session memory |
| `search_knowledge` | Search saved knowledge |
| `task_boundary` | Mode transition tracking |

## Configuration Details

### Agents

| Agent | Mode | Permissions |
|-------|------|-------------|
| `planning` | primary | Read-only, safe bash only |
| `execution` | primary | Full access, asks for dangerous ops |
| `verification` | primary | Test commands only, no source edits |
| `explore` | subagent | Read-only |
| `browser` | subagent | Playwright MCP |

### Key Behavioral Rules

1. **Keep going until done** - Don't stop at partial completion
2. **Aesthetics matter** - Web apps must look modern and polished
3. **Verify before claiming success** - Run tests, check builds
4. **Don't guess** - Use tools to verify file contents

## Comparison with AntiGravity

| Feature | AntiGravity | This Package |
|---------|-------------|--------------|
| Planning/Execution/Verification | ✅ Built-in | ✅ Via agents |
| System prompts | ✅ Injected | ✅ Via instructions |
| Browser automation | ✅ Playwright | ✅ Playwright MCP |
| Artifact system | ✅ Built-in | ✅ Via MCP |
| Cross-session memory | ✅ Built-in | ✅ Via MCP |
| Ephemeral reminders | ✅ Auto-injected | ⚠️ Via prompts |
| Thinking budgets | ✅ API params | ❌ Not supported |

**Coverage: ~95% of AntiGravity's workflow**

## Links

- [OpenCode Documentation](https://opencode.ai/docs)
- [AntiGravity Reverse Engineering](https://github.com/JackkySpice/antigravity-ide-reversing)
- [MCP Server](https://github.com/JackkySpice/antigravity-mcp-server)

## License

MIT
