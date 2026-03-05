# Project Template

A project starter with [Claude Code](https://claude.ai/claude-code) skill pre-configured for autonomous development.

## What's included

```
.claude/
  skills/
    solo-ship/
      SKILL.md    -- Autonomous project engine skill
```

**Solo Ship** lets Claude Code run an entire project lifecycle autonomously -- from your idea to a deployed product. You describe what you want to build, Claude handles research, requirements, tech selection, development, and deployment.

## Usage

### 1. Create a new project from this template

Click **"Use this template"** on GitHub, or:

```bash
gh repo create my-new-project --template Bruce-Kang1994/project-template --clone
cd my-new-project
```

### 2. Start Claude Code

```bash
claude
```

### 3. Describe your idea

```
I want to build a tool that [does X] for [target users] to solve [problem].
```

Claude will take it from there.

## Permission setup (optional)

For a smoother experience with fewer confirmation prompts, create `.claude/settings.json` (gitignored by default):

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Write",
      "Edit",
      "Glob",
      "Grep",
      "Bash(npm run *)",
      "Bash(npx *)",
      "Bash(git *)",
      "Bash(ls *)",
      "Bash(mkdir *)"
    ]
  }
}
```

> `.claude/settings.json` is in `.gitignore` -- your permission settings stay local and are never shared.

## License

MIT
