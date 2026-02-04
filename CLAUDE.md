# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the `~/.claude` configuration directory for Claude Code CLI. It contains:
- User settings and preferences
- Plugin installations and configurations
- Session history and state
- Project-specific overrides
- Custom keybindings
- Background task management

## Directory Structure

### Core Configuration Files
- **settings.json** - Main configuration file containing permissions, enabled plugins, and user preferences
- **keybindings.json** - Custom keyboard shortcuts organized by context (Global, Chat, Autocomplete, etc.)
- **.gitignore** - Defines which files are tracked in version control

### Key Directories
- **plugins/** - Plugin system with marketplace cache and installed plugins
  - `cache/` - Downloaded plugin files from claude-plugins-official
  - `marketplaces/` - Plugin marketplace definitions
  - `installed_plugins.json` - Registry of installed plugins with versions and install paths
- **projects/** - Per-project session data, organized by directory path (with special encoding for paths)
- **plans/** - Saved plan mode files (markdown format with randomly generated names)
- **todos/** - Task lists and todo items organized by agent/session ID (JSON format)
- **session-env/** - Session-specific environment snapshots
- **shell-snapshots/** - Shell environment captures for bash tool consistency
- **file-history/** - File modification history organized by session
- **history.jsonl** - Command history in JSON Lines format
- **debug/** - Debug logs and diagnostic information
- **cache/** - Cached data including changelog.md
- **telemetry/** - Usage analytics and statistics
- **statsig/** - Feature flag and experiment data
- **ide/** - IDE integration lock files
- **downloads/** - Downloaded resources
- **paste-cache/** - Temporary storage for pasted content

## Settings Configuration

### Permission Model
The `settings.json` uses a permission system with three modes:
- **allow** - Auto-approve specific tool/command patterns
- **ask** - Always prompt for approval
- **defaultMode** - Fallback permission mode ("acceptEdits" for automatic edit approval)

### Permission Pattern Syntax
```
"Bash(command:subcommand:*)" - Wildcard patterns for bash commands
"Bash(git status:*)" - Allow all git status variations
"Bash(mvn test:*)" - Allow Maven test commands
```

### Currently Enabled Plugins
- **github@claude-plugins-official** - GitHub integration
- **gopls-lsp@claude-plugins-official** - Go language server
- **jdtls-lsp@claude-plugins-official** - Java language server
- **pr-review-toolkit@claude-plugins-official** - PR review capabilities

### Key Settings
- `includeCoAuthoredBy: false` - Disable co-author attribution in commits
- `autoAllowBashIfSandboxed: true` - Auto-approve bash commands in sandboxed mode
- `gitAttribution: false` - Disable git attribution in commits
- `enabled: true` - Claude Code is enabled

## Keybindings

Custom keybindings are organized by context. Key contexts include:
- **Global** - `ctrl+t` (toggle todos), `ctrl+o` (toggle transcript), `ctrl+r` (history search)
- **Chat** - `enter` (submit), `shift+tab` (cycle mode), `ctrl+g` (external editor)
- **Task** - `ctrl+b` (background task)
- **Confirmation** - `y`/`n` for yes/no, `ctrl+e` (toggle explanation)

## Working with This Repository

### Modifying Settings
Edit `settings.json` to:
- Add/remove allowed bash commands or tools
- Enable/disable plugins
- Configure permission modes
- Adjust auto-accept behaviors

### Managing Plugins
- View installed plugins: Check `plugins/installed_plugins.json`
- Plugin cache location: `plugins/cache/claude-plugins-official/`
- Marketplace sources: `plugins/marketplaces/`

### Session Management
- Sessions are stored per-project in `projects/` using encoded directory names
- Session data includes conversation history, file changes, and task state
- Plans created in plan mode are saved to `plans/` with descriptive names

### Debugging
- Debug logs: `debug/` directory
- Shell snapshots for reproducibility: `shell-snapshots/`
- Session environment state: `session-env/`

## Development Workflows

### Configuration Testing
When modifying settings:
1. Edit the relevant JSON file (settings.json, keybindings.json)
2. Settings take effect immediately without restart
3. Validate with `/doctor` command if issues occur

### Plugin Development
- Local plugin testing uses the marketplace system
- Plugin definitions include frontmatter with metadata
- Plugins can provide commands, agents, hooks, and MCP servers

### History and State
- Command history: `history.jsonl` (JSON Lines format)
- File modifications tracked per session in `file-history/`
- Background tasks and todos organized by agent ID

## Important Notes

- This directory should remain in the home directory (`~/.claude`)
- Session data is project-specific and stored with encoded path names
- Plugin updates are managed through the marketplace system
- Shell snapshots ensure consistent bash tool execution across sessions
- Plans and todos are automatically cleaned up based on retention policies