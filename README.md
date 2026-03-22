# Todoist-skill

A [Claude Code](https://claude.ai/claude-code) plugin for managing [Todoist](https://todoist.com) tasks via the [`td` CLI](https://www.npmjs.com/package/todoist-cli).

## Prerequisites

Install the `td` CLI:

```bash
npm install -g todoist-cli
```

Authenticate:

```bash
td auth login
```

## Installation

### Option 1: Marketplace (recommended)

```
/plugin marketplace add rajatarya/todoist-skill
/plugin install todoist@todoist-skill
```

### Option 2: Local

```bash
git clone https://github.com/rajatarya/todoist-skill.git ~/.claude/plugins/local/todoist-skill
```

Then in Claude Code:
```
/plugin install todoist@local:todoist-skill
```

## Usage

Once installed, Claude will automatically use the skill when you mention tasks or Todoist. You can also invoke it explicitly:

```
/todoist
```

### Examples

- "What's due today?"
- "Add a task to buy groceries tomorrow"
- "Show my work project tasks"
- "Complete the deploy task"
- "What did I get done this week?"

## Permissions

Add `td` to your allowed commands in Claude Code settings:

```json
{
  "permissions": {
    "allow": ["Bash(td:*)"]
  }
}
```

## License

MIT
