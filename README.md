# AntiGravity Workflow for OpenCode

> Replicate Google AntiGravity IDE's agentic workflow in OpenCode

This package provides a complete configuration to make OpenCode behave like Google's AntiGravity IDE, with **Planning → Execution → Verification** workflow and all the behavioral rules.

## What You Get

| AntiGravity Feature | OpenCode Implementation |
|---------------------|------------------------|
| PLANNING mode | `planning` agent - read-only research |
| EXECUTION mode | `execution` agent - full implementation |
| VERIFICATION mode | `verification` agent - test and verify |
| System prompts | `prompts/*.md` instruction files |
| Behavioral rules | `AGENTS.md` + instruction files |
| MCP tools | `antigravity-mcp-server` (optional) |

## Quick Start

### 1. Copy Configuration

```bash
# Clone this repo
git clone https://github.com/JackkySpice/antigravity-opencode
cd antigravity-opencode

# Copy to your project
cp opencode.json /path/to/your/project/
cp -r prompts /path/to/your/project/
cp -r .opencode /path/to/your/project/
cp AGENTS.md /path/to/your/project/
```

### 2. Or Install Globally

```bash
# Copy to global config
cp opencode.json ~/.config/opencode/
cp -r prompts ~/.config/opencode/
mkdir -p ~/.config/opencode/agent
cp .opencode/agent/*.md ~/.config/opencode/agent/
cp AGENTS.md ~/.config/opencode/
```

### 3. Start OpenCode

```bash
cd /path/to/your/project
opencode
```

## Usage

### Switching Modes

Use **Tab** to cycle between agents:

```
Planning → Execution → Verification → Planning ...
```

Or @ mention an agent:
```
@planning analyze this codebase
@execution implement the approved plan
@verification run all tests
```

### Workflow

1. **Planning Mode** (default)
   - Research the codebase
   - Create implementation plan
   - Ask clarifying questions
   - Request approval before coding

2. **Execution Mode** (Tab to switch)
   - Implement changes
   - Follow the plan
   - Fix errors as they arise

3. **Verification Mode** (Tab to switch)
   - Run tests
   - Check linting
   - Verify everything works

## File Structure

```
antigravity-opencode/
├── opencode.json              # Main OpenCode config
├── AGENTS.md                  # Project rules
├── prompts/
│   ├── identity.md            # Core identity prompt
│   ├── code-quality.md        # Code quality rules
│   ├── artifacts.md           # Artifact system rules
│   ├── debugging.md           # Debugging protocol
│   ├── browser-automation.md  # Browser verification rules
│   ├── web-design.md          # UI aesthetics ("Godly" dark mode)
│   ├── git-workflow.md        # Git/commit rules
│   ├── planning-agent.md      # Planning mode prompt
│   ├── execution-agent.md     # Execution mode prompt
│   └── verification-agent.md  # Verification mode prompt
├── .opencode/
│   └── agent/
│       ├── planning.md        # Planning agent (markdown)
│       ├── execution.md       # Execution agent (markdown)
│       ├── verification.md    # Verification agent (markdown)
│       └── browser.md         # Browser subagent (markdown)
└── mcp-server/                # Optional MCP tools
    └── (antigravity-mcp-server)
```

## Configuration Details

### Agents

| Agent | Mode | Temperature | Permissions |
|-------|------|-------------|-------------|
| `planning` | primary | 0.1 | Read-only, safe bash only |
| `execution` | primary | 0.3 | Full access, asks for dangerous ops |
| `verification` | primary | 0.1 | Test commands allowed, no source edits |
| `explore` | subagent | 0.1 | Read-only |
| `browser` | subagent | 0.1 | Browser automation via Playwright MCP |

### Permissions

Planning agent can only run safe commands:
- `git status`, `git log`, `git diff`, `git branch`
- `ls`, `cat`, `head`, `tail`, `grep`, `find`, `tree`, `wc`

Execution agent asks for confirmation on:
- `git push`
- `rm -rf`
- `npm publish`

Verification agent can run test commands freely.

## Browser Automation

The `browser` subagent uses Playwright MCP for web testing:

```
@browser navigate to http://localhost:3000 and verify the page loads
@browser take a screenshot of the current page
@browser click the login button and verify the form appears
```

### Browser Rules (from AntiGravity)

1. **NEVER trust claims - verify with screenshots**
2. **Check state BEFORE and AFTER actions**
3. **If page is loading, wait and screenshot again**
4. **Always check browser console for errors**

The Playwright MCP server provides:
- `navigate` - Go to URL
- `click` - Click elements
- `type` - Enter text
- `screenshot` - Capture page state
- `get_dom` - Inspect DOM structure
- Device emulation (143 presets)

## Optional: MCP Server

For additional tools (task tracking, knowledge items, artifacts), install the MCP server:

```bash
cd mcp-server
npm install
npm run build
```

Then uncomment the MCP section in `opencode.json`.

## Customization

### Change Models

Edit `opencode.json`:
```json
{
  "model": "anthropic/claude-sonnet-4-20250514",
  "agent": {
    "planning": {
      "model": "openai/gpt-4o"
    }
  }
}
```

### Add More Instructions

Add files to `prompts/` and reference them:
```json
{
  "instructions": [
    "prompts/identity.md",
    "prompts/my-custom-rules.md"
  ]
}
```

### Modify Agent Behavior

Edit the markdown files in `.opencode/agent/` or the prompt files in `prompts/`.

## Comparison with AntiGravity

| Feature | AntiGravity | This Package |
|---------|-------------|--------------|
| Planning/Execution/Verification | ✅ Built-in | ✅ Via agents |
| System prompts | ✅ Injected | ✅ Via instructions |
| Ephemeral reminders | ✅ Auto-injected | ⚠️ Via MCP (manual) |
| Model routing | ✅ Server-side | ⚠️ Per-agent config |
| Thinking budgets | ✅ API params | ❌ Not supported |
| Browser automation | ✅ Playwright | ✅ Playwright MCP |
| Artifact system | ✅ Built-in | ✅ Via MCP server |

**Coverage: ~90% of AntiGravity's workflow**

## Links

- [OpenCode Documentation](https://opencode.ai/docs)
- [AntiGravity Reverse Engineering](https://github.com/JackkySpice/antigravity-ide-reversing)
- [MCP Server](https://github.com/JackkySpice/antigravity-mcp-server)

## License

MIT
