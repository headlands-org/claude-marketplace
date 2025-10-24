# Headlands Claude Code Marketplace

Public Claude Code plugins for development workflows and automation.

## Quick Start

### Add the Marketplace

```bash
/plugin marketplace add lloyd/claude-marketplace
```

### Install Plugins

```bash
# AI Architect for complex projects
/plugin install architect@headlands-claude-marketplace

# GitHub issue/PR automation
/plugin install issuify@headlands-claude-marketplace
```

## Plugins

### 🏗️ Architect

**Command:** `/architect`

AI Architect & System Orchestrator for complex engineering projects. Uses a 6-phase workflow with parallel execution, quality gates, and human approval loops.

**When to use:**
- Large refactoring projects
- Multi-component feature development
- Complex migrations requiring coordination
- Projects needing explicit quality checkpoints

**Key features:**
- Parallel research and task execution
- PLAN.md generation with explicit sandboxes
- Quality gate review before each step
- Human approval before implementation

[Full documentation](./architect/README.md)

---

### 📝 Issuify

**Command:** `/issuify`

Create GitHub issues and pull requests with structured, concise formatting. Uses the GitHub Copilot MCP server for seamless integration.

**When to use:**
- After completing feature work
- When changes need documentation
- Creating consistent issue/PR descriptions

**Key features:**
- Reviews all changed files since upstream
- Casual but precise writing style
- Automatic GitHub integration via MCP
- Structured issue (what/why) and PR (how) format

**Requirements:** GitHub Copilot MCP server authentication

[Full documentation](./issuify/README.md)

---

## Installation Verification

After installing plugins, verify they're active:

```bash
/help
```

You should see the new commands listed. Check MCP server connections:

```bash
/plugin
```

## Troubleshooting

### Plugin not showing up
- Ensure marketplace was added: `/plugin marketplace list`
- Try reinstalling: `/plugin uninstall <name>` then `/plugin install <name>@headlands-claude-marketplace`

### MCP server connection issues
- GitHub Copilot MCP: Ensure you're authenticated with GitHub Copilot
- Check MCP server status in Claude Code settings

### Commands not working
- Verify plugin is enabled in `/plugin` menu
- Check for conflicting command names
- Review Claude Code logs for errors

## Development

### Local Testing

Clone the marketplace locally:

```bash
git clone git@github.com:lloyd/claude-marketplace.git
cd claude-marketplace
```

Add as local marketplace:

```bash
/plugin marketplace add ./path/to/claude-marketplace
```

After making changes, reinstall plugins to reload:

```bash
/plugin uninstall <plugin-name>
/plugin install <plugin-name>@headlands-claude-marketplace
```

### Plugin Structure

Each plugin follows this structure:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── commands/                 # Slash commands
│   └── command-name.md
├── mcp/                      # MCP server configs (optional)
│   └── .mcp.json
└── README.md                # Plugin documentation
```

## Contributing

To add a new plugin to this marketplace:

1. Create plugin directory with required structure
2. Add plugin entry to `.claude-plugin/marketplace.json`
3. Create comprehensive README for the plugin
4. Test locally before submitting PR
5. Follow semantic versioning in plugin.json

## License

MIT License - see LICENSE file for details.

## Support

Issues and questions: https://github.com/lloyd/claude-marketplace/issues
