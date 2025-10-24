# Issuify

**IMPORTANT: Before proceeding, check if the GITHUB_PERSONAL_ACCESS_TOKEN environment variable is set.**

If `GITHUB_PERSONAL_ACCESS_TOKEN` is not set in the environment, STOP immediately and output:

```
GitHub Personal Access Token not found.

The issuify plugin requires a GitHub PAT because the GitHub MCP server doesn't support OAuth.

Setup instructions:

1. Create a GitHub PAT at https://github.com/settings/tokens
   Required scope: repo

2. Set the environment variable:
   export GITHUB_PERSONAL_ACCESS_TOKEN="your_token_here"

3. Add to your shell profile to persist across sessions:
   echo 'export GITHUB_PERSONAL_ACCESS_TOKEN="your_token_here"' >> ~/.zshrc

4. Restart Claude Code after setting the variable

Then run /issuify again.
```

If the token IS set, proceed with the normal workflow:

Review all changed files since upstream branch. Include work we're aware of. Ask about unexpected changes.

Use the **GitHub Copilot MCP server** tools to create both the issue and PR:
- `mcp__github__create_issue` - Create the GitHub issue
- `mcp__github__create_pull_request` - Create the pull request

## Issue (what & why)
Write casual, precise language. No fluff. Focus on bottom line.

- **Problem**: What's broken or missing (1-2 sentences max)
- **Value**: Why it matters (1 sentence)
- **Solution**: What we're doing (2-3 bullets, not exhaustive)

Target 3-5 sentences total. Skip obvious details.

## PR (how)
Write casual, precise language. No frilly technical jargon.

- **Summary**: What changed (2-3 bullets max, technical but simple)
- **Why**: How it solves the issue (1 sentence linking back)
- **Test**: What to check (2-3 bullets, just key things)

Target 4-6 sentences total. Cut anything that doesn't add value.

## Style
- Casual but exact (like talking to a teammate)
- No fake technical voice, no marketing speak
- Skip words like "comprehensive", "robust", "ensure", "carefully"
- Bottom line first, skip exhaustive details
