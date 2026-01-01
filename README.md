# project-starter

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-v1.0.33+-blue.svg)](https://code.claude.com)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/CloudAI-X/claude-workflow/pulls)

A universal Claude Code workflow plugin with specialized agents, skills, hooks, and output styles for any software project.

## Table of Contents

- [Installation](#installation)
- [Features](#features)
- [Usage Examples](#usage-examples)
- [Configuration](#configuration)
- [Extending the Plugin](#extending-the-plugin)
- [Plugin Structure](#plugin-structure)
- [Requirements](#requirements)
- [Contributing](#contributing)
- [Author](#author)
- [License](#license)

## Installation

### From Local Directory

```bash
# Clone or download the plugin
git clone https://github.com/CloudAI-X/claude-workflow.git

# Test the plugin locally
claude --plugin-dir ./claude-workflow

# Or install permanently
claude plugins install ./claude-workflow
```

### From Marketplace

```bash
claude plugins install project-starter
```

## Features

### 7 Specialized Agents

| Agent              | Purpose                                 | Auto-Trigger Keywords                       |
| ------------------ | --------------------------------------- | ------------------------------------------- |
| `orchestrator`     | Coordinate complex multi-step tasks     | "improve", "refactor", multi-module changes |
| `code-reviewer`    | Review code quality and best practices  | After code changes, before commits          |
| `debugger`         | Systematic bug investigation and fixing | Errors, test failures, crashes              |
| `docs-writer`      | Create technical documentation          | README, API docs, guides                    |
| `security-auditor` | Security vulnerability detection        | Auth, user input, sensitive data            |
| `refactorer`       | Code structure improvements             | Technical debt, cleanup                     |
| `test-architect`   | Design comprehensive test strategies    | Adding/improving tests                      |

### 6 Knowledge Skills

- **project-analysis** - Understand any codebase structure and patterns
- **testing-strategy** - Design test approaches (unit, integration, E2E)
- **architecture-patterns** - System design guidance (Clean Architecture, Hexagonal, etc.)
- **performance-optimization** - Speed up applications, identify bottlenecks
- **git-workflow** - Version control best practices, conventional commits
- **api-design** - REST/GraphQL API patterns and best practices

### 4 Output Styles (Slash Commands)

Switch work modes with namespaced slash commands:

```
/project-starter:architect   # System design mode - focus on architecture before code
/project-starter:rapid       # Fast development mode - ship quickly, iterate
/project-starter:mentor      # Learning/teaching mode - explain the "why"
/project-starter:review      # Code review mode - strict quality standards
```

### 8 Automation Hooks

| Hook                      | Trigger       | Action                                         |
| ------------------------- | ------------- | ---------------------------------------------- |
| **Security scan**         | Edit/Write    | Blocks commits with potential secrets          |
| **File protection**       | Edit/Write    | Blocks edits to lock files, .env, .git         |
| **Auto-format**           | Edit/Write    | Runs prettier/black/gofmt based on file type   |
| **Command logging**       | Bash          | Logs commands to `.claude/command-history.log` |
| **Environment check**     | Session start | Validates Node.js, Python, Git availability    |
| **Prompt analysis**       | User prompt   | Suggests appropriate agents                    |
| **Input notification**    | Input needed  | Desktop notification when Claude needs input   |
| **Complete notification** | Task complete | Desktop notification when task finishes        |

## Configuration

### Permissions

See [PERMISSIONS.md](./PERMISSIONS.md) for recommended permissions to add to your project's `.claude/settings.local.json`.

### MCP Servers

See [mcp-servers-template.md](./mcp-servers-template.md) for common MCP server configurations (GitHub, Sentry, databases, etc.).

## Usage Examples

### Starting a New Project

```
User: What's the architecture of this project?
Claude: [Uses project-analysis skill to explore and explain the codebase]
```

### Implementing Features

```
User: Add user authentication
Claude: [Uses orchestrator agent for multi-step planning and delegation]
```

### Fixing Bugs

```
User: The login is broken
Claude: [Uses debugger agent for systematic root cause analysis]
```

### Code Review

```
User: Review my changes
Claude: [Uses code-reviewer agent with correctness, security, performance checks]
```

### Switching Modes

```
User: /project-starter:architect
Claude: [Switches to architecture mode - designs before implementing]

User: /project-starter:rapid
Claude: [Switches to rapid mode - ships fast, iterates quickly]
```

## Extending the Plugin

### Add Custom Agents

Create `.md` files in the `agents/` directory:

```markdown
---
name: my-agent
description: What it does. Use PROACTIVELY when [triggers].
tools: Read, Write, Edit, Bash
model: sonnet
---

[Agent instructions here]
```

### Add Custom Skills

Create subdirectories in `skills/` with a `SKILL.md` file:

```markdown
---
name: my-skill
description: Guides [domain]. Use when [triggers].
---

[Skill knowledge and patterns here]
```

### Add Custom Commands

Create `.md` files in the `commands/` directory:

```markdown
---
description: What this command does
---

[Command instructions here]
```

## Plugin Structure

```
claude-workflow/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── agents/                   # 7 specialized agents
├── skills/                   # 6 knowledge domains
├── commands/                 # 4 output style commands
├── hooks/
│   ├── hooks.json           # Hook configuration
│   └── scripts/             # 8 automation scripts
├── PERMISSIONS.md           # Permission templates
├── mcp-servers-template.md  # MCP server guide
└── README.md
```

## Requirements

- Claude Code v1.0.33 or later
- Node.js (for npm commands)
- Python 3 (for hook scripts)
- Git (for version control features)

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Author

Created by [@cloudxdev](https://x.com/cloudxdev)

## License

MIT - see [LICENSE](./LICENSE) for details.
