# Issuify Plugin

Create GitHub issues and pull requests with structured, concise formatting using the GitHub Copilot MCP server.

## Installation

```bash
/plugin install issuify@headlands-plugin-marketplace
```

## Requirements

- GitHub Personal Access Token (PAT) with `repo` scope
- Active git repository with changes to document

## Usage

```bash
/issuify
```

The command will:
1. Review all changed files since upstream branch
2. Catalog known work from context
3. Ask about unexpected changes
4. Create a GitHub issue (what & why)
5. Create a pull request (how)

## Writing Style

Issuify enforces a **casual but precise** style:

**Good:**
> "Auth flow breaks when users spam the login button. Adds debouncing to fix race conditions."

**Bad:**
> "We have carefully implemented a comprehensive and robust solution to ensure that the authentication flow handles edge cases."

**Skip these words:**
- "comprehensive"
- "robust"
- "ensure"
- "carefully"
- "enhance"
- "improve"

## Issue Format

### Problem (1-2 sentences max)
What's broken or missing. Be specific.

### Value (1 sentence)
Why it matters. Business impact or user pain.

### Solution (2-3 bullets, not exhaustive)
What we're doing. High-level approach only.

**Target:** 3-5 sentences total

**Example:**
```
## Problem
User sessions expire mid-checkout, losing cart data. Happens ~5% of the time.

## Value
We're losing sales. Cart recovery would increase conversion 3-4%.

## Solution
- Persist cart to localStorage with 24hr TTL
- Restore on session recovery
- Add warning before timeout
```

## PR Format

### Summary (2-3 bullets max)
What changed. Technical but simple.

### Why (1 sentence)
How it solves the issue. Link back to issue.

### Test (2-3 bullets)
What to check. Key verification steps only.

**Target:** 4-6 sentences total

**Example:**
```
## Summary
- Added localStorage persistence for cart state
- Session recovery checks localStorage before clearing cart
- Toast warning appears 2min before timeout

## Why
Fixes cart data loss on session expiry (#123)

## Test
- Add items to cart, wait for session timeout, refresh → cart preserved
- Verify warning appears at 28min mark
- Clear localStorage → cart resets as expected
```

## GitHub Integration

Uses the **GitHub Copilot MCP server** tools:

- `mcp__github__create_issue` - Creates the issue
- `mcp__github__create_pull_request` - Creates the PR

The plugin automatically:
- Detects repository and branch context
- Links PR to issue
- Formats according to style guide
- Handles authentication via MCP

## Examples

### Feature Addition
```bash
/issuify
```

**Generated issue:**
> **Problem:** No way to filter search results by date. Users scroll through hundreds of old results.
>
> **Value:** Top user request. Would improve search UX significantly.
>
> **Solution:**
> - Add date range picker to search UI
> - Filter results in backend query
> - Persist filter state in URL params

### Bug Fix
```bash
/issuify
```

**Generated issue:**
> **Problem:** File upload fails for images >5MB. Error handling shows generic message.
>
> **Value:** Blocks users from uploading high-res images. Support tickets spiking.
>
> **Solution:**
> - Increase limit to 25MB
> - Add client-side size check with clear error
> - Compress images if needed

## Tips

**Let issuify review diffs:**
Don't explain what you changed. Let the command analyze your git diff and generate descriptions.

**Be honest about unexpected changes:**
If issuify asks about unexpected files, explain truthfully. It helps write better issues.

**Trust the style:**
The casual tone feels weird at first but makes issues much faster to read.

**One issue per logical change:**
If you have multiple unrelated changes, create separate branches and run `/issuify` for each.

## Configuration

### GitHub Personal Access Token Setup

The GitHub MCP server requires a Personal Access Token (PAT) because it doesn't support OAuth authentication correctly.

1. Create a GitHub PAT at https://github.com/settings/tokens with `repo` scope
2. Set the environment variable:
   ```bash
   export GITHUB_PERSONAL_ACCESS_TOKEN="your_token_here"
   ```
3. Add to your shell profile (~/.bashrc, ~/.zshrc, etc.) to persist across sessions

### MCP Server Configuration

MCP server configuration (included with plugin):

```json
{
  "mcpServers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/",
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    }
  }
}
```

The plugin will automatically read `GITHUB_PERSONAL_ACCESS_TOKEN` from your environment.

## Workflow Integration

### Standard Flow
```bash
# 1. Make your changes
git add .

# 2. Create issue and PR
/issuify

# 3. Review and merge
```

### Team Standards
Customize the format by editing `commands/issuify.md` in your plugin fork to match your team's style.

## Troubleshooting

**"MCP server not connected"**
- Verify `GITHUB_PERSONAL_ACCESS_TOKEN` is set in your environment
- Check MCP server status in Claude Code settings
- Restart Claude Code after setting the environment variable

**"No changes detected"**
- Ensure you have uncommitted changes
- Check you're on a feature branch (not main/develop)
- Verify git status shows modifications

**"Generic issue descriptions"**
- Provide more context in your code comments
- Explain non-obvious changes before running
- Give issuify hints about the business value

## Support

Issues: https://github.com/headlands-org/plugin-marketplace/issues
Label: `plugin:issuify`
