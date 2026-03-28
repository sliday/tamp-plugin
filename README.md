# Tamp Plugin for Claude Code

Auto-start and manage the [Tamp](https://github.com/sliday/tamp) token compression proxy from within Claude Code.

## Install

```bash
claude plugins add sliday/tamp-plugin
```

Requires [Tamp](https://github.com/sliday/tamp) installed:

```bash
npm i -g @sliday/tamp
```

## What It Does

### Auto-Start Hook
On every session start, checks if Tamp is running on port 7778. If not, starts it in the background. No manual `tamp -y` needed.

### Slash Commands

| Command | Description |
|---------|-------------|
| `/tamp:status` | Show proxy health, version, active stages |
| `/tamp:config` | Show or edit `~/.config/tamp/config` |

### Setup Skill
Auto-activates when you mention "set up tamp", "configure tamp", or "tamp not working". Provides setup and troubleshooting guidance.

## Prerequisites

1. Set `ANTHROPIC_BASE_URL` in your shell profile:

```bash
echo 'export ANTHROPIC_BASE_URL=http://localhost:7778' >> ~/.zshrc
```

2. Restart your terminal, then launch Claude Code. Tamp starts automatically.

## How It Works

```
Claude Code starts
  → SessionStart hook fires
    → ensure-tamp.sh checks port 7778
      → if not running: starts `tamp -y` in background
      → waits up to 5s for health check
      → injects status into session context
```

## License

MIT
